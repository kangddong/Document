# 컬렉션

배열, 사전, 세트 및 기타 데이터 구조를 사용하여 데이터를 저장하고 구성하십시오.

## 주제 <a id="topics"></a>

## 배열과 사전

[`struct Array`](app-frameworks/swift/swift-standard-library/collections/array.md)
	정렬된, 무작위 접근 컬렉션.

[`struct Dictionary`](https://developer.apple.com/documentation/swift/dictionary)
	요소가 키-값 쌍인 컬렉션.

### 세트
[`struct Set`](https://developer.apple.com/documentation/swift/set)
	독특한 요소들의 순서가 없는 컬렉션.

[`protocol OptionSet`](app-frameworks/swift/swift-standard-library/collections/optionset.md)
	비트 세트에 대한 수학적 집합 인터페이스를 제시하는 유형.

## 범위
반열린(..<) 및 닫힌(...) 범위 연산자를 사용하여 범위의 모든 값 모음을 만듭니다.

[`static func ..< (Self, Self) -> Range<Self>`](https://developer.apple.com/documentation/swift/comparable/'.._(_:_:))
	하한선은 포함하지만 상한선은 포함하지 않는 반개방 범위를 반환합니다.

[`struct Range`](https://developer.apple.com/documentation/swift/range)
	하한에서 상한까지, 그러나 상한을 포함하지 않는 반 개방 간격.

[`struct RangeSet`](https://developer.apple.com/documentation/swift/rangeset)
	 범위로 표현되는 모든 비교 가능한 유형의 값 집합.

[`static func ... (Self, Self) -> ClosedRange<Self>`](https://developer.apple.com/documentation/swift/comparable/'...(_:_:))
	두 경계를 모두 포함하는 닫힌 범위를 반환합니다.

[`struct ClosedRange`](https://developer.apple.com/documentation/swift/closedrange)
	하한에서 상한까지, 그리고 상한까지의 간격.

### 보폭

stride(from:to:by:) 및 stride(from:through:by:) 함수를 사용하여 두 경계 사이의 값을 밟는 보폭을 만듭니다.

[`func stride<T>(from: T, to: T, by: T.Stride) -> StrideTo<T>`](https://developer.apple.com/documentation/swift/stride(from:to:by:))
	시작 값에서 종료 값으로의 시퀀스를 반환하지만, 지정된 양으로 단계별로 정렬합니다.

[`func stride<T>(from: T, through: T, by: T.Stride) -> StrideThrough<T>`](https://developer.apple.com/documentation/swift/stride(from:through:by:))
	시작 값에서 지정된 양에 따라 단계별로 종료 값으로, 그리고 아마도 다음을 포함하는 시퀀스를 반환합니다.

### 특수 사용 컬렉션
이러한 컬렉션은 동일한 요소를 0개, 1개 또는 여러 개 저장할 수 있습니다.
[`func repeatElement<T>(T, count: Int) -> Repeated<T>`](https://developer.apple.com/documentation/swift/repeatelement(_:count:))
	주어진 요소의 지정된 수를 포함하는 컬렉션을 만듭니다.

[`struct CollectionOfOne`](https://developer.apple.com/documentation/swift/collectionofone)
	단일 요소를 포함하는 컬렉션.

[`struct EmptyCollection`](https://developer.apple.com/documentation/swift/emptycollection)
	요소 유형이 요소이지만 항상 비어 있는 컬렉션.

[`struct KeyValuePairs`](https://developer.apple.com/documentation/swift/keyvaluepairs)
	키-값 쌍의 경량 컬렉션.

[`typealias DictionaryLiteral`](https://developer.apple.com/documentation/swift/dictionaryliteral)

### [Dynamic Sequences](https://developer.apple.com/documentation/swift/collections#Dynamic-Sequences)

[`func sequence<T>(first: T, next: (T) -> T?) -> UnfoldFirstSequence<T>`](https://developer.apple.com/documentation/swift/sequence(first:next:))
	Returns a sequence formed from `first` and repeated lazy applications of `next`.

[`func sequence<T, State>(state: State, next: (inout State) -> T?) -> UnfoldSequence<T, State>`](https://developer.apple.com/documentation/swift/sequence(state:next:))
	Returns a sequence formed from repeated lazy applications of `next` to a mutable `state`.

### [Joint Iteration](https://developer.apple.com/documentation/swift/collections#Joint-Iteration)

[`func zip<Sequence1, Sequence2>(Sequence1, Sequence2) -> Zip2Sequence<Sequence1, Sequence2>`](https://developer.apple.com/documentation/swift/zip(_:_:))
	Creates a sequence of pairs built out of two underlying sequences.

### [Advanced Collection Topics](https://developer.apple.com/documentation/swift/collections#Advanced-Collection-Topics)

[Sequence and Collection Protocols](https://developer.apple.com/documentation/swift/sequence-and-collection-protocols)
	Write generic code that works with any collection, or build your own collection types.

[Supporting Types](https://developer.apple.com/documentation/swift/supporting-types)
	Use wrappers, indices, and iterators in operations like slicing, flattening, and reversing a collection.

[Managed Buffers](https://developer.apple.com/documentation/swift/managed-buffers)
	Build your own buffer-backed collection types.

## [See Also](https://developer.apple.com/documentation/swift/collections#see-also)

### [Values and Collections](https://developer.apple.com/documentation/swift/collections#Values-and-Collections)

[Numbers and Basic Values](https://developer.apple.com/documentation/swift/numbers-and-basic-values)
	Model data with numbers, Boolean values, and other fundamental types.

[Strings and Text](https://developer.apple.com/documentation/swift/strings-and-text)
	Work with text using Unicode-safe strings.

[Time](https://developer.apple.com/documentation/swift/time-and-duration)
	Measure how long an operation takes and determine schedules in the future.