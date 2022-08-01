# ConstraintLayout vs Auto Layout: How Do They Compare?

- **2016/10/06 포스팅된 글** / 안드로이드에 ConstraintLayout이 추가된시점
- **플랫폼별 적응형 UI**
  - 안드로이드는 constraintLayout
  - ios는 autoLayout
- **방식**
  - Cassowary라는 선형방정식/부등식 해결 알고리즘을 활용
  - UI요소의 매개변수(뷰의 위치, 크기, 서로간의 관계)를 인수로 받아 방정식 풀이



## Constraint

- 제약조건 : 뷰 속성간 관계를 지정하는 규칙
  - view1과 view2의 수직 위치를 맞추고 싶다면 
    - 수동으로 위치를 설정하는 대신 `view1.top = 10px`, `view2.top = 10px` 
    - 제약조건을 걺 `view1.top = view2.top`
- 플랫폼별 예시, 아래와 같이 XML을 수정하거나 동적으로 설정하거나 할 수 있다
  - android
    ![상위 정렬 iOS](https://bignerdranch.com/assets/img/blog/2016/10/top_aligned_ios_2.png)
  - ios
    ![상위 정렬 iOS](https://bignerdranch.com/assets/img/blog/2016/10/top_aligned_android.png)


## Anchor

- 제약조건에서 설정하는 뷰 속성값, 뷰 위치를 어디에 맞출지 정의
- 안드로이드와 ios는 앵커이름이 거의 비슷하다
  - start/leading : 글자가 시작하는 방향 (이를테면 아랍어에서는 오른쪽이고, 한글에서는 왼쪽)
  - end/trailing
  - ios에서는 특별한 경우가 아니라면 left/right보다 leading/trailing을 권장하고 있음

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
| baseline | baselin  |

- 안드로이드는 가이드라인과 left/right 앵커를 동시에 사용해 centerX, centerY 효과를 낼 수 있다
- 또한 안드로이드는 가이드라인에 대해서 begin/percent 앵커를 적용할 수 있다



## Guideline, Layout Guides and Margins

- 가이드라인은 자동 레이아웃에서 화명 상/하단 표시줄, 노치 등을 처리하는 데 사용한다
- 안드로이드는 `Interface Bilder`를 사용해 가로/세로 참조선을 추가할 수 있고, 해당 안내선은 레이아웃 편집시에만 존재
- 반면 안드로이드 guideline은 `View.GONE`으로 화면에 표시되지 않는 개체를 생성
  ```xml
  <android.support.constraint.Guideline
      ...
      android:orientation="vertical"
      app:layout_constraintGuide_percent="0.5"/>
  ```



## Defining Constraints

- **안드로이드**
  - 제약조건은 단방향이며 한 뷰에서 다른 뷰로 전달된다
    - `app:layout_constraintAnchor1_toAnchor2Of="@id/view2"`
    - 위와 같이 해당 뷰의 레이아웃 매개변수로 제약조건을 정의
  - 명시적인 우선순위가 없으며 모든 제약조건이 필요
- **ios**
  - 0 ~ 1000까지 우선순위를 명시하고, 우선순위가 낮으면 더 빨리 깨질 수 있음
  - 제약조건은 별도 개체이며 가장 가까운 공통조상 뷰에서 정의된다
    - 뷰의 너비와 높이는 뷰 자체에서 결정
    - 뷰와 부모 뷰간 제약조건은 부모 뷰에서 결정
    - 형제 뷰간 제약조건은 부모 뷰에서 결정
    - 그리고 우선순위가 높은 뷰에서 결정



## Mental Model

- **ios**
  - 각 뷰에 수직/수평 위치 및 크기를 결정하기에 충분한 제약조건이 있어야 한다
  - UILabel은 텍스트에 따라 너비/높이가 결정되므로, 일반적으로 위치 제약조건만 필요하다
  - UIImageView는 이미지에 따라 크기를 유추할 수도 있지만, 명시적으로 너비/높이 제약조건을 추가할 수도 있다
- **안드로이드**
  - 너비/높이를 아래와 같이 지정할 수 있다
  - `wrap_content` : 내부 콘텐츠를 감싸는 정도까지
  - 고정너비 `dp` : 특정 dp값으로 너비를 고정함
  - 모든크기 `0dp` : 제약조건을 충족하면서 뷰가 나머지 공간을 차지함
    - `match_parent` 또는 `fill_parent` : 마진을 제외하고 나머지 공간을 차지함



## Android Anchor Compatibility : ConstratintLayout

- 앵커 조합은 '동일한 유형'끼리만 가능하다
  - 수직은 수직끼리, 수평은 수평끼리
  - start/end와 left/right를 혼합할 수는 없다
  - guideline 자체에 제약조건을 걸려면 다른 guideline으로 걸어야 한다  

| Anchors     | Type                 |
| ----------- | -------------------- |
| Baseline    | Vertical (Text only) |
| Top, Bottom | Vertical             |
| Start, End  | Horizontal (1)       |
| Left, Right | Horizontal (2)       |
  
- 텍스트 기준선 맞추는 방법
  - ConstraintLayout은 baseline guideline으로
  - LinearLayout은 baselineAlinged
  - RelativeLayout은 align_baselineTo



## iOS Anchor Compatibility : AutoLayout 

- autolayout은 제약조건 호환성을 유지하기 위해, 
  - 코드단에서 제약조건을 정의할 때 별도의 제네릭 클래스를 사용한다
  - 해당 클래스는 모두 NSLayoutAnchor의 서브클래스로서 아래와 같이 정의한다
    ```swift
    class NSLayoutAnchor<AnchorType : AnyObject> : NSObject {
        ...
        func constraint(equalTo anchor: NSLayoutAnchor<AnchorType>) -> NSLayoutConstraint
        ...
    }
    ```
  - 서브 클래스는 자기자신을 제네릭 제약조건으로 사용한다
    - class ==NSLayoutXAxisAnchor== : NSLayoutAnchor\<==NSLayoutXAxisAnchor==\> {
  - 위와 같은 방식으로 프로그래밍 언어의 타입시스템을 활용한다 (swift, objective-c 동일)

| Anchors           | Type                 | Class               |
| ----------------- | -------------------- | ------------------- |
| Baseline          | Vertical (Text only) | NSLayoutYAxisAnchor |
| Top, Bottom       | Vertical             | NSLayoutYAxisAnchor |
| Leading, Trailing | Horizontal (1)       | NSLayoutXAxisAnchor |
| Left, Right       | Horizontal (2)       | NSLayoutXAxisAnchor |
| Width, Height     | Dimension            | NSLayoutDimension   |

- `NSLayoutAnchor`는 다른 앵커/상수에 따라 `NSLayoutConstraints`를 생성하는 메서드를 정의한다
  - `<REL>`이 equal, less than equal, greater than or equal인 경우
  - `anchor1 <REL> anchor2` / `anchor1 <REL> anchor2 + constant`와 같은 제약조건을 어떻게 생성할지 메서드로 정의한다
- `NSLayoutXAxisAnchor`와 `NSLayoutYAxisAnchor`는 `NSLayoutAnchor` 메서드를 오버라이딩하지 않는다
- `NSLayoutDimension`은 메서드를 오버라이드해서 `anchor1 <REL> constant`과 `anchor1 <REL> multiplier * anchor2 + constant` 방식을 추가한다 



## Conclusion

- ConstraintLayout과 autoLayout은 Cassowary라는 같은 알고리즘에 기반
- anchor/constratint와 같이 용어도 비슷
- 그러나 API에 대한 접근방식, 세부적인 메커니즘은 조금씩 다름
