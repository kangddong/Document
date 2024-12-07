> 출처
> [https://developer.apple.com/documentation/swiftui/observedobject](https://developer.apple.com/documentation/swiftui/observedobject)

# ObservedObject(관찰 객체)
관찰 가능한 객체를 구독하고 관찰 가능한 객체가 변경될 때마다 뷰를 무효화하는 속성 래퍼 유형.
```swift
@MainActor @propertyWrapper @preconcurrency @frozen
struct ObservedObject<ObjectType> where ObjectType : ObservableObject
```

<hr class="header">

## 개요


입력이 [ObservableObject](app-services/combine/observable-objects/observableobject.md)일 때 SwiftUI [View](https://developer.apple.com/documentation/swiftui/view)의 매개 변수에 @ObservedObject 속성을 추가하고 객체의 게시된 속성이 변경될 때 뷰가 업데이트되기를 원합니다. 일반적으로 [StateObject](app-frameworks/swiftui/model-data/stateobject.md)를 하위 뷰로 전달하기 위해 이렇게 합니다.

다음 예제는 데이터 모델을 관찰 가능한 객체로 정의하고, 뷰에서 모델을 상태 객체로 인스턴스화한 다음, 인스턴스를 관찰 객체로 하위 뷰로 전달합니다.

```swift
class DataModel: ObservableObject {
    @Published var name = "Some Name"
    @Published var isEnabled = false
}

struct MyView: View {
    @StateObject private var model = DataModel()

    var body: some View {
        Text(model.name)
        MySubView(model: model)
    }
}

struct MySubView: View {
    @ObservedObject var model: DataModel

    var body: some View {
        Toggle("Enabled", isOn: $model.isEnabled)
    }
}
```

관찰 가능한 객체의 게시된 속성이 변경되면 SwiftUI는 객체에 의존하는 모든 뷰를 업데이트합니다. 하위 뷰는 또한 위의 예에서 [토글](https://developer.apple.com/documentation/swiftui/toggle)과 같은 모델 속성을 업데이트할 수 있으며, 이는 뷰 계층 구조 전반에 걸쳐 다른 관찰자에게 전파됩니다.

관찰 객체에 대한 기본값 또는 초기 값을 지정하지 마십시오. 위의 예에서와 같이 뷰의 입력 역할을 하는 속성에만 속성을 사용하십시오.

{% hint style="info" %}
**노트**
@ObservedObject로 [Observable](https://developer.apple.com/documentation/Observation/Observable) 프로토콜을 준수하는 개체를 래핑하지 마십시오. SwiftUI는 본문 내에서 사용되는 Observable 객체에 대한 종속성을 자동으로 추적하고 데이터가 변경되면 종속 뷰를 업데이트합니다. @ObservedObject로 Observable 객체를 래핑하려고 하면 래핑된 객체가 [ObservableObject](app-services/combine/observable-objects/observableobject.md) 프로토콜을 준수해야 하기 때문에 컴파일러 오류가 발생할 수 있습니다.

뷰가 본문에서 Observable 객체의 속성에 바인딩이 필요한 경우, 대신 [Bindable](https://developer.apple.com/documentation/swiftui/bindable) 속성 래퍼로 객체를 감싸십시오; 예를 들어, @Bindable var model: DataModel. 자세한 정보는 [앱에서 모델 데이터 관리](https://developer.apple.com/documentation/swiftui/managing-model-data-in-your-app)를 참조하십시오.
{% endhint %}

<hr class="overview">

## 주제

### 관찰 객체 생성하기
[`init(wrappedValue: ObjectType)`](https://developer.apple.com/documentation/swiftui/observedobject/init(wrappedvalue:))
	초기 래핑 값으로 관찰된 개체를 만듭니다.

[`init(initialValue: ObjectType)`](https://developer.apple.com/documentation/swiftui/observedobject/init(initialvalue:))
	초기 값으로 관찰된 개체를 만듭니다.

### 값 읽어오기
[`var wrappedValue: ObjectType`](https://developer.apple.com/documentation/swiftui/observedobject/wrappedvalue)
	관찰 객체가 참조하는 기본 값.

[`var projectedValue: ObservedObject<ObjectType>.Wrapper`](https://developer.apple.com/documentation/swiftui/observedobject/projectedvalue)
	속성에 대한 바인딩을 생성하는 관찰 객체의 투영.

[`struct Wrapper`](https://developer.apple.com/documentation/swiftui/observedobject/wrapper)
	속성에 대한 바인딩을 생성할 수 있는 기본 관찰 가능한 객체의 래퍼.

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

[`struct StateObject`](app-frameworks/swiftui/model-data/stateobject.md)
	관찰 가능한 객체를 인스턴스화하는 속성 래퍼 유형.

[`protocol ObservableObject : AnyObject`](app-services/combine/observable-objects/observableobject.md)
	객체가 변경되기 전에 방출되는 게시자가 있는 객체 유형.