# __2d 게임 만들기__

## 1. 플래피 버드(FLAPPY BIRD) && 의지의 히어로(WILL HERO)
![Flappy Bird](https://user-images.githubusercontent.com/68374446/94271138-2a5d3300-ff7c-11ea-848a-2d61f551a930.jpg)

![99C44F3E5B46F6E008](https://user-images.githubusercontent.com/68374446/95655352-a1302980-0b41-11eb-8523-4df116e8ac47.jpg)


  2014년에 스마트폰 초기 당시 히트를 친 간단한 모바일 게임(플래피 버드)
  2018년에 히트를 친 모바일 게임 의지의 히어로를 섞어 개발할 예정

  게임의 방식은 키조작(상하좌우)를 통해 떨어지는 물고기를 관 사이로 통과시키는 것이다.
  더블클릭을 할시 의지의 히어로 케릭터처럼 원하는 방향으로 대쉬를 한다.
  그리고 스페이스 바를 통해 부메랑을 투척 그리고 스페이스바를 다시 누를시 부메랑과 케릭터의 위치를 변경할 예정
  이를 통한 간단한 보스전 (간단한 패턴을 가진)을 부메랑을 통해 처치할 수 있게 만들 예정
  최대한 관에 부딪치지 말고 고득점을 하는 것이 게임의 목적이다.

## 1. GameState (Scene) 의 수 및 각각의 이름

  일단 Game 시작 화면, 인게임 state, 게임 오버 state 3개를 계획중
  추후 flappy bird를 기반으로 다른 scene을 추가 예정
  
  - 게임 오버 state를 따로 만들 필요를 못 느껴 인게임 state에 포함시켜 2개의 state로 구성함
  
## 2. 각 GameState 별 다음 항목

### - 첫 시작화면 GameState
    아무 키나 눌렀을 때 게임이 시작하도록 설계할 예정 
    화면의 fish 객체가 뛰어다니도록 설계할 예정
    클릭 혹은 키보드 입력시 인게임으로 이동할 예정
    
    -아무키가 아닌 spacebar 를 누르면 시작하도록 설정
    -화면에 bird객체가 움직이며 화면이 자연스럽게 스크롤 되도록 설정    구현률 100
    
![title_screen_shoot](https://user-images.githubusercontent.com/68374446/101348193-9938ff80-38ce-11eb-845e-52102294e1f2.PNG)
    
   타이틀 화면
    
    

### - 인게임 GameState
    
    조작 -
      w,a,s,d = 상하좌우 이동(상은 플러피 버드의 점프형태, 하는 중력값을 1.5배로 조정)
      스페이스바 = 마우스가 있는 곳을 향해 부메랑 투척(if 부메랑이 화면에 하나 있다면 부메랑과 위치 변경) 데미지 수치 10
      마우스 왼쪽 클릭 = 부메랑이 잠깐 더욱 빠르게 회전하여 탄막을 랜덤한 방향으로 튕김 (탄이 날아가던 방향에 90~270도 사이)
      튕겨진 탄환은 색이 변하며 보스의 히트박스에 적중할시 데미지 수치 10
      
      -최종 변경된 부분
      -w,a,s,d 상하좌우로 조작을 하며 기본 게임상태에서도 점프를 하지 않도록 변경(기존 Flappy Bird가 어려워서)
      -boss 출현시 움직임은 똑같으나 물고기가 마우스를 따라 고개를 돌리도록 설정
      -마우스 클릭시 공격을 위한 파이프 관 생성 마우스를 떼면 파이프관 끝으로 순간이동
      -마우스를 클릭 중 스페이스바를 누르면 등껍질 발사 데미지 5 비용은 score -1     구현률 100프로
    
    게임 구성 -
      물고기 객체와 파이프 객체들을 생성 O(구현)
      물고기를 따라 화면이 움직임 O(구현)
      보스가 생성될 시 화면 고정 O(구현)
      화면이 스크롤 되면서 파이프의 위치가 랜덤으로 상하 높이 조절 될 것 O(구현)      구현률 100프로
      
      -추가된 부분
      -파이프 관에서 랜덤한 등껍질이 나옴(초록색, 빨간색)
      -플레이어의 체력 우측 상단 비주얼 표시 및 보스 체력 상단 표시
      -플레이어의 체력이 감소될 시 플레이어가 반투명해지며 잠깐 무적
      
    
    게임 시스템 -
      파이프의 갯수가 20개를 넘었을 시에 보스전으로 돌입되게 할 것 -score 득점의 기준을 파이프 통과가 아닌 빨간색 등껍질 객체를 먹을시로 수정. 10개로 수정
      2가지의 보스중 랜덤으로 생성  - 1가지의 보스만 구현
      보스 1 - 주로 탄알 공격을 하며 기를 모아 튕겨낼 수 없는 거대한 탄을 던지는 공격을 가짐 (체력 200)
      보스 2 - 파장을 퍼뜨려 순간이동으로만 피해야 하는 공격을 날림 (체력 200)
      Escape키를 누를시 게임이 일시 정지 되도록 만들 것
      그리고 떨어지거나 파이프에 부딪히면 게임오버 State로 이동          구현률 80프로
      
      -변화된 점
      -score 득점의 기준을 파이프 통과가 아닌 빨간색 등껍질 객체를 먹을시로 수정. 10개로 수정
      -보스를 한마리만 만들고 패턴을 단일화. 캐릭터를 바라보며 등껍질을 쏘고, 
       체력이 절반 이하로 떨어질 시 움직이며 캐릭터를 향해 공격(체력 100)
       
      -Escape키를 누를 시 게임 종료, GameOver상태에서 enter키를 누를시 게임을 재시작
      -체력 모두 소진 혹은 score가 0이 되면 GameOver 즉 score = 탄환의 갯수
      -보스전에서 score가 모두 소진되지 않게 탄환을 쏘고 순간이동을 통해 자신이 쏜 탄환에 부딪쳐 점수를 
       다시 획득해야됨(자신이 쏜 탄환은 부딪쳐도 사라지지 않음)
      


![boss_screen_shot](https://user-images.githubusercontent.com/68374446/101348259-b2da4700-38ce-11eb-80c3-59a5185f241b.PNG)
      
      게임의 보스전과 플레이어가 공격하는 모습
      
      
### - 게임 오버 GameState
    기존 화면이 블러처리 되면서 게임오버 글자를 띄울 것
    Escape키를 누를시 첫 시작화면 GameState로 이동
    마우스 클릭 혹은 space bar 입력시 게임 다시 시작
    
    -변화된 점
    -게임 오버 state를 인게임 state에 통합
    -GameOver 후 자신의 기록을 저장, 랭킹이 보이게 설정 
    -GameOver 후 엔터를 누르면 다시 게임이 시작하게 만듬              구현률 100프로
    

## 3. 필요한 기술

  내가 지정한 객체가 움직일 때 그 객체가 중심이 되어 화면(스크롤)이
  자연스럽게 움직이는 기술 O(구현)
  
  나를 따라서 스크롤이 움직이는 기술 O(구현)
  
## 4.개발 일정

  1주차 - 필요한 디자인 자료 수집 및 게임 시스템 구성

  2주차 - 게임 시스템 구성

  3주차 - 게임 이미지 적용 및 플레피 버드 케릭터의 물리 구현

  4주차 - 보스의 움직임을 구현 및 보스의 패턴 공격 기획

  5주차 - 보스의 패턴 구현 및 부메랑 구현

  6주차 - 보스의 패턴을 다양화 및 가능하다면 또다른 보스 구현

  7주차 - 디버깅을 통한 최적화 및 버그 수정 혹은 하다가 더욱 추가하고 싶은 요소 추가

  8주차 - 더욱 추가하고 싶은 요소 추가 및 마무리
  
  기존 일정
  
  
![commit](https://user-images.githubusercontent.com/68374446/101347270-2a0edb80-38cd-11eb-91e9-979d6afd9f57.PNG)
  
  변경된 커밋 일정
  
  
  
  
  1차발표 링크 - https://www.youtube.com/watch?v=B6PeV2sMLm8&feature=youtu.be
  
  2차발표 링크 - https://youtu.be/rEzOJciKe3g
  
  3차발표 링크 -
