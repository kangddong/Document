> 출처
> [https://developer.apple.com/documentation/swiftui/stateobject](https://developer.apple.com/documentation/swiftui/stateobject)

# Stateobject(상태 개체)
관찰 가능한 객체를 인스턴스화하는 속성 래퍼 유형.
```swift
@MainActor @frozen @propertyWrapper @preconcurrency
struct StateObject<ObjectType> where ObjectType : ObservableObject
```

<hr class="header">

## 개요


뷰 계층 구조에 저장하는 참조 유형의 단일 진실 공급원으로 상태 객체를 사용하십시오. 속성 선언에 @StateObject 속성을 적용하고 [ObservableObject](app-services/combine/observable-objects/observableobject.md) 프로토콜을 준수하는 초기 값을 제공하여 [App](https://developer.apple.com/documentation/swiftui/app), [Scene](https://developer.apple.com/documentation/swiftui/scene) 또는 [View](https://developer.apple.com/documentation/swiftui/view)에서 상태 객체를 만듭니다. SwiftUI가 제공하는 스토리지 관리와 충돌할 수 있는 멤버와이즈 이니셜라이저에서 설정하지 않도록 상태 개체를 비공개로 선언합니다.

```swift
class DataModel: ObservableObject {
    @Published var name = "Some Name"
    @Published var isEnabled = false
}

struct MyView: View {
    @StateObject private var model = DataModel() // 상태 객체 생성.

    var body: some View {
        Text(model.name) // 데이터 모델이 변경시에 업데이트.
        MySubView()
            .environmentObject(model)
    }
}
```

SwiftUI는 상태 객체를 선언하는 컨테이너의 수명 동안 한 번만 모델 객체의 새 인스턴스를 생성합니다. 예를 들어, SwiftUI는 뷰의 입력이 변경되면 새 인스턴스를 생성하지 않지만, 뷰의 ID가 변경되면 새 인스턴스를 생성합니다. 관찰 가능한 객체의 게시된 속성이 변경되면 SwiftUI는 위의 예제의 [Text](https://developer.apple.com/documentation/swiftui/text) 뷰처럼 해당 속성에 의존하는 모든 뷰를 업데이트합니다.


{% hint style="info" %}
**노트**
구조, 문자열 또는 정수와 같은 값 유형을 저장해야 하는 경우, 대신 [State](https://developer.apple.com/documentation/swiftui/state) 속성 래퍼를 사용하십시오. 또한 [Observable()](https://developer.apple.com/documentation/Observation/Observable()) 프로토콜을 준수하는 참조 유형을 저장해야 하는 경우 [State](https://developer.apple.com/documentation/swiftui/state)를 사용하십시오. SwiftUI의 관찰에 대해 자세히 알아보려면, [앱에서 모델 데이터 관리](https://developer.apple.com/documentation/swiftui/managing-model-data-in-your-app)를 참조하십시오.
{% endhint %}



### 하위 뷰와 상태 개체 공유

[ObservedObject](app-frameworks/swiftui/model-data/observedobject.md) 속성이 있는 속성을 통해 상태 객체를 하위 뷰로 전달할 수 있습니다. 또는 위 코드의 MySubView처럼 [`environmentObject(_:)`](https://developer.apple.com/documentation/swiftui/view/environmentobject(_:)) 수정자를 뷰에 적용하여 뷰 계층의 환경에 객체를 추가하십시오. 그런 다음 [EnvironmentObject](app-frameworks/swiftui/model-data/environmentobject.md) 속성을 사용하여 MySubView 내부의 객체 또는 그 후손을 읽을 수 있습니다.

```swift
struct MySubView: View {
    @EnvironmentObject var model: DataModel

    var body: some View {
        Toggle("Enabled", isOn: $model.isEnabled)
    }
}
```

달러 기호($) 연산자를 사용하여 상태 객체의 속성에 [바인딩](https://developer.apple.com/documentation/swiftui/binding)을 가져옵니다. 양방향 연결을 만들고 싶을 때 바인딩을 사용하세요. 위의 코드에서, [토글](https://developer.apple.com/documentation/swiftui/toggle)은 바인딩을 통해 모델의 isEnabled 값을 제어합니다.

### 외부 데이터를 사용하여 상태 개체를 초기화합니다.

상태 객체의 초기 상태가 컨테이너 외부에서 오는 데이터에 의존하는 경우, 컨테이너의 이니셜라이저 내에서 객체의 이니셜라이저를 명시적으로 호출할 수 있습니다. 예를 들어, 이전 예제의 데이터 모델이 초기화 중에 이름 입력을 받고 뷰 외부에서 오는 해당 이름에 대한 값을 사용하고 싶다고 가정합니다. 뷰에 대해 생성한 명시적 이니셜라이저 내에서 상태 객체의 이니셜라이저를 호출하여 이를 수행할 수 있습니다.

```swift
struct MyInitializableView: View {
    @StateObject private var model: DataModel

    init(name: String) {
        // SwiftUI는 초기화 클로저를 통해 생성한 상태 객체가
        // 뷰의 수명 동안 단 한 번만 생성되도록 보장합니다.
        // 나중에 뷰의 name 속성의 입력을 변경해도 영향을 미치지 않습니다.
        _model = StateObject(wrappedValue: DataModel(name: name))
    }

    var body: some View {
        VStack {
            Text("Name: \(model.name)")
        }
    }
}
```

이것을 할 때 주의하세요. SwiftUI는 주어진 뷰에서 초기화를 처음 호출할 때만 상태 객체를 초기화합니다. 이는 뷰의 입력이 변경되더라도 객체가 안정적인 저장 공간을 제공하도록 보장합니다. 그러나 상태 개체를 명시적으로 초기화하면 예기치 않은 동작이나 원치 않는 부작용이 발생할 수 있습니다.

위의 예에서, MyInitializableView에 입력된 name이 변경되면, SwiftUI는 새로운 값으로 뷰의 이니셜라이저를 다시 실행합니다. 그러나 SwiftUI는 상태 객체의 이니셜라이저를 처음 호출할 때만 상태 객체의 이니셜라이저에 제공하는 자동 클로저를 실행하므로 모델의 저장된 이름 값은 변경되지 않습니다.

명시적 상태 객체 초기화는 객체가 의존하는 외부 데이터가 객체 컨테이너의 주어진 인스턴스에 대해 변경되지 않을 때 잘 작동합니다. 예를 들어, 다른 상수 이름을 가진 두 개의 뷰를 만들 수 있습니다:

```swift
var body: some View {
    VStack {
        MyInitializableView(name: "Ravi")
        MyInitializableView(name: "Maria")
    }
}
```

{% hint style="warning" %}
**중요**
구성 가능한 상태 개체의 경우에도, 당신은 여전히 그것을 비공개로 선언합니다. 이를 통해 뷰의 멤버별 이니셜라이저를 통해 실수로 매개 변수를 설정할 수 없도록 합니다. 그렇게 하면 프레임워크의 저장 관리와 충돌하고 예상치 못한 결과가 발생할 수 있기 때문입니다.
{% endhint %}

## 뷰 아이덴티티를 변경하여 강제 재초기화

뷰 입력이 변경될 때 SwiftUI가 상태 개체를 다시 초기화하도록 하려면 뷰의 ID가 동시에 변경되는지 확인하십시오. 이를 수행하는 한 가지 방법은 [`id(_:)`](https://developer.apple.com/documentation/swiftui/view/id(_:)) 수정자를 사용하여 변경되는 값에 뷰의 ID를 바인딩하는 것입니다. 예를 들어, name 입력이 변경될 때 MyInitializableView 인스턴스의 ID가 변경되도록 할 수 있습니다.

```swift
MyInitializableView(name: name)
    .id(name) // Binds the identity of the view to the name property.
```

{% hint style="info" %}
**노트**
당신의 뷰가 [ForEach](https://developer.apple.com/documentation/swiftui/foreach) 안에 나타나면, 해당 데이터 요소의 식별자를 사용하는 [`id(_:)`](https://developer.apple.com/documentation/swiftui/view/id(_:)) 수정자를 암시적으로 수신합니다.
{% endhint %}

하나 이상의 값의 변경에 따라 상태를 재초기화하기 위해 뷰가 필요한 경우, [Hasher](https://developer.apple.com/documentation/Swift/Hasher)를 사용하여 값을 단일 식별자로 결합할 수 있습니다. 예를 들어, 이름 또는 isEnabled의 값이 변경될 때 MyInitializableView에서 데이터 모델을 업데이트하려면 두 변수를 하나의 해시로 결합할 수 있습니다.

```swift
var hash: Int {
    var hasher = Hasher()
    hasher.combine(name)
    hasher.combine(isEnabled)
    return hasher.finalize()
}
```

그런 다음 결합된 해시를 식별자로 보기에 적용하십시오:

```swift
MyInitializableView(name: name, isEnabled: isEnabled)
    .id(hash)
```

입력이 변경될 때마다 상태 개체를 다시 초기화하는 성능 비용을 염두에 두십시오. 또한, 뷰 아이덴티티를 바꾸는 것은 부작용이 있을 수 있다. 예를 들어, SwiftUI는 뷰의 ID가 동시에 변경되면 뷰 내부의 변경 사항을 자동으로 애니메이션화하지 않습니다. 또한 ID를 변경하면 State, FocusState, GestureState 등으로 관리하는 값을 포함하여 뷰가 보유하는 모든 상태가 재설정됩니다.

<hr class="overview">

## 주제

### 상태 객체 생성하기
[`init(wrappedValue: @autoclosure () -> ObjectType)`](https://developer.apple.com/documentation/swiftui/stateobject/init(wrappedvalue:))
	초기 래핑 값으로 새로운 상태 객체를 생성합니다.

### 값 읽어오기
[`var wrappedValue: ObjectType`](https://developer.apple.com/documentation/swiftui/stateobject/wrappedvalue)
	상태 객체가 참조하는 기본 값.

[`var projectedValue: ObservedObject<ObjectType>.Wrapper`](https://developer.apple.com/documentation/swiftui/stateobject/projectedvalue)
	속성에 대한 바인딩을 생성하는 상태 객체의 투영.

<hr class="topics">

## 관계

### 채택

[`DynamicProperty`](https://developer.apple.com/documentation/swiftui/dynamicproperty), [`Sendable`](https://developer.apple.com/documentation/Swift/Sendable)

<hr class="relationship">

## 같이보기

### 모델 데이터 생성

[Managing model data in your app](https://developer.apple.com/documentation/swiftui/managing-model-data-in-your-app)
앱의 데이터 모델과 뷰 간의 연결을 만듭니다.

[Migrating from the Observable Object protocol to the Observable macro](https://developer.apple.com/documentation/swiftui/migrating-from-the-observable-object-protocol-to-the-observable-macro)
Swift에서 Observation의 이점을 활용하려면 기존 앱을 업데이트하세요.

[`@attached(member, names: named(_$observationRegistrar), named(access), named(withMutation)) @attached(memberAttribute) @attached(extension, conformances: Observable) macro`](https://developer.apple.com/documentation/Observation/Observable())
[Observable()](https://developer.apple.com/documentation/Observation/Observable())
	관찰 가능한 프로토콜의 적합성을 정의하고 구현합니다.

[Monitoring data changes in your app](https://developer.apple.com/documentation/swiftui/monitoring-model-data-changes-in-your-app)
관찰 가능한 개체를 사용하여 앱의 사용자 인터페이스에서 데이터에 대한 변경 사항을 표시합니다.

[`struct ObservedObject`](https://developer.apple.com/documentation/swiftui/observedobject)
	관찰 가능한 객체에 가입하고 관찰 가능한 객체가 변경될 때마다 뷰를 무효화하는 속성 래퍼 유형.

[`protocol ObservableObject : AnyObject`](https://developer.apple.com/documentation/Combine/ObservableObject)
	객체가 변경되기 전에 방출되는 게시자가 있는 객체 유형.










