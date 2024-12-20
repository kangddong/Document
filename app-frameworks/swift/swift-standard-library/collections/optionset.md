
> 출처
> [https://developer.apple.com/documentation/swift/optionset](https://developer.apple.com/documentation/swift/optionset)

# OptionSet
비트 세트에 대한 수학적 집합 인터페이스를 제시하는 유형.

```swift
protocol OptionSet : RawRepresentable, SetAlgebra
```

<hr class="overview">

## 개요 <a id="overview"></a>

OptionSet 프로토콜을 사용하여 개별 비트가 집합의 구성원을 나타내는 비트셋 유형을 나타냅니다. 사용자 지정 유형에 이 프로토콜을 채택하면 멤버십 테스트, 조합 및 해당 유형에 대한 교차점과 같은 집합 관련 작업을 수행할 수 있습니다. 더욱이, 특정 기준을 사용하여 구현될 때, 이 프로토콜의 채택은 추가 작업이 필요하지 않습니다.

옵션 세트를 만들 때, 유형 선언에 rawValue 속성을 포함시키세요. 귀하의 유형이 집합 관련 작업에 대한 기본 구현을 자동으로 수신하려면 rawValue 속성이 Int 또는 UInt8과 같이 FixedWidthInteger 프로토콜을 준수하는 유형이어야 합니다. 다음으로, 각 속성이 유형의 원시 값의 단일 비트로 표현될 수 있도록 각 속성이 각 속성의 원시 값에 대해 두 개의 고유한 거듭제곱(1, 2, 4, 8, 16 등)을 사용하여 사용자 지정 유형의 정적 속성으로 고유한 옵션을 만듭니다.

예를 들어, 고객의 구매를 배송할 수 있는 가능한 방법의 옵션 집합인 ShippingOptions라는 사용자 지정 유형을 고려하십시오. ShippingOptions는 사용 가능한 배송 옵션의 비트 마스크를 저장하는 Int 유형의 rawValue 속성을 포함합니다. 정적 멤버 nextDay, secondDay, priority 및 standard는 독특하고 개별적인 옵션입니다.

```swift
struct ShippingOptions: OptionSet {
    let rawValue: Int
    
    static let nextDay = ShippingOptions(rawValue: 1 << 0)
    static let secondDay = ShippingOptions(rawValue: 1 << 1)
    static let priority = ShippingOptions(rawValue: 1 << 2)
    static let standard = ShippingOptions(rawValue: 1 << 3)
    static let express: ShippingOptions = [.nextDay, .secondDay]
    static let all: ShippingOptions = [.express, .priority, .standard]
}
```

추가 사전 구성된 옵션 세트 값을 다른 옵션 값을 포함하는 배열 리터럴로 초기화된 정적 속성으로 선언합니다. 예에서, express static 속성은 nextDay 및 secondDay 옵션이 있는 배열 리터럴을 할당받았기 때문에, 이 두 요소를 포함할 것이다.

# 옵션 세트 유형 사용법

옵션 세트의 인스턴스를 생성해야 할 때, 유형의 정적 멤버 중 하나를 변수 또는 상수에 할당하십시오. 또는 여러 멤버가 있는 옵션 세트 인스턴스를 만들려면 옵션 세트의 여러 정적 멤버가 있는 배열 리터럴을 할당하십시오. 빈 인스턴스를 생성하려면, 변수에 빈 배열 리터럴을 할당하십시오.

```swift
let singleOption: ShippingOptions = .priority
let multipleOptions: ShippingOptions = [.nextDay, .secondDay, .priority]
let noOptions: ShippingOptions = []
```

집합 관련 작업을 사용하여 멤버십을 확인하고 사용자 지정 옵션 세트 유형의 인스턴스에서 회원을 추가하거나 제거하십시오. 다음 예는 고객의 구매 가격에 따라 무료 배송 옵션을 결정하는 방법을 보여줍니다.

```swift
let purchasePrice = 87.55

var freeOptions: ShippingOptions = []
if purchasePrice > 50 {
    freeOptions.insert(.priority)
}

if freeOptions.contains(.priority) {
    print("You've earned free priority shipping!")
} else {
    print("Add more to your cart for free priority shipping!")
} // 출력 "You've earned free priority shipping!"
```


<hr class="topics">

## 주제 <a id="topics"></a>

<hr class="relationships">

## 연관 관계 <a id="relationships"></a>
### 상속 받음
- [`Equatable`](https://developer.apple.com/documentation/swift/equatable)
- [`ExpressibleByArrayLiteral`](https://developer.apple.com/documentation/swift/expressiblebyarrayliteral)
- [`RawRepresentable`](https://developer.apple.com/documentation/swift/rawrepresentable)
- [`SetAlgebra`](https://developer.apple.com/documentation/swift/setalgebra)

<hr class="see-also">

## 같이 보기 <a id="see-also"></a>

### 세트

[`struct Set`](https://developer.apple.com/documentation/swift/set)
	독특한 요소들의 순서가 없는 컬렉션.