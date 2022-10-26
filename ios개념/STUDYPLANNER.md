# STUDYPLANNER

> 모바일 플랫폼 기술학습

- 4-5월: 개인학습, 내용공유
  - 헬로월드 코드랩 따라해보고 책 구매
  - do it swift 책 따라서 학습
  - 5월 안에 박스오피스 앱 만들어보기
- 6월: 공통프로젝트
- 7-11월: 개인프로젝트





## 어떤 앱을 만들까

- **박스오피스앱: 메인화면에서 일일 순위, 항목 선택시 상세화면**
  - [영화진흥위원회 오픈API (kobis.or.kr)](https://www.kobis.or.kr/kobisopenapi/homepg/apiservice/searchServiceInfo.do)
  - 주요기능: Http통신, 이미지/텍스트 리스트뷰, 스크롤/공유
  - **http통신, json 파서, 이미지뷰**, 스크롤뷰 최신 라이브러리 찾아보기
- (미정) 디바이스 기능 사용: 촬영, UID, 위치, 신체정보, 블루투스 등
- (미정) 커스텀뷰: 뷰를 자유롭게 그리기, 정밀하게 제어하기 등
- (미정) 성능관리: 대용량 파일송수신, 백그라운드 작업 등




## 어떤 플랫폼/언어로 만들까

- flutter로 모든 기능을 만들 수 있는 것은 아니기에, 기본이 되는 swift를 먼저 학습하고 flutter로 변환하는 것이 순서에 맞겠다.
- **플랫폼: ios를 위주로**
  - ios/android/webApp
  - 유려한 UI와 특별한 보안/권한정책을 사용해보고 싶다.
  - 시간이 남는다면 android/kotlin/jetpack도
- **언어: swift로 개발하고, dart/flutter로 전환할 부분 확인**
  - Swift, Xamarin, React Native, Flutter
  - [(2019-08-26)Flutter, 왜 선택하지 못했나 - LINE ENGINEERING (linecorp.com)](https://engineering.linecorp.com/ko/blog/flutter-pros-and-cons/)
    - 카메라 등 플러그인이 필요한데, 플러터 플러그인이 충분히 성숙하지 못한 상태였다.
    - 플러터로 구현하기 어려운 UI가 있는데, UI 기획이 결정되기 전에 플러터로 무엇을 만들 수 있는지 먼저 알았다면 더 좋았을 것이다.
  - [(2021-11-19/경험자체는2019년의 일)지식iN 앱을 Flutter로 개발하는 이유 (d2.naver.com)](https://d2.naver.com/helloworld/3384599)
    - 크로스플랫폼, 선언형UI 방식으로 성능과 생산성이 예상보다 뛰어나다.
    - 선언형UI는 적응이 필요하고, 플러터가 제공하는 라이브러리(카메라/지도/동영상 등) 안정성이 아직 많이 떨어진다.
    - hot reload로 UI 작업시 빠르게 결과물을 확인하며 작업할 수 있다.

  


## 개발/테스트환경

- **개인맥북, xcode, ios 시뮬레이터**
  - 아이폰 당근마켓에서 구하는중
- **ios에서 디바이스 테스트하기, 개발자 계정 만들면 바로 가능**
  - [iOS 디바이스 테스트 - RN(react native)로 개발한 프로젝트를 iOS 디바이스에서 테스트해 봅시다. (posstree.com)](https://dev-yakuza.posstree.com/ko/react-native/ios-test-on-device/)
    - 디바이스 테스트는 개발자 등록 안해도됨, 계정만 있어도됨
  - [iOS TestFlight - iOS의 TestFlight를 이용하여 개발한 어플을 테스터를 통해 테스트해 보자. (posstree.com)](https://dev-yakuza.posstree.com/ko/react-native/ios-testflight/)
    - 앱 테스트 배포는 개발자 등록 해야 함
  - [[Xcode] iOS 시뮬레이터(iOS Simulator) 실행 방법 | 디바이스 변경 방법 (tistory.com)](https://envia.tistory.com/161)
    - 지원 되는 기능: 회전, 멀티터치, 흔들기, GPS(수동입력)
    - 지원 안 되는 기능: 전화착신시 동작, 카메라, 가속도, GPS(실제)
- 애플 개발자 프로그램 옵션 - [[멤버십 선택하기 - 지원 - Apple Developer]](https://developer.apple.com/kr/support/compare-memberships/)

  


## 학습교재/커리큘럼

- **코드랩**
  - swift 
    - swift [Swift - Apple Developer](https://developer.apple.com/kr/swift/)
    - swiftUI [SwiftUI Tutorials | Apple Developer Documentation](https://developer.apple.com/tutorials/swiftui)
  - flutter [NAVER Tech Talk: Flutter meetup](https://d2.naver.com/news/9527890)
- **책**
  - swift [(2022-03)Do it! 스위프트로 아이폰 앱 만들기 입문 - 개정 6판](https://www.aladin.co.kr/m/mproduct.aspx?ItemId=289731712), 전자책 18000STUDYPLANNER.md
