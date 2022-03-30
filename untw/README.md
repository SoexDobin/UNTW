
#1 이동구현코드
1. transform.Translate 로컬 포지션을 통한 이동구현
transform.Translate(new Vector3(Speed1 * Time.deltaTime, 0, 0));
2. AddForce 물리함수를 통한 이동구현
rigid.AddForce(new Vector2(Speed2, 0), ForceMode2D.Impulse);
3. Rigidbody2D가 가진 velocity(속도)값을 통한 이동구현
rigid.velocity = new Vector2(Speed3 , 0);

# untw
#1 이동구현 코드
  1.1 변수선언 목록
  int Speed1 = 5;
  float Speed2 = 0.2f;
  float Speed3 = 1.5f;
  Rigidbody2D rigid;

  1.2 시작시 선언 목록
  void Start(){
    rigid = GetComponent<Rigidbody2D>();
    // rigid 변수에 Rigidbody2D 컴포넌트 요소들을 호출하겠다
  }

  1.3 이동 코드

  1.3.1 transform.Translate 로컬 포지션을 통한 이동구현
    if (Input.GetKey(KeyCode.RightArrow))
        // Input태그는 키보드 마우스를 눌렀을때 입력받음
        // GetKey는 누르는 기간만큼 불린값 true를 반환
        // KeyCode는 키코드를 부름
        // 입력 받겠다.키를 누르는 시간만큼.키코드 우측화살표키로
    { transform.Translate(new Vector3(Speed1 * Time.deltaTime, 0, 0)); }
        // 문장은 상대좌표를 기준으로 위치시킴이라는 정의(각 프레임마다)
        // transform은 x, y, z 포지션을 조정하는 함수
        // translate는 물체를 기준으로 물체를 이동
        // new Vector3을 선언하는 이유는 계속해서 프레임당 값을 업데이트 해야해서
        // Vector3는 당연하게도 x y 위치를 표현하며 3차원 벡터도 가져옴
        // x값은 변수 이동속도X각프레임 만큼 움직이겟단는 뜻 
        // 순간이동에 가까움

  1.3.2 AddForce 물리함수를 통한 이동구현
    if (Input.GetKey(KeyCode.RightArrow))
    { rigid.AddForce(new Vector2(Speed2, 0), ForceMode2D.Impulse); }
        //rigid안에 AddForce함수 호출할때마다 x축으로 speed값을 줌
        // ForceMode2D는 물리를 주는 방식을 말함
        // speed를 Impulse방식 (한번에 주겠다)

  1.3.3 Rigidbody2D가 가진 velocity(속도)값을 통한 이동구현
    if(Input.GetAxisRaw("Horizontal") > 0)
    //GetAxisRaw 즉발적 키입력을 받고 왼쪽화살표키는 -1 오른쪽화살표키 1을 출력함
      { rigid.velocity = new Vector2(Speed3 , 0); }
      // 리지드 속도값에 벡터값x에 Speed를 할당해줌;

