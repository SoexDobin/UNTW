
## 1 이동구현코드
1. transform.Translate 로컬 포지션을 통한 이동구현
```
transform.Translate(new Vector3(Speed1 * Time.deltaTime, 0, 0));
```
2. AddForce 물리함수를 통한 이동구현
```
rigid.AddForce(new Vector2(Speed2, 0), ForceMode2D.Impulse);
```
3. Rigidbody2D가 가진 velocity(속도)값을 통한 이동구현
```
rigid.velocity = new Vector2(Speed3 , 0);
```

## 2 점프코드와 2d 충돌인식방식
* 점프
  1. velocity 속도값을 통한구현
  ```
  rigid.velocity = new Vector2(0, Jump);
  ```
  2. AddForce()함수로 충격을 주는 방식
  ```
  rigid.AddForce(new Vector2(0, Jump), ForceMode2D.Impulse) ;
  ```
* 충돌인식방식
  1. Colision 물리력이 있는 객체와 충돌하면 반환하는 함수
  ```
  private void OnCollisionEnter2D(Collision2D object){}
  private void OnCollisionStay2D(Collision2D object){}
  private void OnCollisi nExit2D(Collision2D object){}
  // kenematic 속성이 꺼져 있어야함
  // Kinematic: 외부에서 가해지는 물리적 힘에 반응하지 않음
  ```
  2. Trigger 두 오브젝트 간의 물리적 연산을 하지 않고 충돌값을 가져오는 함수
  ```
  private void OnTriggerEnter2D(Collision2D object){}
  private void OnTriggerStay2D(Collision2D object){}
  private void OnTriggerExit2D(Collision2D object){}
  // isTrigger 속성이 꺼져 있어야함
  // isTrigger: 물리충돌을 제거하고 충돌감지만 한다.
  ```
  3. Raycast 객체에서 레이저를 발사해 다른 객체를 판별함
  ```
  RaycastHit2D rayHit = Physics2D.Raycast(rigid.position, Vector3.down, 1, LayerMask.GetMask("Water"));
  // Raycast 변수 = 2D물리의 Raycast사용 (위치, 레이저쏘는 방향, 레이저크기, 레이어 마스크)
  // 레이어 마스크는 레이어 값을 가져옴 
  ```

### 1 이동구현코드
  1.1 변수선언 목록
  ```
  int Speed1 = 5;
  float Speed2 = 0.2f;
  float Speed3 = 1.5f;
  Rigidbody2D rigid;
  SpriteRenderer spr;
  ```
  1.2 시작시 선언 목록
  ```
  void Start(){
    rigid = GetComponent<Rigidbody2D>();
    // rigid 변수에 Rigidbody2D 컴포넌트 요소들을 호출하겠다
    spr = GetComponent<SpriteRenderer>();
  }
  ```

  1.3 이동 코드

  1.3.1 transform.Translate 로컬 포지션을 통한 이동구현
  ```
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
  ```
  1.3.2 AddForce 물리함수를 통한 이동구현
  ```
  if (Input.GetKey(KeyCode.RightArrow))
  { rigid.AddForce(new Vector2(Speed2, 0), ForceMode2D.Impulse); }
    //rigid안에 AddForce함수 호출할때마다 x축으로 speed값을 줌
    // ForceMode2D는 물리를 주는 방식을 말함
    // speed를 Impulse방식 (한번에 주겠다)
  ```
  1.3.3 Rigidbody2D가 가진 velocity(속도)값을 통한 이동구현
  ```
  if(Input.GetAxisRaw("Horizontal") > 0)
    //GetAxisRaw 즉발적 키입력을 받고 왼쪽화살표키는 -1 오른쪽화살표키 1을 출력함
  { rigid.velocity = new Vector2(Speed3 , 0); }
    // 리지드 속도값에 벡터값x에 Speed를 할당해줌;
  ```
  1.3.3.1 x축과 y축 값설정과 flipx 사용법
  ```
  if(Input.GetAxisRaw("Horizontal") > 0)
  {
    rigid.velocity = new Vector2(Speed3 , rigid.velocity.y);
    // x축으로 Speed가 움직일때마다. 리지드 속도값 y만큼 값을 할당
    spr.flipx = true;
    // 스프라이트 렌더러로 이동키 입력시마다 flip값을 쥐어줌
  }
  ```
### 2 점프코드와 2D타일맵객체 인식방식
  2.1 변수선언목록
  ```
  int Jump = 20;
  ```
  2.2 시작시 선언 목록
  ```
  없음
  ```
  2.3 점프코드
  2.3.1 객체에서의 속도값을 통한 점프구현
  ```
  if (Input.GetKeyDown(KeyCode.UpArrow))
    {
        rigid.velocity = new Vector2(rigid.velocity.x, Jump);
    }
  ```
  2.3.2 객체에게 충격을 주는 방식
  ```
  if (Input.GetKeyDown(KeyCode.UpArrow))
    {
        rigid.AddForce(new Vector2(rigid.velocity.x, Jump), ForceMode2D.Impulse);
    }
  ```
  2.4 2D 충돌인식방식

  2.4.1 Collision 물리작용되는 객체에 충돌 값을 가져옴 (상대 객체 isTrigger 속성 켜저야함)

  * OnCollisionEnter()
  ``` 
  private void OnCollisionEnter2D(Collision2D collision)
  // 충돌이 일어날때 호출
  // Collision객체는 (Collison2D가 부딛힌 객체를 가져옴)
  {
    if(collision.gameObject.name == "col")
    { Debug.Log("코인"); }
    // 부딛힌 객체 이름이 "col"인지 물어보고 로그를 띄움
  }
  ```
  * OnCollisionStay()
  ```
  private void OnCollisionStay2D(Collision2D collision) {}
  // 충돌이 되는 매 프레임마다 호출
  ```
  * OnCollisionExit()
  ```
  private void OnCollisionExit2D(Collision2D collision){}
   // 충돌이 끝날 때 호출
  ```

  2.4.2 Trigger 물리작용되지 않는 객체에 충돌 값을 가져옴(상대 객체 kenematic 속성 꺼져있어야함)

  * OnTriggerEnter()
  ```
  private void OnTriggerEnter2D(Collision2D collision)
  // 충돌이 일어날때 호출
  // Collision객체는 (Collison2D가 부딛힌 객체를 가져옴)
  {
    if(collision.gameObject.name == "col")
    { Debug.Log("코인통과"); }
    // 부딛힌 객체 이름이 "col"인지 물어보고 로그를 띄움
  }
  ```
  * OnTriggerStay()
  ```
  private void OnTriggerCollisionStay2D(Collision2D collision) {}
  // 충돌이 되는 매 프레임마다 호출
  ```
  * OnTriggerExit()
  ```
  private void OnTriggerExit2D(Collision2D collision){}
  // 충돌이 끝날 때 호출
  ```

  2.4.3 Raycast 객체에서 레이저를 발사해 다른 객체를 판별함
  * Raycast
  ```
  void Ray()
    {
      Debug.DrawRay(rigid.position, Vector3.down * 0.9f, new Color(0, 0, 1));
      RaycastHit2D rayHit = Physics2D.Raycast(rigid.position, Vector3.down, 1, LayerMask.GetMask("Water"));
      // Raycast 변수 = 2D물리의 Raycast사용 (위치, 레이저쏘는 방향, 레이저크기, 레이어 마스크)
      // 레이어 마스크는 레이어 값을 가져옴 
      if(rayHit.collider != null)
      {
          Debug.Log(rayHit.collider.name);
      }
    }
  ```
