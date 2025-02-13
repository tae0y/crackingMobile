# doit! ios swift - 기본개념

총 19장까지 있고, 5월까지 12장까지 공부하는 것이 목표. 다른 내용은 필요할 때마다 학습. 여기에는 책 읽으면서 기본적인 내용들 요약/정리.

- **이 책의 내용은**
  - **[V] storyboard**는 XML뷰/컨트롤러 방식
    - 코드양이 많고 협업하고 유지보수하기 까다롭다
    - ios13 이전 버전에서도 동작, 개발가능
    - 레퍼런스가 풍부함
  - **swiftUI**는 선언형 UI프레임워크
    - ios13 이후 버전에서 동작, 개발가능
    - 코드를 작성하는 동시에 디자인 인터페이스가 생성
    - 디자인 요소가 코드로 생성

​    

## 1, 2장

- **#? 앱의 구조**
  - [ ] 앱의 생명주기 app delegate
  - [ ] 사용자 인터페이스의 생명주기 scene delegate
  - [x] 뷰와 뷰 컨트롤러 viewcontroller
  - [ ] 스토리보드 main.storyboard, lanchscene.storyboard
  - [ ] 설정파일 info.plist
- 스토리보드에서 화면에 직접 컴포넌트를 배치할 수 있음
- 뷰컴포넌트와 컨트롤러 변수/함수는 1대1로 대응시켜서 관리함
  - 컨트롤러에서 변수/함수를 삭제하고, 뷰컴포넌트 outlet 설정에서도 삭제해줘야함, 뷰컴포넌트 attributes편집창 또는 컴포넌트 우측클릭
- **swift 톺아보기**
  - 세미콜론은 안쓰는데 느낌표!랑 물음표?는 쓴다.
    - `nil` nonexistent
      - 다른언어에서 null은 주소값이 없는것
      - swift에서 nil은 값이 없는것
    - 그래서 무슨뜻?
      - ?로 nullable
      - !로 safety check를 무시하고 강제로 unwrap
        - 변수선언 부분에서 사용하면, 호출할 때마다 강제 unwrap
        - 변수호출 부분에서 사용하면, 강제 unwrap
        - 보통은 if문으로 safety check 먼저
    - [Swift - nil & Optional (물음표, 느낌표) (tistory.com)](https://dmsitter.tistory.com/102)
    - #? [Swift Optional (1). Optionals 기본 개념 | by 홍창남(Hong, Chang Nam) | Medium](https://medium.com/@codenamehong/swift-optional-1-54ae4d37ee09)
  - 함수 시그니처에 `_`(underscore)를 쓸 수 있다.
    - swift는 함수 호출시 넘기는 파라미터 앞에 라벨을 명시해야한다.
    - 라벨을 생략하고 싶을 때 `_`를 사용한다.
    - [Swift underscore(_). 함수에서의 _ (underscore) | by 홍창남(Hong, Chang Nam) | Medium](https://medium.com/@codenamehong/swift-underscore-90dcbec5072f)

```swift
//about nil
var varName: String? //nullable
varName = "Hello"
print(varName) //Optional("Hello")
print(varName!) //Hello

//about type casting
let num = "123"
let converted = Int(num)
print(converted) //Optional(123)
```

​    

## 3, 4, 5장

- **ios**
  - `viewDidLoad`
  - `CGFloat`
  - `CGSize`
  - `UIColor`
  - `view` 전역객체
  - 나중에 적용할 기능: 기기 화면크기에 컴포넌트 자동맞춤
  - `UIAlertController`
  - `UIAlertAction`
  - content hugging priority
- **swift**
  - `#`
  - `@`
  - 형변환 `String(val)`, `date as Date`
  - datepicker를 돌릴때는 다른 UI 라벨이 업데이트되지 않음, 왜?
  - 기본데이터 자료형
    - Bool
    - Int, Int32, Int64
    - Int8, Int16
    - UInt, UInt32, UInt64
    - UInt8, UInt16
    - Float, Double
    - Character
    - String
  - dateFormat 형식
  - 익명함수
  - 랜덤 idx
- **코멘트**
  - OOP 클래스상속/추상화, 의존성주입, 오버라이드/로딩을 이해하고 써보자. 예를들어 dart 위젯트리는 의존성주입임.


​      

## 1- 5장 복습, 6장

- **네비게이션 view의 생명주기** [iOS ) View의 생명주기2(Life-Cycle) / navigation controller (tistory.com)](https://zeddios.tistory.com/44?category=682195) : 네비게이션 view는 root view를 가지며, 새로 열린 view가 그 위에 스택처럼 쌓이는 구조이다. 뒤로가기를 누르면 맨 위에 있는 view가 pop되어 메모리에서 삭제되고, 전에 메모리에 로드해뒀던 view를 다시 보여준다.

- **view controller의 생명주기** [iOS ) View Controller의 생명주기(Life-Cycle) (tistory.com)](https://zeddios.tistory.com/43)
  - ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile26.uf.tistory.com%2Fimage%2F2613D13C58C64DE32C838B)
  - load 메모리에 올리고, appear 화면에 보여주고, disappear 화면에 안보이고, unload 메모리에서 삭제한다
  - **viewDidLoad**  : 뷰 로딩이 완료되었을때 시스템이 자동호출. 리소스 초기화 또는 초기화면 구성하는 용도로 사용. 화면이 처음 만들어질 때 한 번 실행.
  - **viewWillAppear** : 뷰가 백그라운드에서 포그라운드로 나올때, 처음 화면이 구성되어 보여지는 경우에 호출됨. #? 백그라운드에서 몇개까지 유지될까
  - **viewDidAppear** : 뷰가 화면에 나타난 직후
  - **viewWillDisappear** : 뷰가 화면에서 없어지기 직전
    - 첫번째뷰 - 버튼클릭 - 두번째뷰
    - 첫번째 willDisappear
    - 두번째 didLoad
    - 두번째 willAppear
    - 첫번째 didDisappear
    - 두번째 didAppear
  - **viewDidDisappear** : 뷰가 화면에서 사라지고난 직후
  - **viewDidUnload**
- **#? [[iOS] View와 Layer 관계 정리 - Coding To Coding (woookdev.github.io)](https://woookdev.github.io/programming/iOS-View와-Layer-관계-정리/)**
- `CGFloat` : 32비트에서 float으로 64비트에서 double로 처리한다.
- `CGSize` : 너비와 높이 값을 저장할 수 있는 데이터타입.

```swift
public struct CGSize {
    public var width: CGFloat
    public var height: CGFloat
    public init()
    public init(width: CGFloat, height: CGFloat)
}
```

- `UIColor` / `CGColor` [[iOS] UIColor와 CGColor의 차이점을 알아보자 — 코딩하는 체대생 (tistory.com)](https://mini-min-dev.tistory.com/89)
  - **UIColor** : UIKit 프레임워크에서 사용하는 요소의 색상값
    - 색상 데이터와 불투명도를 저장하는 개체
    - UIKit 프레임워크의 하위요소로서 사용자 인터페이스를 다루는 곳에서 지정하는 색상이다.
  - **CGColor** : Core Graphics 프레임워크에서 사용하는 요소의 색상값
    - 색상 해석 방법을 지정하는 '색상공간' 및 '색상을 정의하는 구성요소'의 집합
    - Core Graphics 프레임워크의 하위요소이다. 
- `UIAlertController ` 메시지 창 구현을 위한 뷰 컨트롤러
  - 알림창 : 화면 중앙에 배치, 버튼 가로로 가능, 모달방식이라 알림창 외 다른 부분은 반응하지 않도록 잠겨있음
  - 액션시트 : 화면 하단에 배치, 버튼 세로로, 메시지 떠 있는 동안에도 다른 영역을 건드릴 수 있으며 그 결과로 액션 시트 창이 닫힘
  - `UIAlertAction` 메시지 창 컨트롤러에 먹일 버튼 액션 객체
  - 사용방법: `UIAlertController` 인스턴스를 생성하고, 원하는 버튼을 `UIAlertAction` 객체로 만들어 먹인다. `self.present(메시지창컨트롤러객체, animated_option)` 구문으로 표시.
- **`self` #? [Swift의 Self와 self - AppyPie](https://www.appypie.com/self-swift-how-to/)**
- **content hugging priority** :triangular_flag_on_post:
  - **content hugging** 최대크기 제한, 값이 클수록 더 작아질 수 있다. 안을 때 팔이 안으로 굽는 것처럼, 값이 클 수록 컴포넌트가 더 작아질 수 있다.
    - 빨간 라벨(가로 90)과 파란 라벨(가로 10) content hugging이 같을 때 ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNQVhU%2FbtquDruGDE7%2FkI89bkM0w1EnDpOCwoQ4C0%2Fimg.png)
    - 빨간 라벨(가로 90)의 content hugging 값이 파란 라벨(가로 10)보다 작을때 ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbRpSDj%2FbtquCtUai2R%2F6qZnhnSveHDxY0yjyRmQH1%2Fimg.png)
  - **compression resistance** 최소크기 제한, 값이 클수록 더 커질 수 있다. 더 움츠러들지 않으려고 저항하는 것처럼, 값이 클 수록 컴포넌트가 더 커질 수 있다.
    - 버튼의 width의 constraint와 compression resistance가 같으면, width 제약이 UIButton 기본 width 44를 가리키므로 버튼 타이틀이 다 보이지 않는다.![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPPRgp%2FbtquCKVM7rT%2FpLO0xVqZTDbiMG1xpWDuL0%2Fimg.png)
    - 버튼의 width의 constraint가 compression resistance보다 작으면, constraint 대신 compression resistance가 적용되어 주어진 width 보다 크기가 커져 버튼 타이틀이 모두 보이게 되었다.![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFAtH5%2FbtquCZkMCEf%2FKYXRVOSMhExMfgK2ZBWhxk%2Fimg.png)

- `#` swift2 이하에서 함수 시그니처의 매개변수 이름과 라벨 이름이 같으면, 반복할 필요 없이 그 앞에 `#`을 붙이면 됐다. 이제는 더 이상 사용되지 않는다. :triangular_flag_on_post:
  - [What is the meaning of the '#' mark in swift language - Stack Overflow](https://stackoverflow.com/questions/24382118/what-is-the-meaning-of-the-mark-in-swift-language)

```swift
func someFunction(parameterName: Int) { parameterName }
someFunction(parameterName: 5) // argument label not specified

func someFunction(argumentLabel parameterName: Int) { parameterName }
someFunction(argumentLabel: 5) // argument label specified

func someFunction(_ parameterName: Int) { parameterName }
someFunction(5) // argument label omitted
```

```swift
//swift ver3.*
func someFunction(parameterName parameterName: Int) { parameterName }

//swift ver^2.* 
func someFunction(#parameterName: Int) { parameterName }
```

- `@` 컴파일러를 위한 지침이라고 보면 된다. 이를테면 view와 관련된 변수라는 뜻으로 `@IBOutlet` attribute를 사용한다. 참고로 스위프트는 타입 지정을 타입 annotation이라고 하더라. :triangular_flag_on_post:
  - [What does the '@' symbol mean in Swift? - Stack Overflow](https://stackoverflow.com/questions/30081372/what-does-the-symbol-mean-in-swift)
  - [Attributes — The Swift Programming Language (Swift 5.6)](https://docs.swift.org/swift-book/ReferenceManual/Attributes.html)
- 형변환 `String(val)`, `date as Date` :triangular_flag_on_post:
  - `as` 키워드로 캐스팅하면, 캐스팅이 불가능한 경우 컴파일도 안 된다.
  - [Swift 3.0 - as, as?, as! and is operators. Downcasting and upcasting (jayeshkawli.ghost.io)](https://jayeshkawli.ghost.io/swift-3-0-whats-is-as-as-and-as-operators/)
- **#? datepicker를 돌릴때는 다른 UI 라벨이 업데이트되지 않음, 왜?**
  - [왜 UI작업은 main thread에서 해야할까? - Neph's iOS blog (neph3779.github.io)](https://neph3779.github.io/ios/WhyUIOnlyInMainThread/)
  - [[iOS]Thread의 이해(1) - Main Thread와 Background Thread (velog.io)](https://velog.io/@yongchul/iOSThread의-기본개념)
- 기본데이터 자료형 [Swift : 기초문법 [Double / Float / Booleans] (tistory.com)](https://seons-dev.tistory.com/entry/Swift-기초문법6-Doubles과-Integers가-모두-필요한-이유)
  - Bool 불리언
  - Float 32비트 부동소수, 6자리 십진수 표현
  - Double 64비트 부동소수, 15자리 십진수 표현
  - Int 정수
- 부동소수점/단정밀도/배정밀도
  - ![sRBfNiu](https://i.imgur.com/sRBfNiu.png)
  - [TIL/그래프탐색_알고리즘.md at 4ec47becaab047795ad5d7c21d8f7201225748a3 · tae0y/TIL (github.com)](https://github.com/tae0y/TIL/blob/4ec47becaab047795ad5d7c21d8f7201225748a3/algo/그래프탐색_알고리즘.md#추가자료)


| 포맷                            | 가수 부분  (용량) | 가수 부분  (자릿수) | 지수  (크기) | 지수  (범위)       | 기수  | 데이터 길이                                                  |
| ------------------------------- | ----------------- | ------------------- | ------------ | ------------------ | ----- | ------------------------------------------------------------ |
| Binary16 (반정밀도)  (FP16)     | 11bit             | 3 자리              | 5bit         | -14 ~ + 15         | 2     | 16bit                                                        |
| **Binary32 (단정밀도)  (FP32)** | **24bit**         | **7 자리**          | **8bit**     | **-126 ~ +127**    | **2** | **32bit**                                                    |
| **Binary64 (배정밀도)  (FP64)** | **53bit**         | **15 자리**         | **5bit**     | **-1022 ~ + 1023** | **2** | **64bit**                                                    |
| Binary128 (4배정밀도)  (FP128)  | 113bit            | 34 자리             | 15bit        | -16382 ~ + 16383   | 2     | 128bit                                                       |
| Binary256 (8배정밀도)  (FP256)  | 237bit            | 71 자리             | 19bit        | -262142 ~ + 262143 | 2     | 256bit                                                       |
| Decimal32 (단정밀도)            | 21bit             | 7 자리              | 11bit        | -95 ~ + 96         | 10    | 32bit                                                        |
| Decimal64 (배정밀도)            | 51bit             | 16 자리             | 13bit        | -383 ~ + 384       | 10    | 64bit                                                        |
| Decimal128 (4배정밀도)          | 111bit            | 34 자리             | 17bit        | -6143 ~ + 6144     | 10    | 128bit부동 소수점 연산. 단정밀도와 배정밀도의 차이 - 컴퓨터 / 하드웨어 - 기글하드웨어 : https://gigglehd.com/gg/?mid=hard&document_srl=5427559 |

- dateFormat 형식 
  - 요약 [[Swift] Date() 날짜구하기, DateFormatter() 다루기 오전, 오후 등등 (tistory.com)](https://formestory.tistory.com/6)
  - 전체 [UTS #35: Unicode LDML: Dates](http://www.unicode.org/reports/tr35/tr35-31/tr35-dates.html#Date_Format_Patterns)

- 익명함수 [[Swift] 익명 함수(Anonymous Functions) : 네이버 블로그 (naver.com)](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=horajjan&logNo=220498324173)
  - java `(parameter) -> expression/{statement}`
  - swift `(parameter) -> (returnType) in expression/statement` :triangular_flag_on_post:
    - 반환타입을 생략할 수 있다
    - 파라미터가 없는 경우 in까지 모두 생략할 수 있다
    - 파라미터가 하나면 소괄호를 생략할 수 있다

- **OOP 클래스상속/추상화, 의존성주입, 오버라이드/로딩** [The Swift Language Guide (한국어) - The Swift Language Guide (한국어) (gitbook.io)](https://jusung.gitbook.io/the-swift-language-guide/)
  - [x] 옵셔널
  - [x] 프로퍼티
  - [x] 클래스/구조체
  - [x] 프로토콜
  - [x] 서브스크립트
  - [x] 오버라이드/오버로딩
  - [ ] 접근제한자
  - [ ] 클로저
  
- **팀장님 코멘트**
  - 푸시
    - 구글/애플 push서버, push토큰을 알고 있으면 푸시 다 보낼 수 있음
    - 카카오 자체서비스, push서비스를 직접구현
    - 포그라운드/백그라운드 push
    - 구글 정책에 따라 백그라운드 죽일 수도 있음
    - FCM (Firebase Cloud Messaging), 푸시서버 사용할 수도 있음
  - 서버가 필요하면 Firebase를 추천
  - 혹은 Linux, 미들웨어, mariaDB로 직접 해봐도 좋을거 같다
  - 안드로이드에서 동적으로 액티비티를 생성할 수 있는가
  - https://flutter-ko.dev/docs/get-started/flutter-for/android-devs

  

  

## swift 좀더 깊게 파보기 :nerd_face::thumbsup:

- **타입추론**(Type Inference), **타입어노테이션**(Type Annotation) :triangular_flag_on_post:

```swift
// 타입추론
var name = "tae0" 

// 타입어노테이션
var name: String 
name = "tae0"
```

- **옵셔널**(Optional) [Swift) Optional 부수기 (3) Optional Unwrapping - 옵셔널 바인딩(if let vs guard let) (tistory.com)](https://babbab2.tistory.com/17?category=828998) :triangular_flag_on_post:
  
  - 'nil'을 가질 수 있으면 '옵셔널 형식'이라고 한다. nil은 '값이 없음'을 뜻한다(빈 주소값이 아님)
    ```swift
    var name: String?
    var name2 = name
    
    name = nil //옵셔널형식으로 명시한 경우
    name2 = nil //타입추론으로 옵셔널이된 경우
    
    var name3 = nil //오류 
    ```
    
  - 옵셔널을 언랩할때
    - Optional(1)은 맞지만 Optional(nil)은 틀렸다. nil은 nil이고 옵셔널로 감싸지 않는다.
    
    - **옵셔널 강제추출**, 변수 뒤에 !를 붙이면, 어떤 값이 들어있는지 상관없이 강제로 추출됨. 그래서 보통 분기를 세워서 nil인지 검사하고 강제추출.
    
      ```swift
      var name: String?
      name = "tae0"
      
      print(name) //Optional(tae0)
      print(name!) //tae0
      if(name!=nil) print(name!) //tae0
      ```
      
    - **옵셔널 바인딩**
      - if let : 값이 nil일때 아닐때 분기해서 처리
        ```swift
        let optionalValue: Int? = nil
        
        if let nonOptionalValue = optionalValue {
        	//optionalValue는 nil이 아님
        	//optionalValue는 여전히 옵셔널 형식
          //nonOptionalValue는 중괄호 안에서만 접근
        	print(nonOptionalValue)
        } else {
        	//optioanlValue는 nil
        	print(optionalValue)
        }
        ```
      - guard let : 값이 nil이면 함수 밖으로 내쫓음
        ```swift
        let optionalValue: Int? = nil
        
        guard let nonOptionalValue = optionalValue else {
          //optionalValue는 nil
          return
        }
        print(nonOptionalValue) //nonOptionalValue를 guard문 밖에서 사용할 수 있음
        ```
      
    - **옵셔널 묵시적추출**, 변수를 선언할 때 느낌표를 붙이면 옵셔널을 논옵셔널에 대입할 때 별도 추출과정이 필요없음. 프로퍼티 지연 초기화를 위해 사용함.
      
      ```swift
      var name: String!
      name = "tae0"
      print(name) //tae0
      ```
      
    - **옵셔널 nil-coalescing operator**, nil일때 대체할 값을 지정
    
      ```swift
      let name: String? = "tae0"
      print("hello, " + (name ?? "anonymous"))
      ```
    
    - **옵셔널 체이닝** #? [Swift) Optional 부수기 (6) - Optional Chaining (옵셔널 체이닝) (tistory.com)](https://babbab2.tistory.com/32?category=828998)
    
      - 반환값은 마지막 체인에 옵셔널 씌운 것
      - 옵셔널 체이닝의 마지막 표현식은 옵셔널이더라도 ? 생략
      - 옵셔널 체이닝 중 하나라도 nil이면 이어지는 표현식은 평가하지 않고 nil을 리턴
      - 함수에도 체인을 걸 수 있는데, 함수가 옵셔널이면 앞에, 리턴값이 옵셔널이면 함수명 뒤에 물음표를 붙인다.
      - 딕셔너리에도 체인을 걸 수 있고, 딕셔너리가 옵셔널이면 앞에 물음표를 붙인다. 다만, 키로 밸류 값에 접근할 때는 무조건 딕셔너리 이름 뒤에 물음표를 붙인다.
    
      ```swift
      struct Contacts {
        var email: String
        var address: [String: String]
      }
      
      struct Person {
        var name: String
        var contacts: Contacts
        
        init(){
          //init code
        }
      }
      
      var tae0: Person? = Person(name: "tae0", email:"tae0yp@gmail.com", address:"Seoul")
      tae0?.contacts.email //반환값은 Optional<String>
      ```
  
- **구조체와 클래스** [[iOS / Swift] Swift 문법을 알아보자! - 9편 : 클래스와 구조체의 공통점과 차이점 (velog.io)](https://velog.io/@wook4506/iOS-Swift-Swift-문법을-알아보자-9편-클래스와-구조체의-공통점과-차이점) 

  - 프로퍼티, 메서드를 가지며 점(`.`)으로 프로퍼티/메서드에 접근할 수 있다.

  - **클래스만 할 수 있는 것: 언제나 참조타입, 복사하면 참조복사** :triangular_flag_on_post:

    - 상속하고 확장할 수 있음

    - 타입캐스팅할 수 있음

    - 초기화해제(deinitialize) 할 수 있음

      >인스턴스가 할당 해제되기 전에 호출된다.
      
      ```swift
      class Player {
         var coinsInPurse: Int
      
         //초기화
         init(coins: Int) {
            coinsInPurse = Bank.vendCoins(coins)
         }
      
         func winCoins(coins: Int) {
            coinsInPurse += Bank.vendCoins(coins)
         }
      
         //초기화해제
         deinit {
            Bank.receiveCoins(coinsInPurse)
         } 
      }
      ```

    - 참조횟수계산(Reference Counting)을 할 수 있음

      > swift의 Automatic RC는 **컴파일 타임에 인스턴스별 참조횟수를 계산**하고, 런타임에는 미리 계산한 참조횟수에 따라 **자원을 자동으로 해제**한다. java GC와는 런타임에 동적으로 자원 해제여부를 확인하고 해제한다는 점이 다르다. 
      >
      > 아울러 인스턴스간 **순환참조가 있으면** RC 계산이 제대로 되지 않아 **자원이 해제되지 않는다**.
      >
      > ***RC**: 모든 인스턴스는 자신을 가리키는 레퍼런스 개수를 계산해서 가지고 있다. 참조횟수가 0이 되는 시점에 자원이 해제된다.

  - **구조체만 할 수 있는 것: 언제나 값타입, 복사하면 값복사**

    - init() 메서드를 직접 작성하지 않으면 자동으로 초기화 메서드를 만들어줌

- **프로퍼티**

  - **저장 프로퍼티**: 클래스와 구조체에서, 값을 저장하기 위해 선언하는 상수/변수

    - let 클래스 인스턴스 변수는 레퍼런스를 변경할 수 없지만, 인스턴스 변수 프로퍼티는 변경할 수 있다. **레퍼런스 참조니까~**

    - let 구조체 인스턴스 변수는 그 자신과 멤버 일체를 변경할 수 없다. **값이니까~**
    ```swift
    class Human {
    	var name: String?
    	var address: String?
    	
    	init(name: String?, address: String?){
    		self.name = name
    		self.address = address
    	}
    }
    
    let tae0 = Human(name: "tae0", address: "Seoul")
    tae0 = nil //err
    tae0 = Human(name: "minsu", address: "Incheon") //err
    tae0?.name = "minsu" //OK
    ```

    ```swift
    struct Human {
    	var name: String?
    	var address: String?
    	
    //생략가능
    //	init(name: String?, address: String?){
    //		self.name = name
    //		self.address = address
    //	}
    }
    
    let tae0 = Human(name: "tae0", address: "Seoul")
    tae0 = nil //err
    tae0 = Human(name: "minsu", address: "Incheon") //err
    tae0?.name = "minsu" //err
    ```

    > 클래스는 힙 영역
    > 지역변수/구조체는 스택 영역
    > 전역변수는 데이터 영역
    > 기계어 코드는 코드 영역

    - 지연 저장 프로퍼티: 프로퍼티 앞에 `lazy` 키워드를 달아두면 처음 접근할 때 초기화 된다.

  - **연산 프로퍼티**: 클래스, 구조체, 열거형에서 사용 :triangular_flag_on_post:

    - 저장 공간을 갖지 않고, 다른 '저장 프로퍼티'의 값을 읽어 연산을 실행하거나 다른 프로퍼티로 전달받은 값을 다른 프로퍼티에 저장한다.

    - 어떠한 값을 저장하는 것이 아니기에 타입 추론으로 형식을 알 수 없어서, 반드시 선언할 때 타입 어노테이션으로 자료형을 명시해야 한다.

      ```swift
      var name: Type {
        get {
          statements
          return expr
        }
      	set(name) {
          statements
        }
      }
      ```

      ```swift
      class Person {
        var name: String = "tae0"
        
        var alias: String {
          get {
            //return alias
            return name
          }
          set(name) {
            //self.alias = name
            self.name = name
          }
        }
      }
      ```

      ```swift
      let ty: Person = .init()
      
      print(ty.alias)
      
      ty.alias = "영태"
      print(ty.alias)
      ```

  - **타입 프로퍼티**: 클래스, 구조체, 열거형에서 사용 :triangular_flag_on_post:

    - 저장타입/연산타입 프로퍼티 앞에 `static`을 붙여 선언하며 디폴트로 `lazy`하게 동작한다.

    - 저장타입 프로퍼티는 꼭 선언할 때 초기화해주어야 한다.

      ```swift
      class Human {
        static let name: String = "태영"
        static var alias: String {
          return name + " 취준끝, 최고야"
        }
      }
      ```

      ```swift
      print(Human.name) //태영
      print(Human.alias) //태영 취준끝, 최고야
      ```

    - 연산 타입 프로퍼티는 서브클래스에서 오버라이딩할 수 있음

      ```swift
      class Human {
        static var dna: String { // 오버라이드 못함
          return "blabla"
        }
        class var alias: String { //오버라이드 할 수 있음
          return "Human Type Property"
        }
      }
      
      class Ty: Human{
        override class var alias: String {
          return "Ty Type Property"
        }
      }
      
      Human.alias
      Ty.alias
      ```

  - **프로퍼티 옵저버**: 저장 프로퍼티 및 연산 프로퍼티 일부에 적용 가능 :triangular_flag_on_post:

    - willSet: 값이 저장되기 직전에 호출

    - didSet: 새 값이 저장된 직후에 호출

      ```swift
      var name: String = "Unknown" {
        willSet {
          print("현재이름=\(name), 바뀔이름=\(newValue)")
        }
        didSet {
          print("현재이름=\(name), 바뀔이름=\(oldValue)")
        }
      }
      ```

    - 연산 프로퍼티에는 부모 클래스의 연산 프로퍼티를 오버라이드하는 경우 프로퍼티 옵저버를 추가할 수 있음

- **서브스크립트**: 클래스, 구조체, 열거형에서 시퀀스의 멤버 요소에 접근하기 위한 바로가기 첨자, 단일 타입에 여러 서브스크립트를 정의할 수 있다. :triangular_flag_on_post:

  ```swift
  let nums: [Int] = [1, 2, 3, 4]
  nums[0] //1
  nums[1] //2
  ```

  ```swift
  subscript(index: Int) -> Int {
    get {
    }
    set(newValue){
    }
  }
  ```

- **확장(extension)**: 기존 코드에 새 코드 먹이기 / 클래스, 구조체, 열거형 타입에 새로운 프로퍼티, 메서드, 이니셜라이저 등을 추가하는 것으로, 원본 코드에 접근하지 못하는 타입도 확장해서 사용할 수 있다. :triangular_flag_on_post:

  - ```swift
    extension SomeType: SomeProtocol, AnotherProtocol {
    }
    ```

  - 연산 프로퍼티만 추가할 수 있다

- **상속(inheritance)**: 기존 코드를 상속해 새 코드 만들기 / 클래스만 상속 가능하며, 상속은 단일 상속만 가능하다. 클래스는 메서드, 프로퍼티 및 기타 특징들을 상속할 수 있다. :triangular_flag_on_post:

  - ```swift
    class Human: Hashable {
      var name: String?
      var age: Int?
    }
    ```

- **프로토콜이란** (인터페이스 같은거) #?[오늘의 Swift 상식 (Protocol). 프로토콜이란? | by 장국진 | Medium](https://medium.com/@jgj455/오늘의-swift-상식-protocol-f18c82571dad)

  - '타입'으로 사용되므로, 함수/메서드/이니셜라이저의 파라미터 또는 리턴타입, 상수/변수/프로퍼티 타입, 배열/딕셔너리의 원소타입으로 사용할 수 있다.

  - 저장 프로퍼티, 연산 프로퍼티를 구분하지 않고 아래와 같이 gettable/settable만 명시해준다.

    ```swift
    protocol Student {
      var height: Double { get set }
    	var name: String { get }
      static var schoolNumber: Int { get set }
    }
    ```

  - 자바 인터페이스와 차이점 :triangular_flag_on_post:
    - 기본값을 설정할 수 없음
    - 프로토콜은 optional로 선택적으로 구현할 수 있음
      -  `@objc` 상속할 때 꼭 정의 안 해도 되는 부분에 붙이면 된다.

- Delegation: 동작을 인수로 전달받아 처리하는 방식, 동작을 '위임한다'는 것이 핵심 :triangular_flag_on_post:
  - 자바에서 인터페이스로 파라미터 타입을 설정하고, 해당 인터페이스를 구현한 클래스에 동작을 담아 전달하는 것처럼
  - 스위프트는 프로토콜로 파라미터 타입을 설정하고, 해당 프로토콜을 채택한 클래스에 동작을 담아 전달하는 것임
  - 동작을 인수로 전달 / 동작을 서브클래스에 위임
- **참조값 비교 연산** :triangular_flag_on_post:
  - `===` 두 상수나 변수가 같은 인스턴스를 참조하고 있는 경우 참
  - `!==` 두 상수나 변수가 다른 인스턴스를 참조하고 있는 경우 참



## 7, 8장

- indicater view
- Outlet, Action, Outlet Collection
- webKit
  - URLRequest
- info.plist
  - App Transport Security Settings
  - Allow Arbitary Loads
- Bundle.main.path
- String.hasPrefix

- Segment Control
- kCLLocationAccuracyBest




## 9, 10, 11, 12장

- **뷰 컨트롤러 기반**
  - 페이지 컨트롤 : 페이지가 바뀔때 뷰를 삭제/생성
  - 탭바 컨트롤러 : 화면 전체선택 > editor > embed in
    - Segue
  - 내비게이션바 컨트롤러 : 화면 전체선택 > editor > embed in
    - show
    - pop
    - Segue
    - main > sub로 데이터 전달하기, sub > main으로 데이터 전달하기, delegate
  - 테이블뷰 컨트롤

- **세그웨이 옵션**
  - show : swift 2.X의 push와 유사, 새로운 뷰 컨트롤러가 스택에 푸시하면서 활성화된다, 이전 화면으로 돌아갈 때는 뷰 컨트롤러가 팝되면서 밑에 있던 뷰 컨트롤러가 활성화된다.
  - show detail : show와 비슷하지만 push가 아니라 replace된다. 현재 뷰 컨트롤러 스택의 최상단 뷰를 교체한다.
  - present modally : 새로운 뷰 컨트롤러를 보여 주는 스타일과 화면 전환 스타일을 결정하여 뷰를 모달 형태로 보여준다.
  - present as popover : 현재 보이는 뷰 컨트롤러 위에 앵커를 가진 팝업 형태로 콘텐츠 뷰를 표시한다.
  - custom : 개발자가 임의로 지정한 동작을 수행한다.



## Navigation, Tab, TableView, Segue

(작성 중)




## 메모리에 남지 않는 문자열 만들기
![](https://velog.velcdn.com/images/eddy_song/post/e09e9b98-4913-47ed-848a-a455f89bebda/image.gif)
- [(발표영상)토스ㅣSLASH 21 - 메모리에 남지 않는 문자열](https://toss.im/slash-21/sessions/3-6)
- [(요약/정리)'메모리에 남지 않는 문자열'을 만드는 방법](https://velog.io/@eddy_song/memory-string)
- 변수는 스택 영역, 객체는 힙 영역에 할당된다
- 힙 영역에서는
  - 힙 영역에서 할당 해제되면, 데이터 참조만 없어질뿐 해당 값은 '쓰레기값'으로 메모리에 남아있다
  - swift는 클래스 deinit 필드에 객체가 메모리할당 해제될때 어떻게 동작할지 정해줄 수 있다
  - 왜냐하면 ios는 gc와 달리 rc를 써서([iOS) 타 언어의 GC와 Swift ARC의 차이](https://sihyungyou.github.io/iOS-GC-vs-ARC/)), 컴파일시 해당 객체가 메모리할당 해제되는 시점을 알 수 있기 때문이다
  - 따라서 deinit 필드에 문자열과 동일한 크기로 buffer와 같은 임의데이터를 덮어씌우고 해제해주면 메모리에서 쓰레기값까지 지울 수가 있다
- 스택 영역에서는
  - 그렇다면 메모리 해제시점을 알 수 없는 스택영역의 경우는 어떻게할까?
  - 입력한 값을 별도 객체로 옮겨놓고, 스택영역에는 \-이나 \*같은 문자열로 대체한다
  - 다시 해당 객체는 deinit 필드에서 메모리해제될때 임의의 값으로 덮어씌운다



## 공통프로젝트 - 랜덤플레이트

- **랜덤메뉴추천앱**
  - 네이버 search API를 활용해 지역/키워드별 플레이스 정보 받아오기
  - 음식점만 추리고, 버튼 누르면 랜덤하에 띄워주기 (상단: 앱바 // 중간: 지도에 마커 // 하단: 카테고리, 설명, 주소, 전화번호, 세부링크) 
  - 다음목표: 백그라운드에서 정보 업데이트, DB 등에 저장, 화면 예쁘게 만들기

### 동적 레이아웃(sautolayout)

- **constraint** : 제약조건 / ***anchor**는 각 constraint항목의 기준선!*
  
  - autolayout은 위치와 크기를 상대적으로, 동적으로 지정한다. 
  - ![img](https://www.zehye.kr/assets/post-img/swift/30.png)
  - left / leading : 왼쪽 / 텍스트가 시작하는 위치로 이를테면 아랍어는 오른쪽임. WWDC 2015에서 왼쪽, 오른쪽을 특정해야 하는 상황이 아니라면 leading / trailing을 사용할 것을 권고함.
  - 이를테면 뷰 제약조건으로 leading / trailing을 30으로 주고 width를 비워두면, 어떤 기기에서도 양 사이드는 30을 비워두고 화면을 꽉 채울 수 있음.
  - 안드로이드 / iOS 비교
  
    | Android  | iOS      |
    | -------- | -------- |
    | top      | top      |
    | bottom   | bottom   |
    | left     | left     |
    | right    | right    |
    | start    | leading  |
    | end      | trailing |
    |          | centerX  |
    |          | centerY  |
    | baseline | baseline |
  
- **safe area** : 최상위 레이아웃 가이드
  - 노치가 없을 때 : 위, 아래 마진만 고려하면 됨, top / bottom layout guide
  - 노치가 생기고서 : 위, 아래, 양옆 마진을 모두 고려해야함
  - ![img](https://blog.kakaocdn.net/dn/bAPeEh/btq3y7iUJVD/kvDkiQlEfWePu169RjCm2k/img.png)

- **Intrinsic Content Size**
  - 콘텐츠에 따라 자동으로 뷰 width, height가 지정된다. 그래서 이를테면 leading은 constraint를 걸고 width와 trailing은 비워둬도 빌드가 된다.
  - 관련 뷰 종류
    | 구분                                         | **Intrinsic Contet Size Width** | **Intrinsic Contet Size Height** |
    | -------------------------------------------- | ------------------------------- | -------------------------------- |
    | **UIView**                                   | X                               | X                                |
    | **UISlider**                                 | O                               | X                                |
    | **UILabel, UIButton, UISwitch, UITextField** | O                               | O                                |
    | **TextView, ImageView**                      | Content에 따라 변화함           |                                  |

- **priority** : 제약조건 우선순위
  - 예를들어 왼쪽뷰의 trailing이 오른쪽뷰의 leading인 경우, 어느쪽이 "늘어날지" 판단해줘야함
    ![img](https://blog.kakaocdn.net/dn/1WMS9/btq3U7wo2dV/Nm9M1H56cJDW6KV94qHw70/img.png)
  -  hugging priority : 높을수록 잘 줄어듬, 허깅, 수그러듦, 안쪽으로 잘 말림
  -  compression resistance priority : 높을수록 안 줄어듬, 저항함, 안 말림

- **stackview** : 안드로이드의 ListView와 같음
  
  - constraint : autolayout을 위한 제약조건
  - spacing : 뷰끼리 간격
  - alignment : horizontal / vertical 방향/정렬
    |          | **Fill**                                                     | **Top**                                                      | **Center**                                                   | **Bottom**                                                   |
    | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
    | **특징** | 사이즈 만큼 뷰들이 채워짐                                    | 위쪽으로 정렬                                                | 가운데 정렬                                                  | 밑쪽으로 정렬                                                |
    | **비교** | ![img](https://blog.kakaocdn.net/dn/pTSLa/btrvaujJAhe/nP424LKbgkHxPOzg4mreWk/img.png) | ![img](https://blog.kakaocdn.net/dn/lIjkR/btrvbfGDpmx/0xqWkZaPetW7VLpiIBJcKK/img.png) | ![img](https://blog.kakaocdn.net/dn/cMfBMJ/btru8JaEtmd/C6zQj4tMnS80csSyDI8BPk/img.png) | ![img](https://blog.kakaocdn.net/dn/KS27X/btrvcGEZ9au/Rvu6TGGpoJ0wDNukJjdzIk/img.png) |
  
    |          | Fill                                                         | **Leading**                                                  | **Center**                                                   | **Trailing**                                                 |
    | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
    | **특징** | 사이즈 만큼 뷰들이 채워짐                                    | 왼쪽으로 정렬                                                | 가운데 정렬                                                  | 오른쪽으로 정렬                                              |
    | **비교** | ![img](https://blog.kakaocdn.net/dn/Xilvm/btru5cxGes6/DuwzfUEwqwFdaHXufAuDiK/img.png) | ![img](https://blog.kakaocdn.net/dn/8J8dW/btrvbgNkvVK/ZYbZjJTMJGFemg29gAKd4k/img.png) | ![img](https://blog.kakaocdn.net/dn/cTBpGm/btrvbffADIM/yEt7vPvXiLyDdEADvWHtGK/img.png) | ![img](https://blog.kakaocdn.net/dn/51EYH/btru9PJtzQo/OEKVuyOTfkAbKljegLh9SK/img.png) |
  - distribution
  
    |                    | 특징                                                         | 비교                                                         |
    | ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
    | Fill               | stackview 크기에 맞춰 뷰들을 채우고, priority는 사용자가 설정해주어야 함 | -                                                            |
    | Fill Equally       | 모든 뷰의 크기를 같게 맞춰줌, spacing은 사용자 설정 그대로   | ![img](https://blog.kakaocdn.net/dn/pn0nE/btrvbiRZb6O/twLAxDtJFQd8QWGS0RsVv1/img.png) |
    | Equal Spacing      | 모든 뷰의 간격이 동일함, 설정한 spacing 이상으로 뷰간 간격을 똑같이 맞춰줌 | ![img](https://blog.kakaocdn.net/dn/YkBTE/btrvcHxaXF2/luzqB8S7IoTkmg2M2K0yeK/img.png) |
    | Equal Centering    | 뷰 가운데를 기준으로 등간격으로 맞춰줌                       | ![img](https://blog.kakaocdn.net/dn/F0ks6/btrvhOaYBQn/tQ4L9tNz1HUFwd6HccMXik/img.png) |
    | Fill Propotionally | 뷰 크기가 크면 여백이 커지고 뷰 크기가 작으면 여백이 작아짐, spacing은 사용자 설정 그대로 | ![img](https://blog.kakaocdn.net/dn/Uyszx/btrvbiEpaK3/XQEcdBX6Ly7tgdj93VjUk0/img.png) |
  
- **코드로 화면그리기**  
  - 뷰를 생성
  - 뷰를 추가 addSubView / addArrangedSubView [ios - addArrangedSubview vs addSubview - Stack Overflow](https://stackoverflow.com/questions/55221703/addarrangedsubview-vs-addsubview)
    - addSubView 
    - addArrangedSubView : `.axis` `.alignment` `.distribution` `.spacing` 등으로 subview를 조정해준다.
  - `.translatesAutoResizingMaskIntoConstraints = false`
    - true면 frame을 따르고
    - false면 autolayout을 따름
  - `.topAnchor.constraint(equalTo: , constraint).isActive = true`
    - 참고로 trailingAnchor와 bottomAnchor에 한해서 constraint를 음수로 주어야한다.
    - `NSLayoutConstraint.activate` 구문을 사용해서 `[]`로 constraints를 나열해 한번에 활성화해줄 수 있다.


- **참고한자료**
  - ['iOS/AutoLayout' 카테고리의 글 목록 (tistory.com)](https://babbab2.tistory.com/category/iOS/AutoLayout)
  - ['아이폰 개발/ios 디자인' 카테고리의 글 목록 (tistory.com)](https://qteveryday.tistory.com/category/아이폰 개발/ios 디자인)
  - [ConstraintLayout vs auto layout (bignerdranch.com)](https://bignerdranch.com/blog/constraintlayout-vs-auto-layout-how-do-they-compare/)
  - layout driven ui https://developer.apple.com/videos/play/wwdc2018/233?time=525 / swiftUI는 ios13 이상부터만 쓸 수 있음 / `@state` `@combine` / RxSwift 
- **목표**
  - [x] ~~UIView autolayout, constraint, anchor, addArrangedSubview, adaptive layout~~
  - [ ] gestureRecognizer, scrollview/button touch
  



### 터치액션 컨트롤 (GestureRecognizer)

(작성 중)



## 개인프로젝트 - 냉장고파먹기

- **개발할때 어려웠던 점**
  - :man_dancing:**데이터 파싱/디코딩/저장** : 레시피 목록 CSV 파일을 파싱해서 JSON으로 변환, 다시 Realm 객체에 담아 저장하는 과정. 
    - 공공데이터 포털에서 내려받은 CSV 파일은 UTF-8, UNICODE로 디코딩되지 않아 계속해서 오류가 났다. 데이터가 너무 커서 로컬에서는 애플 스프레드로 열리지도 않았다. 구글 드라이브에 올려 스프레드 시트에서 CSV로 다시 변환해서 내려받은 후 UTF-8로 디코딩해 사용했다.
    - 파일을 프로젝트 폴더에 포함시켰는데, `./fileName.csv` 같은 상대경로로 참조할 수 없었다. 뷰 컨트롤러가 실제로 어떤 디렉토리에서 작업 중인지 모르겠다.
  - :runner:**데이터 저장후 뷰에 반영** : 사용자가 입력한 요리재료를 Realm 데이터베이스에 저장까지는 성공했지만, 변경을 감지해 화면에 다시 불러오는 부분은 구현하지 못했다. 
    - 등록 후 네비게이션 컨트롤러와 세그웨이를 타고 목록 화면으로 돌아가는 시점에서 화면을 다시 불러오는 방법, 또는 목록화면에서 Realm 데이터베이스 변경사항을 자동으로 감지해서 다시 불러오는 방법 두 가지가 있겠다.
    - 더 적합한 방법을 고르라면 첫번째겠는데, 구현해보고 싶은 방법은 두번째이다. 탭/네비게이션바와 세그웨이가 뒤섞인 상태에서 뷰 생명주기가 어떻게 돌아가는지 공부할 기회가 될 것 같다.
  - 알림 기능 어떻게 테스트하지?
    - 실기기, 맥에 구동
    - 애플 개발자 등록
  - 검색 기능 어떻게 구현할까?
  - 시금치 가격정보
  - 도서 바코드정보



## 참고한 자료

- [iOS ) NavigationBar (tistory.com)](https://zeddios.tistory.com/574)
- [Segue 파헤치기 (jcsoohwancho.github.io)](https://jcsoohwancho.github.io/2019-07-28-Segue-파헤치기/)
  - [what is segue selector - Google 검색](https://www.google.com/search?q=what+is+segue+selector&sxsrf=ALiCzsamqZsxjobGSr9coBHX3rJzesgN8A%3A1661053107691&ei=s6gBY-_tKZOjoASM2q-IDQ&ved=0ahUKEwivk7-Dgdf5AhWTEYgKHQztC9EQ4dUDCA4&uact=5&oq=what+is+segue+selector&gs_lcp=Cgdnd3Mtd2l6EAM6BwgAEEcQsANKBAhBGABKBAhGGABQhwRY1Q5gqBBoAXABeACAAY4BiAH1B5IBAzAuOJgBAKABAcgBCsABAQ&sclient=gws-wiz)
- table view vs table view controller
  - [objective c - UITableViewController vs TableView - Stack Overflow](https://stackoverflow.com/questions/9694185/uitableviewcontroller-vs-tableview)
  - [iOS) 테이블뷰 (UITableView) 기초 - (2) :: 운노스의 iOS (tistory.com)](https://woonhyeong.tistory.com/6)
- [[iOS/Swift] Toast Message 만들기 (tistory.com)](https://royhelen.tistory.com/46)
- Realm / view
  - [iOS ) View Controller의 생명주기(Life-Cycle) (tistory.com)](https://zeddios.tistory.com/43)
    - viewWillAppear() 리로드할 수 있음
    - viewDidLoad() 리로드 못함
  - [Swift(스위프트) - Realm 설치 및 연동 예제 (tistory.com)](https://value-of-life.tistory.com/154?category=888433)
  - [[Swift/Realm] realm 데이터 모델 @persisted의 의미, property wrapper (velog.io)](https://velog.io/@luboolu/SwiftRealm-realm-데이터-모델-persisted의-의미-property-wrapper)
  - [[Swift] Realm의 특징과 사용법 (velog.io)](https://velog.io/@dlskawns96/Swift-Realm의-특징과-사용법)
  - [ios - RLMException, Migration is required for object type - Stack Overflow](https://stackoverflow.com/questions/33363508/rlmexception-migration-is-required-for-object-type)
  - [성능 향상과 메모리 사용량 최소화에 최적화된 Realm API를 소개합니다.](https://academy.realm.io/kr/posts/realm-api-optimized-for-performance-and-low-memory-use/)
  - [iOS Swift 라이브러리 Realm 사용하기 (tistory.com)](https://gonslab.tistory.com/16)
  - [ios - RealmSwift: Convert Results to Swift Array - Stack Overflow](https://stackoverflow.com/questions/31100011/realmswift-convert-results-to-swift-array)
  - [RxSwift Realm(3) - realm변경 감지 (Observable.changeset) (tistory.com)](https://myseong.tistory.com/15)
  - [Realm swift struct 타입, List타입 수정 하는법 :: Dumb-veloper (tistory.com)](https://dev-in-gym.tistory.com/134)
- 알림
  - [[TIL] 2021.02.05 (velog.io)](https://velog.io/@sainkr/TIL-2021.02.05)

- ios swift URLSession : [[iOS/Swift] HTTP/HTTPS 통신의 기본, URLSession (tistory.com)](https://tngusmiso.tistory.com/50)
- 스플래시 [[IOS]스플래시 이미지 적용#02 - 커스텀 뷰 컨트롤러를 사용하여 애니메이션까지! - StakTree](https://staktree.github.io/ios/IOS-splash-02/)
- CSV to JSON
  - [Quick CSV to JSON in Swift (github.com)](https://gist.github.com/algal/ceb17773bbc01e9b6bb1)
  - [Easily read a CSV in Swift (for Newbies) | by Jason Pettett | Medium](https://medium.com/@deadbeef404/reading-a-csv-in-swift-7be7a20220c6)
- 로딩중
  - [swift 로딩 중 표시하기 - Better me than yesterday (tistory.com)](https://42kchoi.tistory.com/376)
  - [[iOS - swift] 로딩화면 구현 방법, UIActivityIndicatorView (tistory.com)](https://ios-development.tistory.com/985)




## 개인프로젝트 주제모음

- **박스오피스앱**
  - 이달의 박스오피스
  - 무한스크롤 / 빠른이미지로딩, 로딩안될때는 스켈레톤
- **냉장고 관리앱**
  - 바코드인식해서 물품등록, 유통기한도 입력
  - 유통기한 얼마 안남았을때 알려주기
  - 남은재료로 할 수 있는 음식 알려주기
- **TIL레포 관리앱**
  - 모바일 마크다운 에디터
  - 페이지 단위로 랜덤하게 띄워주기
  - 기억나면 왼쪽, 기억안나면 오른쪽 스와이프
- **동선 짜주는 앱**
  - 출발지와 목적지, 경유지를 입력하면 어떤 동선으로 가야할지 알려줌
  - 어떤 지역을 선택하면 해당 지역에서 추천맛집/명소 동선을 짜줌
  
- **약관리**
  - 같이 먹으면 안되는 약 알려주기
  - 매일 알림으로 먹었는지 알려주기
  



## 도전과제 주제모음

- [iOS10 ) TTS(Text-To-Speech) 구현 (tistory.com)](https://zeddios.tistory.com/42?category=682195)
- [iOS10 ) STT(Speech-To-Text) 구현 (tistory.com)](https://zeddios.tistory.com/45?category=682195)
- [칸루 (khanlou.com)](https://khanlou.com/)
