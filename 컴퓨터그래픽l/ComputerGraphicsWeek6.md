# 6주차 

## 전경색과 배경색 단축키
* [D] : 전경색과 배경색 색 지정
* [X] : 전경색과 배경색 색 반전

## 이미지 모드 이해하기
* 이미지 모드(Image Mode) : 이미지의 색을 표현하는 방식

**이미지 표현방식 중 중요한 3가지**   
* **흑백 음영 : 일반적인 흑백 이미지로 표현. 256단계의 흑백 명암을 표현**
* **RGB 색상 : 빛의 3원색인 RGB를 기본 색상으로 하여 가산혼합방식으로 이미지를 표현**
* **CMYK 색상 : 잉크의 3원색 원리를 사용하여 CMYK를 기본적으로 한 감산혼합방식으로 이미지 표현**

* 비트맵 : 완전한 검정 흰색으로만 이미지표현
* 이중톤 : 검정 잉크 외에 한 가지 색을 더 사용하여 표현(색상이 가미된 흑백사진)
* 인덱스 색상 : 256개의 한정된 색상으로 컬러 이미지 표현
* LAB 색상 : 색 파괴를 최소화 하고 색상 변화를 적게하기 위한 RGB & CMYK 장점을 활용한 방식
* 다중 채널 : 녹청(Cyan), 자주(Magenta), 노랑(Yellow) 채널로 색상 요소를 분리할 수 있는 방식

## 조정메뉴를 사용하여 이미지 보정하기
* **명도/대비 : 밝기와 선명도**
* 반전 : 기존색을 보색으로 만듬
* 포스터화 : 사용하는 색상을 줄여 포스터 화
* 한계값 : 기준값을 기준으로 밝으면 흰색 어두우면 검은색으로 표현
* 그레이디언트 맵 : 여러 색을 자연스럽게 섞어 밝기에 따른 그레이디언트 색상 적용
* 선택 색상 : 특정 색의 양을 더하거나 빼고 & 다른 색으로 수정이 가능함
* 밝은 영역/어두운 영역 : 이미지톤을 안정화
* HDR토닝 : 8비트 jpg 포토 이미지 보다 다이나믹한 느낌을 나타내는 HDR 포토 이미지로 랜더링
* **채도 감소 : 이미지를 흑백화 함**
* 색상 일치 : 주어진 이미지를 다른 이미지와 비슷한 색상의 느낌으로 보정
* **색상 대체 : 특정 색을 지정하여 영역을 선택 후 색조, 채도, 밝기를 변경(주로 색상을 변경할 때)**
* 균일화 : 이미지 명암의 단계를 조정, 이미지 명도를 고르게 함

## 밝기 조절을 위한 메뉴 -시험
1. 밝기/대비(Brightness/Contrast) : [이미지] -> [조정] -> [밝기/대비]
2. 레벨(Levels) : [이미지] -> [조정] -> [레벨]
    - 이미지의 빛과 색의 농도를 표현해 놓은 막대그래프로 [Input Levels] (입력 레벨)을 조절하여 빛과 색의 농도를 조절
3. 곡선(Curves) : [이미지] -> [조정] -> [곡선]
    - 대비와 하이라이트 조정
    - S 라인으로 조정하면 대비가 강력해짐
4. 노출(Exposure) : [이미지] -> [조정] -> [노출]
    - 노출 : 빛의 양
    - 오프셋 : 중간톤 대비를 조절
    - 감마 : 명암 대비
5. HDR 토닝 : [이미지] -> [조정] -> [HDR토닝]
    - 이미지에서 가장 밝고 어두운 부분의 농도차 결정
6. 균일화(Equalize) : [이미지] -> [조정] -> [균일화]
    - 자동으로 평균값의 밝기와 어둡기 조정


## 색상 조절을 위한 메뉴 -시험
1. 활기(Vibrance) : [이미지] -> [조정] -> [활기]
    - 순색이 되도록 채도를 조절하는 기능
2. 색조/채도(Hue/Saturation) : [이미지] -> [조정] -> [색조/채도]
    - 색상, 채도, 명도를 조절
    - Master에서 색상만 변경하거나 Colorize를 체크하여 전경색을 적용할 수 있음
3. 색상 균형 : [이미지] -> [조정] -> [색상 균형]
    - C M Y 로 색상을 조절
    - 광도유지(Preserve Luminosity)로 발광 유지하며 색상만 변경 가능
4. 포토 필터 : [이미지] -> [조정] -> [포토 필터]
    - 스노우 같은 필터기능 제공
5. 색상 검색 : [이미지] -> [조정] -> [색상 검색]
    - 전문 옵션 메뉴 다른 시스템의 요소를 최적화 
6. 포스터화 : [이미지] -> [조정] -> [포스터 화]
    - 레벨 값으로 이미지 색상 수 가 조절되며 단순/복잡 하게 해줌
7. 그레이디언트맵 : [이미지] -> [조정] -> [그레이디언트맵]
    - 그레이디언트를 이미지 명암에 따라 적용
8. 선택 색상 : [이미지] -> [조정] -> [선택 색상]
    - 선택한 색을 CMYK색상으로 **보정**
9. 색상 일치 : [이미지] -> [조정] -> [색상 일치]
    - 기준이 되는 소스 이미지를 불러와 유사한 색상과 채도 자동조절 할때 사용
    - 기준이 되는 소스 파일은 반드시 열려 있어야 하며 조절된 옵션은 '이미지옵션'에서 조절 가능
10. 색상 대체 : [이미지] -> [조정] -> [색상 대체]
    - 스포이드로 이미지의 특정 부분을 클릭하여 색상을 추출하고 '허용량'을 조절하여 '결과값'으로 지정된 색상영역으로 변경


## 흑백 조절을 위한 메뉴(채도0) -꼭시험
1. 색조/채도(Hue/Saturation) : [이미지] -> [조정] -> [색조/채도]
    - 채도를 -100으로 조정하면 이미지가 흑백으로 바뀜
2. 흑/백 : [이미지] -> [조정] -> [흑/백]
    - 색상 별 옵션을 이용하여 흑백 정도 조절
    - 틴트를 적용하면 흑백 이미지에 틴트가 적용되면서  듀오톤 이미지가 만들어짐
3. 한계점(Threshold) : [이미지] -> [조정] -> [한계점]
    - RGB를 검은색과 흰색으로만 구분하여, 한계점 값에따라 수치조절
4. 활기 : [이미지] -> [조정] -> [활기]
    - 채도를 최저로 낮추기


## 실습
* 이미지 듀오 톤으로 변경(6주차 2-1)
    1. [이미지] -> [모드] -> [회색음영]
    2. [이미지] -> [모드] -> [이중톤]

* 이미지를 인덱스 모드로 변경하기(6주차 2-2)
    1. [이미지] -> [모드] -> [인덱스색상]

* **레벨 조정 레이어로 밝기 보정(6주차 2-7)**
    - [레이어창 하단메뉴] -> [레벨]
    - [속성창] -> [조정] -> [레벨 아이콘]
    2. 레벨값 조정

* **부분적으로 밝기 보정하기(6주차 2-8)**
    1. 레이어 복사
    2. [빠른 객체 선택도구]
    3. [이미지] -> [레벨]

    1. [이미지] -> [레벨] -> 포커스 객체에 맞게 레벨 조정
    2. 전셩색 검정으로 칠하기
    3. [브러쉬]로 레이어 마스크 기능 이용


## 실습

1. 안개로 흐린 사진을 선명하게 보정 (6주차 2-T2)
    * [이미지] -> [명도/채도] -> 명도/대비 조정

2. 사진이 파란색으로 치우쳐 있습니다. 색을 보기좋게 보정하시오 (6주차 2-T3)
    * [색상조정] || [자동색상]

3. 하늘 부분을 맑은 파란색으로 강조하시오. & 전체적으로 색감이 강조되도록 바꾸시오 (6주차 2-T4)
    * [이미지] -> [레벨] 하늘만 레벨 보정
    * [작업내역브러쉬도구]로 하늘을 제외한 부분 롤백
    * [색조/채도]&[활기]를 통해서 분위기 조정

4. 특정 부분 색 변경 (6주차 2-T6)
    * [색상 대체] 사용
    * [shift]키로 영역 잘 추가/제거 확인하여 변경

5. 과일사진의 노란색과 빨간색 채도를 보기 좋게 변경 & 색조,채도 조정 레이어 활용
    * [레이어창 하단 조정 레이어 생성 메뉴] -> [색조, 채도]
    * [빨강계열]&[노랑계열] 채도 증가


## 레이어의 기능
* **레이어 복제 : [Ctrl] + [J]**
* 새로 만들기 : 새로운 투명 레이어 생성
* 삭제 : 선택 레이어 삭제
* PNG로 빠른 내보내기 : 현재 레이어 이미지만 PNG파일로 내보내 저장합니다.
* 내보내기 형식 : 현재 에이어 이미지만 포맷을 지정하여 내보내 저장합니다.
* 새 칠 레이어 : 단색, 그라데이션, 패턴을 정하여 칠해주는 레이어 생성 (레이어 패널 돋보기 아이콘)
* 새 조정 레이어 : 이미지의 색상, 밝기 등을 조정할 수 있는 레이어 생성 (레이어 패널 돋보기 아이콘)
* 레이어 마스크 : 두 장의 레이어를 합성 할때 사용
* 벡터 마스크 : 벡터 요소에 이미지를 합성할 때 사용 / 패스가 존재하는 상태에서 활성화
* 레이어 이름 바꾸기 : 레이어창에서 더블클릭으로도 변경가능
* 레이어 스타일 : 레이어 광원, 그림자, 테두리 효과 지정 (레이어 패널 fx 아이콘)

## 레이어 메뉴의 주요기능
* **클리핑 마스크 : 이미지를 텍스트, 도형 등으로 오리는 효과를 낼때 사용**
* 고급 개체 : 비파괴적인(이미지 손실없는) 방법으로 이미지를 편집할 수 있도록 이미지를 고급개체로 변환
* 비디오 레이어 : 동영상 파일을 레이어로 불러옵니다.
* 레스터화 : 레이어 객체들을 비트맵으로 변경
* 레이어 그룹화
* 레이어 숨기기
* 레이어 잠그기
* 레이어 연결
* 레이어 병합 : 여러 레이어를 하나로 만듬
* 아래 레이어와 병합
* 보이는 레이어 병합
* 배경 이미지로 병합

## 레이어 패널의 구성
* 레이어 연결하기
* 레이어 스타일
* 레이어 마스크
* 색칠 및 조정 레이어
* 레이어 그룹 만들기
* 새로운 레이어 만들기
* 지정된 레이어 삭제하기
* 레이어 혼합모드 : 현재레이어와 아래 레이어를 합성하는 방법을 설정
* 잠그기
* 불투명도 : 레이어 스타일에도 불투명도가 적용됨
* 칠 : 레이어 스타일은 제외하고 레이어 자체의 투명도를 조절

## 레이어 불투명도와 채우기
* Opacity : 테두리와 칠하기 불투명도
* Fill : 칠하기 불투명도

## 레이어 스타일 적용하기
* 경사와 엠보스 : 레이어 개체에 입체감 효과 적용
* 획 : 레이어 개체에 테두리 적용
* 내부 그림자 : 레이어 개체 안쪽으로 그림자 표시
* 내부 광선 : 레이어 개체 안쪽으로 빛을 적용
* 색상 오버레이 : 레이어 개체에 단색을 칠하는 효과 적용
* 그레이디언트 오버레이 : 레이어 개체에 그레이디언트 칠 효과 적용
* 패턴 오버레이 : 레이어 개체에 지정한 패턴을 칠하는 효과 적용
* 외부 광선 : 레이어 개의 바깥쪽으로 발산하는 광선 적용
* 드롭 쉐도우 : 레이어 개체에 그림자 효과를 적용

## 실습

* 레이어를 활용하여 비추는 효과 만들기 : 캔버스크기 조정
    1. 레이어 복사
    2. [이미지] -> [캔버스크기]
    3. 선택 레이어 이미지 반전및 보정해제해서 크기 조정
    4. 불투명도 조정

* 퍼펫 뒤틀리기로 개체 변경하기(6주차 3-4)
    1. 선택 도구로 손 형태 선택
    2. [Ctrl] + [J] 로 선택 레이어 만들기
    3. 기존 배경 레이어 손을 제거하고 [내용인식적용]
    4. 선택영역 크기 넓히고 손만 있는레이어로 이동
    5. [편집] -> [퍼펫뒤틀기]

*
