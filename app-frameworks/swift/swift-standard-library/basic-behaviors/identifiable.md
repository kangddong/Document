
> 출처
> [https://developer.apple.com/documentation/swift/identifiable](https://developer.apple.com/documentation/swift/identifiable)
# Identifiable
인스턴스가 안정적인 정체성을 가진 엔티티의 값을 보유하는 유형의 클래스.

```swift
protocol Identifiable<ID>
```

<hr class="overview">

## 개요 <a id="overview"></a>

Identifiable 프로토콜을 사용하여 클래스 또는 값 유형에 대한 안정적인 정체성 개념을 제공합니다. 예를 들어, 앱과 앱의 데이터베이스 저장소에 걸쳐 안정적인 id 속성으로 사용자 유형을 정의할 수 있습니다. 사용자 이름과 같은 다른 데이터 필드가 변경되더라도 특정 사용자를 식별하기 위해 id 속성을 사용할 수 있습니다.

Identifiable은 신원의 기간과 범위를 지정하지 않습니다. 정체성은 다음과 같은 특징 중 하나를 가질 수 있다:

- UUID와 같이 항상 고유하게 보장됩니다.
- 데이터베이스 레코드 키와 같이 환경마다 지속적으로 고유합니다.
- 전역 증분 정수와 같은 프로세스의 수명에 대해 고유합니다.
- 개체 식별자와 같은 개체의 수명에 대해 고유합니다.
- 컬렉션 지수와 같은 현재 컬렉션 내에서 고유합니다.

신원의 특성을 문서화하는 것은 프로토콜의 준수자와 수신자 모두에게 달려 있습니다.

## Identifiable 프로토콜 준수하기

Identifiable은 클래스 유형(ObjectIdentifier 사용)에 대한 기본 구현을 제공하며, 이는 객체의 수명 동안만 고유하게 유지되도록 보장됩니다. 객체가 정체성에 대한 더 강력한 개념을 가지고 있다면, 사용자 지정 구현을 제공하는 것이 적절할 수 있습니다.


<hr class="topics">

## 주제 <a id="topics"></a>

### 연관 타입 지정하기
[associatedtype ID : Hashable]()
	인스턴스와 연관된 엔티티의 안정적인 정체성을 나타내는 유형.
	**필수**
### 식별되는 아이템 지정하기
[var id: Self.ID]()
	이 인스턴스와 관련된 엔티티의 안정적인 정체성.
	**필수** 기본 구현 제공됨.

<hr class="relationships">

## 연관 관계 <a id="relationships"></a>

### 상속 받는 관계
[DistributedActor](https://developer.apple.com/documentation/distributed/distributedactor)

### 채택한 타입
[Never](https://developer.apple.com/documentation/swift/never)

<hr class="see-also">

## 같이 보기 <a id="see-also"></a>\

동등성과 순서
protocol Equatable
protocol Comparable