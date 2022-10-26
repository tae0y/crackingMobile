# And&iOS 뷰 생명주기 비교 [작성 중]

- **Android**
  - Activity : 화면에서 사라져도 메모리가 부족해질 때까진 유지됨
    - `onPause` : 상호작용이 불가능한 상태 (팝업창 등), 충분한 작업시간을 보장하지 않음
    - `onStop` : 화면에 표시되지 않고 실행이 중단된 후
    - `onDestroy` : 메모리 해제되기 직전에
  - Fragment : 화면에서 사라지면 메모리에서 해제됨
- **iOS**
  - 여러 개의 뷰 컨틀롤러가 있다
  - viewController : 메모리 해제될 때 `deinit`이 호출되지만, OS 레벨에서 메모리를 자유롭게 제어하기 위해 개발자가 해당 메서드를 직접 호출하지는 않는다. 대신 `viewDidDisappear` 메서드에서 뷰가 화면에서 사라질 때 필요한 작업을 수행한다.
    - `viewDidDisappear` : 뷰가 화면에서 사라질 때
    - `deinit` : 메모리에서 해제될 때
  - navigationViewController
  - tabBarController
  - tableViewController