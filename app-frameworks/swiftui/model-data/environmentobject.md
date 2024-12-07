> 출처
> [https://developer.apple.com/documentation/swiftui/environmentobject](https://developer.apple.com/documentation/swiftui/environmentobject)

# EnvironmentObject(환경 객체)
부모 또는 조상 뷰가 제공하는 관찰 가능한 객체에 대한 속성 래퍼 유형.
```swift
@MainActor @frozen @propertyWrapper @preconcurrency
struct EnvironmentObject<ObjectType> where ObjectType : ObservableObject
```

<hr class="header">

## 개요

환경 객체는 [ObservableObject](app-services/combine/observable-objects/observableobject.md)에 부합하는 관찰 가능한 객체가 변경될 때마다 현재 뷰를 무효화합니다. 속성을 환경 객체로 선언하는 경우, [`environmentObject(_:)`](https://developer.apple.com/documentation/swiftui/view/environmentobject(_:)) 수정자를 호출하여 조상 부에서 해당 모델 객체를 설정해야 합니다.

{% hint style="info" %}
**노트**
관찰 가능한 객체가 [Observable](https://developer.apple.com/documentation/Observation/Observable) 프로토콜을 준수하는 경우, EnvironmentObject 대신 [@Environment](https://developer.apple.com/documentation/swiftui/environment)를 사용하고 [`environment(_:)`](https://developer.apple.com/documentation/swiftui/view/environment(_:)) 또는 [`environment(_:_:)`](https://developer.apple.com/documentation/swiftui/view/environment(_:_:)) 수정자를 호출하여 조상 뷰에서 모델 객체를 설정하십시오.
{% endhint %}

<hr class="overview">

## 주제

### 환경 객체 생성하기
[`init()`](https://developer.apple.com/documentation/swiftui/environmentobject/init())
	환경 개체를 만듭니다.

### 값 읽어오기
[`var wrappedValue: ObjectType`](https://developer.apple.com/documentation/swiftui/environmentobject/wrappedvalue)
	환경 객체가 참조하는 기본 값.

[`var projectedValue: EnvironmentObject<ObjectType>.Wrapper`](https://developer.apple.com/documentation/swiftui/environmentobject/projectedvalue)
	동적 멤버 조회를 사용하여 속성에 바인딩을 생성하는 환경 개체의 투영.

[`struct Wrapper`](https://developer.apple.com/documentation/swiftui/environmentobject/wrapper)
	동적 멤버 조회를 사용하여 속성에 바인딩을 생성할 수 있는 기본 환경 개체의 래퍼.

<hr class="topics">

## 관계

### 채택

[`DynamicProperty`](https://developer.apple.com/documentation/swiftui/dynamicproperty), [`Sendable`](https://developer.apple.com/documentation/Swift/Sendable)

<hr class="relationship">

## 같이보기

### 앱 전체에 모델 데이터 배포

[`func environmentObject<T>(T) -> some View`](https://developer.apple.com/documentation/swiftui/view/environmentobject(_:))
	뷰의 계층 구조에 관찰 가능한 개체를 제공합니다.

[`func environmentObject<T>(T) -> some Scene`](https://developer.apple.com/documentation/swiftui/scene/environmentobject(_:))
	뷰 하위 계층 구조에 ObservableObject를 제공합니다.