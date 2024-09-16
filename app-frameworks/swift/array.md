
> 출처
> [https://developer.apple.com/documentation/swift/array](https://developer.apple.com/documentation/swift/array)


# Array
정렬된, 무작위 접근 컬렉션.

```swift
@frozen
struct Array<Element>
```

<hr class="overview">
## 개요 <a id="overview"></a>

배열은 앱에서 가장 일반적으로 사용되는 데이터 유형 중 하나입니다. 배열을 사용하여 앱의 데이터를 구성합니다. 특히, 배열 유형을 사용하여 배열의 요소 유형인 단일 유형의 요소를 보유합니다. 배열은 정수에서 문자열, 클래스에 이르기까지 모든 종류의 요소를 저장할 수 있습니다.

Swift는 배열 리터럴을 사용하여 코드에 배열을 쉽게 만들 수 있습니다: 쉼표로 구분된 값 목록을 대괄호로 둘러싸기만 하면 됩니다. 다른 정보 없이 Swift는 지정된 값을 포함하는 배열을 생성하여 배열의 요소 유형을 자동으로 추론합니다. 예를 들면:

```swift
// 'Int' 요소의 배열
let oddNumbers = [1, 3, 5, 7, 9, 11, 13, 15]

// 'String' 요소의 배열
let streets = ["Albemarle", "Brandywine", "Chesapeake"]
```

선언에서 배열의 요소 유형을 지정하여 빈 배열을 만들 수 있습니다. 예를 들면:

```swift
// 단축된 양식이 선호된다
var emptyDoubles: [Double] = []

// 전체 유형 이름도 허용됩니다
var emptyFloats: Array<Float> = Array()
```

고정된 수의 기본값으로 미리 초기화된 배열이 필요한 경우, Array(repeating:count:) 이니셜라이저를 사용하십시오.

```swift
var digitCounts = Array(repeating: 0, count: 10)
print(digitCounts)
// 출력 "[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]"
```

# 배열 값들에 접근 <a id="accessing-array-values"></a>

배열의 모든 요소에 대한 작업을 수행해야 하는 경우, for-in 루프를 사용하여 배열의 내용을 반복합니다.

```swift
for street in streets {
    print("I don't live on \(street).")
}
// 출력 "I don't live on Albemarle."
// 출력 "I don't live on Brandywine."
// 출력 "I don't live on Chesapeake."
```

isEmpty 속성을 사용하여 배열에 요소가 있는지 빠르게 확인하거나 count 속성을 사용하여 배열의 요소 수를 찾으십시오.

```swift
if oddNumbers.isEmpty {
    print("I don't know any odd numbers.")
} else {
	print("I know \(oddNumbers.count) odd numbers.")
}
// 출력 "I know 8 odd numbers."
```

배열의 첫 번째와 마지막 요소의 값에 안전하게 접근하기 위해 첫 번째와 마지막 속성을 사용하십시오. 배열이 비어 있으면, 이 속성들은 nil입니다.

```swift
if let firstElement = oddNumbers.first, let lastElement = oddNumbers.last {
	print(firstElement, lastElement, separator: ", ")
}
// 출력 "1, 15"

print(emptyDoubles.first, emptyDoubles.last, separator: ", ")
// 출력 "nil, nil"
```

서브 스크립트를 통해 개별 배열 요소에 액세스할 수 있습니다. 비어 있지 않은 배열의 첫 번째 요소는 항상 인덱스 0에 있습니다. 배열의 개수를 포함하지 않는 0부터 정수로 배열에 서브 스크립트를 할 수 있습니다. 음수 또는 카운트보다 크거나 같은 인덱스를 사용하면 런타임 오류가 발생합니다. 예를 들면:

```swift
print(oddNumbers[0], oddNumbers[3], separator: ", ")
// 출력 "1, 7"

print(emptyDoubles[0])
// 런타임 에러 트리거: Index 의 범위를 벗어남
```

# 요소들 추가와 삭제 <a id="adding-and-removing-elements"></a>





## 배열의 크기 증가 <a id="growing-the-size-of-an-array"></a>

# 배열의 복사본 수정 <a id="modifying-copies-of-arrays"></a>

Each array has an independent value that includes the values of all of its elements. For simple types su

# Array 와 NSArray 사이 브릿징 <a id="bridging--between-array-and-nsarray"></a>

When you need to access APIs that require data in an `NSArray`instance instead of `Array`, use