# CS496 Week3 Report

개발자: 우혜인(@woohyein), 조재구(@Jaegoomon)

## Abstraction

"하마하마"는 공동구매를 위한 웹사이트 애플리케이션으로 공동구매를 위한 전용 채팅방을 만들 수 있는 기능을 제공한다. 이번 프로젝트 동안 구현한 기능은 다음과 같이 요약할 수 있다.

1. 로그인 기능/ 회원가입 기능

로그인의 경우는 서버에 있는 데이터 베이스 정보와 단순 비교를 통해서 메인 페이지로의 이동을 허용/ 제한 할 수 있다. 회원가입의 경우는 아이디, 비밀번호 그리고 비밀번호 재확인 항목을 통해서 완료할 경우 데이터 베이스에 새로운 로그인 정보가 저장된다.

2. 채팅방 생성

`+` 표시 버튼을 누르게되면 채팅 방에 필요한 정보를 입력한 후에 관련 데이터를 DB에 저장하게 된다. 이때 만든 인원은 채팅방의 주인이 되며, 이후 채팅방의 삭제 권한을 가지게 된다. 새로 만든 채팅방은 화면 가장 상단에 띄워진다.

3. 실시간 채팅 및 채팅 데이터 백업

채팅방을 만들게 되면 채팅방 안에서 소켓통신을 이용해서 채팅을 한다. 채팅 기능은 실시간으로 실행되며, 채팅방을 나갔다 들어올 때, DB에 저장된 채팅 데이터가 자동으로 백업되어 이전에 기록했던 채팅방 내용을 볼 수 있다.

4. 채팅방 내의 공유 메모장

채팅방의 사이드바에서 지원하는 기능으로 채팅을 통해서 정해진 내용이나 주요 정보를 채팅방 좌측 사이드 바의 메모장을 이용해서 기록할 수 있다. 마찬가지로 기록된 메모는 DB에 자동으로 저장되며 구성원 모두가 볼 수 있다. 단, 새로 고침을 통해서 갱신이 된다는 단점이 있다.

5. 채팅방 바로가기 기능

메인 화면의 우측 상단에 있는 '내 채팅방' 버튼을 누르면 현재 로그인되어 있는 사용자가 들어가 있는 채팅방의 목록을 볼 수 있다. 목록 중 하나를 선택하면 해당 채팅방으로 바로 이동할 수 있다.

6. 채팅방 카테고리 필터링 기능

채팅방 목록에 떠 있는 카테고리를 누르면, 해당 카테고리가 포함된 채팅방들만 필터링되어 나타난다. 두 개 이상의 카테고리를 선택한다면 각 태그들이 모두 포함되어 있는 교집합의 채팅방 목록만 노출된다.

## Demo

* 로그인

![](https://raw.githubusercontent.com/madcamp2020-proj3/Syno_front/master/demo/login.gif)

회원가입 버튼을 클릭하게되면 모달창이 열리고 기본 데이터를 입력하면 회원가입이 종료된다. 회원가입의 경우는 단순히 비밀번호와 비밀번호 재확인으로 이뤄진다. 회원가입이 완료되면 관련된 정보가 DB로 저장된다.

* 방만들기

![](https://raw.githubusercontent.com/madcamp2020-proj3/Syno_front/master/demo/make.gif)

방 정보의 경우도 마찬가지로 모달창이 열리고 관련된 데이터를 적는 것으로 완료된다. 사진 업로드와 미리보기가 가능하며 달력을 통해서 채팅방의 지속시간을 설정할 수 있다. 만약 시작 날짜가 현재 날짜와 같다면, 채팅방 정보에 'NOW' 표지가 활성화되어 현재 모집하고 있는 채팅방임을 알려준다.

* 채팅

![](https://raw.githubusercontent.com/madcamp2020-proj3/Syno_front/master/demo/chat.gif)

실시간 채팅의 경우는 채팅방에 들어갈 경우 채팅 백업 데이터를 불러와 화면에 그려준다. 이후 소켓 통신을 통해서 양방향으로 전달이 가능하다. 

* 바로가기

![](https://raw.githubusercontent.com/madcamp2020-proj3/Syno_front/master/demo/goto.gif)

바로가기 기능은 메인 화면에서 자신이 참여한 정보를 확인할 수 있으며, 회색빛으로 칠해진 부분이 자신이 속한 대화방 중에 자신이 방장으로 있는 채팅방이다. 클릭을 하며 해당 채팅방으로 이동이 된다.

## Functions

프로젝트를 진행하면서 사용했던 두 언어를 바탕으로 서술하였다.

### React.js 

![](https://reactjs.org/logo-og.png)

이번 프론트 엔드의 경우 react.js를 이용하였다. 반응형 웹과 컴포넌트 단위로 화면 구성을 할 수 있다는 특징으로 잘 알려진 react의 기능을 사용하면서 느꼈던 장점과 단점은 다음과 같이 정리해 보았다.

* 장점
  * 다양한 패키지로 지원해주는 감각적인 디자인: 리액트를 사용하면서 가장 좋았던 부분 중 하나는 바로 리액트에서 패키지로 지원해주는 다양한 기능의 구성요소(Button, Modal, ...) 들을 [친절한 참고자료](https://react-bootstrap.github.io/)와 함께 쉽게 사용할 수 있다는 것이다.
  * Hook의 다양한 기능: 이전 프로젝트에서 안드로이드를 개발하면서 느꼈던 난해했던 점이 바로 데이터가 변하였을 때, 이를 인지하고 화면을 업데이트 해야 했던 것이다. 하지만 리액트의 가장 기본이 되는 개념인 `state`, `props`가 변화 하였을 때, 렌더링이 된다는 것을 Hook과 활용하면 특별한 함수 없이 화면을 업데이트 시켜줄 수 있었다. 
  * 최근 많은 사용자들이 사용하고 있는 만큼, 유튜브나 구글을 통해 다양한 reference를 참고할 수 있었다. 특히 npm의 풍부한 라이브러리와 [tailwind cheat sheet](https://nerdcave.com/tailwind-cheat-sheet)를 통해 많은 정보를 빠르게 얻을 수 있었다.
  * 반응형 웹이라는 점에서 화면 크기에 따른 구성을 변경할 수 있다는 점이 인상 깊었는데,  PC용 웹사이트를 만들면서도 동시에 모바일 웹을 구성할 수 있다는 것이 큰 장점으로 다가왔다.
* 단점(힘들었던 점)
  * 서버 통신과 비동기 : 서버 부분에서도 다룰 내용이긴 하지만, 항상 많은 생각과 시간을 쏟는 부분이 바로 이 비동기 처리 부분이다. 이전 Week2 보다는 `Promise`와 `aync/await`의 개념이 익숙해 져서 간단한 비동기 처리는 쉽게 해결하였지만 서버와 통신을 통해 데이터를 받아오고 이 데이터를 바탕으로 렌더링을 해야하는 상황에서 직면하는 비동기 문제가 가장 많은 시간을 쏟은 부분이다. 
  * Hook과 Life-cycle의 난해함: Hook과 Life-cycle은 분명 매우 좋은 기능이며 웹, 앱을 제작하는데 있어 이런 수명과 같은 부분은 화면을 나타내는 가장 기본적인 요소이다. 하지만, 1주일이란 짧은 기간동안 이러한 개념을 모두 숙지하고, 실제 앱에 적용하기란 매우 난해한 부분이 많았다. 의도하지 않은 렌더링이 실시된다 거나, 실시되지 않는 등의 통제하지 못하는 다양한 케이스가 발생하였다. 가장 핵심이 되는 기능이지만 실제로 이를 완전히 이해하고 적용하기란 더 많은 시간의 공부량이 필요하다는 생각을 하였다.
  * javascript, css, html을 분리하지 않고 한꺼번에 작업하다 보니, 해당 언어로 기술되어 있는 reference를 참고할 때 어려움을 느꼈다. 더군다나 웹에 대한 지식이 전무한 상태에서 프로젝트를 시작했기 때문에 각각의 문법이나 작동방식에 대해 익혀가는 과정에 많은 시간을 소요했던 것 같다. 

#### Node.js

![](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Node.js_logo.svg/1200px-Node.js_logo.svg.png)

2주차에 이어서 사용한 Node.js와 MongoDB를 통해 이번 프로젝트의 백엔드를 구성하였다. 채팅 웹 애플리케이션을 만들면서 가장 느꼈던 이슈들을 중심으로 서술하도록 하겠다. 

* 비동기 처리: 비동기 처리는 리액트 부분에서 설명하였듯이, 이번 프로젝트에서 가장 중점이 되었던 이슈이다. 특히 MongoDB와 연결을 하고 데이터를 받아와 추가 데이터를 처리하는 동안 비동기 처리를 못하여 연결이 끊어지는 등의 에러가 발생하였다. `Promise`를 활용하여 연속적으로 `then()`을 사용함으로써 발생했던 문제의 대부분을 해결하였다. 하지만 이 과정에서 코드 길이가 길어지면 읽기가 어려워 지는 등의 문제가 발생하였다. `async/await`을 통해서 동기적인 방향으로 코드를 작성하는 방법이 필요하다는 생각을 하였다.
* 파일정리: 서버의 코드가 길어짐에 따라 다양한 종류의 서버사이드를 만들게 되었는데 이 과정에서 코드 수정하거나 찾는 과정에서 힘든점이 있었다. 서버사이드를 만들면서 느꼈던 부분은 서로 매우 비슷한 특징의 서버 사이드를 묶어서 `import` 방식으로 이를 이용한다면 한층 보기 편한 코드가 되지 않을까하는 생각이 들었다.
* CORS 에러(SOP): 프로젝트를 처음 시작하는 첫날 많은 어려움을 주었던 부분이었다. 실제로 해결책은 그리 어렵지 않았지만, CORS와 관련된 내용을 받아들이는데 시간이 걸렸다. 요약을 하자면 결국 웹 브라우저에서 출저(origin)이 불명확한 출저와의 통신을 차단한다는 것이다. 개발하는 입장에서 이러한 문제는 애초에 시작부터 서버와 클라이언트를 연결하는 첫단추를 빗나가게 하는데 거하게 일조하였다. Node에서는 `npm cors` 패키지를 이용해서 이와 관련된 header를 풀어주는 방법이 있지만, 이는 모든 header를 허용함으로써 보안상 매우 취약한 부분을 만든다 하여 선택적으로 허용하는 방법을 알아보았지만, 결국 전자의 방법을 채택하였다.
* 동시성 처리: 이 부분을 직접적으로 처리하지는 않았지만 20년 가을학기에 들었던 동시성 프로그래밍에서 배운 내용들이 문득 생각나서 작성을 하게 되었다. 채팅과 관련된 서버사이드를 코딩하면서 문득 들었던 생각을 10명 혹은 그 이상의 사람들이 동시에 채팅을 보낸다면 서버는 이를 어떻게 반을 할까였다. 실제로 이러한 개면을 처리할 만큼의 실력과 지식이 없는 나로서는 단순히 가정과 추측을 해보는데 그쳤지만 이과정에서 수업에서 배운 commit point와 lock등과 관련된 지식이 이러한 분야에서 사용할 수 있다는 생각이 들었다.

## Discussion

#### 로컬스토리지와 DB의 조화

채팅앱의 가장 기본적인 과정을 다음과 같이 요약할 수 있다.

1. 채팅방에 들어간다: 백업된 채팅 DB를 로드하여 화면에 그려준다(로컬 스토리지에도 저장된다).
2. 채팅을 치게된다: 채팅 내용을 로컬과 DB에 모두 저장을 하며 소켓 통신을 이용하여 다른 사용자의 화면에 그려준다. 소켓 통신을 할 수 없는 화면에 있는 경우는 DB에 저장된 데이터를 이후 채팅방 참여와 동시에 백업된 데이터를 불러와 화면에 표시한다.

간단하게 2 단계로 표현을 해보았고 이 과정에서 로컬 저장소와 DB 저장소를 모두 이용하고 있다. 다른 앱의 채팅 시스템이 실제로 어떤 시스템에서 실행되는지는 알 수 없지만 로컬 저장소와 메인 저장소(DB)와의 적절한 분배가 필요하 것이라는 생각이 이번 프로젝트를 진행하면서 느끼게 되었다. 이번에 작성한 코드의 경우는 로컬에 방에 입장과 동시에 DB의 모든 데이터를 로드하지만 이는 실제로 배우 비효율 적인 방식으로 보인다. 실제로 몇년동안 기록된 데이터를 입장할 때 마다 로드하게된다면 성능면에서 매우 느려지는 결과를 가져올 것이다. 지금의 우리가 사용하는 채팅앱의 경우는 적당한 캐싱을 이용해 좋은 성능을 유지한 채팅앱을 구현해 내고 있다는 생각이 들었다.

#### 앱?, 웹?

이번 프로젝트에서 처음 리액트를 접하면서 동시에 웹과 앱을 디자인 한다는 것이 어떤 개념인지를 접하게 되었다. 단순히 css코드를 이용해서 화면이 줄어드는 포인트에 대한 css를 따로 설정하는 과정이었지만 이를 통해서 웹을 통해서 앱에서도 가시성있는 화면을 만든다는 것이 어떤 의미인지 알 수 있었다. 기능적인 측면(센서 및 thread 사용 등)에서는 과연 리액트가 어느정도까지 안드로이드 언어(java, kotlin)를 대체할 수 있는지 알 수 없지만 디자인이나 화면 구성에서의 만큼에서는 앱과 화면 모두 사용자에게 훌륭한 UI를 제공할 수 있을 것이라는 생각을 하게 되었다.

#### 더 구현하고 싶었던 것들

공동구매를 위한 서비스라는 측면에서 기능적인 아쉬움이 남았다. 크게 개인 정보 보안이나 치안 강화의 측면에서 구현하고 싶었던 서비스, 그리고 공동구매라는 측면에서의 서비스 두 가지로 나눌 수 있다. 전자의 경우에는 1) 성별 필터링 2) 송금 시스템 구축 등이 있고, 후자의 경우에는 1) 지역을 기반으로 한 주변 편의점 알리미 등 공동구매 상품을 수령할 수 있는 정보를 알려주는 기능 2) 메인 화면에서 제목/소제목별 검색 기능 3) 지역별 필터링 기능 4) 모바일 버전 UI 관리 및 모바일에서 방 생성 시 이미지 업로드 기능 등이 있다. 기회가 된다면 리액트와 웹, DB에 대해 깊이 공부해서 이런 기능들을 구현하고 싶다.  

## Reference
