<h1>초보자 운전연수 프로젝트 - "교차로"</h1>


<h2>1. 기획 의도</h2>
<div dir="auto" style="display: flex;">
<img width="1180" alt="스크린샷 2022-12-27 오전 12 09 34" src="https://user-images.githubusercontent.com/122762404/233542161-4f88db30-e854-4c74-a2f4-f9b74e76979d.png" style = "width: 45%; height : 45%">
</div>


<h2>2. 기대 효과</h2>
<img width="1161" alt="스크린샷 2022-12-27 오전 12 20 31" src="https://user-images.githubusercontent.com/122762404/233542200-77ce5c96-0349-41ca-96ed-3135b044b44d.png" style = "width: 45%; height : 45%">


<h2>3. 프로젝트 사용 툴</h2>
<img width="1160" alt="스크린샷 2022-12-27 오전 12 23 33" src="https://user-images.githubusercontent.com/122762404/233542226-f4123930-0ef0-49ad-9a58-25296f83b56e.png" style = "width: 45%; height : 45%">


<h2>4. 퍼블리싱 담당 업무</h2>
<img width="1160" alt="스크린샷 2022-12-27 오전 12 23 33" src="https://user-images.githubusercontent.com/122762404/233549093-dd680d2d-1b5f-4304-a8b9-63033aabb42a.png" style = "width: 80%; height : 45%">

4-1. 관리자페이지
  - 관리자페이지 홈
  - 관리자페이지 회원
  - 관리자페이지 연수신청
  - 관리자페이지 결제
  - 관리자페이지 후기

4-2. 메인
  - 헤더(로그인 전 헤더, 로그인 후 헤더)
  - 푸터
  - 메인페이지
  
<h2>5. 백엔드 담당 업무</h2>
<img width="1160" alt="스크린샷 2022-12-27 오전 12 23 33" src="https://user-images.githubusercontent.com/122762404/233548768-1ae66af4-e59d-4949-bf05-44cca7e563b2.png" style = "width: 80%; height : 45%">

5-1. 마이페이지 - 초보자 회원
  - 마이페이지 회원정보 조회(이름, 이메일, 전화번호)
  - 마이페이지 회원정보 수정(이름, 이메일, 전화번호)
  - 마이페이지 프로필 변경, 삭제
  - 마이페이지 비밀번호 변경
  - 마이페이지 회원탈퇴
  
5-2. 마이페이지 - 베테랑 회원(모바일)
  - 마이페이지 비밀번호 변경
  - 마이페이지 회원탈퇴

5-3. 마이페이지 - 연수신청
  - 초보자 회원이 신청한 전체 횟수 조회
  - 연수신청 진행상태 조회(수락대기중, 연수 진행중, 완료한 운전연수)
  - 연수신청 상세내역 조회(날짜, 지역, 코스, 상태)

5-4. 마이페이지 - 포인트(초보자/베테랑)
  - 회원의 현재 포인트 조회
  - 회원의 포인트 상세내역(날짜, 상태, 포인트내역)
        <br>- 초보자 포인트 상태(충전/사용)
        <br>- 베테랑 포인트 상태(적립/환전)
        
5-5. 포인트 - 결제하기
  - 포인트 결제하기(부트페이 API)
  
<h2>6. 느낀점</h2>
<h3>6-1. 어려웠던 부분</h3>
📌마이페이지 member, apply, review 3개의 테이블을 join하는게 어려웠습니다.  <br>
✔ member와 apply 테이블을 먼저 join 후 .<br><br>
📌프로젝트 초반에는 entity와 DTO를 언제 어떻게 구분해서 사용해야 하는지 감이 잘 잡히지 않아서 헷갈렸다. <br>
✔ 프로젝트를 통해 학습과 적용을 반복하다보니 자연스레 언제 사용해야 하는지 알게됐다. 특히, DTO에 내가 필요한 변수를 능숙하게 선언, 사용 할 수 있게 됐다는 점이 큰 수확이었다. <br><br><br><br>


<h3>6-2. 문제를 해결했던 부분</h3>
<h4>📌WebSocket session 실종사건</h4> <br>
🌩문제 상황🌩<br>
웹소켓의 경우 해당 채팅방에 접속한 모든 참여자의 WebSocketSession을 받아와서 메세지를 보낸다. 메세지를 보내는 메소드는 자바스크립트 메소드인 onMessage()인데, 어찌된 일인지 onMessage 메소드가 실행되질 않았고, 오류문도 나오지 않았다.<br><br>
🚨문제 원인🚨 <br>
채팅이 전송될 때 거치는 모든 메소드와 컨트롤러에 전부 로그를 찍어봤는데, list에 담아둔 WebSocketSession이 중간이 실종된다는 것을 확인했다. 즉, 메세지를 받을 대상이 없었기 때문에 onMessage 메소드가 실행되지 않았던 것이다. <br><br>
🚀해결 방법🚀<br>
WebSocketSesssion을 담아뒀던 list를 static으로 선언해서 해결했다. Java에서 Static 변수는 메모리에 한번 할당되어 프로그램이 종료될 때 해제되는 변수로, 메모리에 한번 할당되므로 여러 객체가 해당 메모리를 공유하게 된다.<br><br><br>



<h4>📌채팅방 확성기 기능 사건</h4> <br>
🌩문제 상황🌩<br>
A사용자가 a채팅방에 보낸 메세지가 B사용자가 접속중인 b채팅방에도 전송되는 현상이 발생했다. 이 현상이 마치 게임 메이플스토리의 캐시템 중 하나인 확성기 같았기에 채팅방 확성기 기능 사건이라 명명했다.<br><br>
🚨문제 원인🚨 <br>
위에서 접속자들의 WebSocketSession을 static list에 담았다고 적은 바 있다. 다른 채팅방에 접속 중인 사용자의 세션 또한 동일한 list에 담겨있었기 때문에 메세지를 받게된 것이다. 그렇다고 static을 지우자니 다시 메세지 전송이 되질 않았다. <br><br>
🚀해결 방법🚀<br>
메세지를 전송하는 메소드에서 발신자의 채팅방과 수신자의 채팅방이 일치하는 세션들에만 메세지를 전송하도록 만들었다. 이를 위해 우선 채팅방을 클릭했을 때 이동하는 컨트롤러에서 HttpSession에 채팅방 아이디를 추가하도록 만들었다. 즉, 채팅방을 클릭할때마다 HttpSession에 저장된 채팅방 정보가 바뀌는 것이다.<br>다음으로, WebSocketConfig 파일에 .addInterceptors(new HttpSessionHandshakeInterceptor()) 를 추가했다. 이를 통해 HttpSession에 저장돼있던 값들을 WebSocketSession에도 저장할 수 있게했다. 이 두가지 작업을 통해 현재 사용자 어떤 채팅방에 접속한 것인지 확인할 수 있었고, 확성기 오류 또한 해결할 수 있었다.<br><br><br>



<h4>📌메세지가 여러번 출력되는 오류</h4> <br>
🌩문제 상황🌩<br>
A 사용자가 a채팅방 입장 → b채팅방 입장 → 다시 a채팅방 입장 이런식으로 동일한 채팅방에 여러번 입장, 퇴장을 반복할 경우 해당 사용자가 보내는 메세지가 화면에 여러번 출력됐다.<br><br>
🚨문제 원인🚨 <br>
위에서 접속자들의 WebSocketSession을 static list에 담았다고 적은 바 있다. 동일한 유저가 동일한 채팅방에 여러번 입장했더라도 해당 유저의 WebSocketSession은 list에 하나만 담겨있어야 한다. 그러나 입장을 할 때 마다 해당 유저의 WebSocketSession이 list에 추가되면서 메세지가 입장한 횟수만큼 전송된 것이다. <br><br>
🚀해결 방법🚀<br>
WebSocketSession을 list에 담지 않고, map의 value 값으로 담았다. map의 key 값은 HttpSession에서 가져온 유저의 아이디로 설정했다(중복 방지). 이를 통해 채팅방에 입장할 때 해당 유저의 아이디가 map에 key값으로 존재한다면 그 key의 value 값을 갱신하고, 존재하지 않는다면 key값과 value 값을 map에 추가하는 방식으로 구성했다. 따라서 동일한 유저의 webSocketSession이 여러번 저장되지 않았고, 중복 출력 또한 해결됐다.




<h3>5-4. 총평</h3>
<h4>🌟 두려워하지 말자. 나는 내 생각보다 집요한 사람이다. </h4>



웹소켓이라는 기술은 국비 교육 중 배우지 않고 독학해서 프로젝트에 적용한 기술이다. 당연히 주변에 물어볼 수 있는 사람도 없었다. 로직을 이해하는 것도, 오류를 해결하는 것도 너무 막막해서 초반에는 많이 괴로웠다. 특히 채팅 전송이 정상적으로 되지 않을 때 오류문이 나오지 않아서 더 힘들었다. 그러나 결국 나는 해내고야 말았다. 메세지가 거치는 모든 메소드에 값이 들어왔는지 로그를 전부 찍어서 문제의 원인을 발견하고 해결했다. 이 과정에서 나도 나 자신의 집요함과 끈기에 놀랐다. 지금까지 항상 스스로의 한계를 정해두고 새로운 도전을 꺼렸었는데, 이 프로젝트를 계기로 한발짝 도약한 것 같아 행복했다. 



<h4>🌟 내가 마주한 오류와 해결방안을 구체적으로 기록해두자. </h4>



정말 많은 오류를 경험하고 해결했는데, 기록을 해두지 않아서 많이 잊어버린 점이 프로젝트가 끝난 이후 아쉬웠다. 간단하게라도 블로그에 기록하면서 기상천외한 오류를 겪을 동료 개발자들에게 한 줌의 도움이라도 주고싶다. 



<h4>🌟 어떻게 더 친근한 동료, 친근한 리더가 될 것인가. </h4>



해당 프로젝트를 진행하면서, 프론트엔드 작업을 진행할 때 우리 팀의 팀장이 국비 교육에서 중도탈락했다. 나는 얼떨결에 부팀장에서 팀장이 됐고, 프로젝트 기간 동안 리더의 역할을 수행했다. 약 한달간 팀장으로서의 역할을 수행하면서 중간 관리자의 고충을 약간이나마 알게 된 것 같다. 특히, 커뮤니케이션에 미숙한 팀원을 어떻게 이끌어야 할까? 라는 질문에 대해 고민하게 됐다. 몇 주간의 고민 끝에 나온 나의 답은 '더 친해지자!'였다. 친하지 않으면 같은 말도 서로 더 날서게 받아들이기 쉽다. 따라서 팀원의 업무 태도를 지적하고, 해결하려는 자세에 앞서서 그 사람의 마음을 얻는 것이 더 먼저라는 생각이 들었다. 앞으로 리더가 될 때까지는 많은 시간이 남았지만, 항상 이 경험을 되새기면서 팀원들에게 먼저 다가갈 수 있는 우호적인 사람이 돼야겠다.    


<h2>ERD</h2>
<img width="100%" alt="erd" src="https://user-images.githubusercontent.com/109493547/209980568-1cf4273c-fc51-4615-8703-e11562ba5892.png">

