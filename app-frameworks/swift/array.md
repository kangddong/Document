
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

당신이 가르치고 있는 수업에 등록한 학생들의 이름 목록을 저장해야 한다고 가정해 봅시다. 등록 기간 동안, 학생들이 수업을 추가하고 삭제할 때 이름을 추가하고 제거해야 합니다.

```swift
var students = ["Ben", "Ivy", "Jordell"]
```

배열 끝에 단일 요소를 추가하려면 `append(_:)` 메서드를 사용하십시오. 다른 배열이나 어떤 종류의 시퀀스를 `append(contentsOf:)` 메서드에 전달하여 동시에 여러 요소를 추가하십시오.


```swift
students.append("Maxime")
students.append(contentsOf: ["Shakia", "William"])
// ["Ben", "Ivy", "Jordell", "Maxime", "Shakia", "William"]
```

단일 요소에 대해 `insert(_:at:)` 메서드를 사용하고 `insert(contentsOf:at:)`를 사용하여 다른 컬렉션 또는 배열 리터럴에서 여러 요소를 삽입하여 배열 중간에 새로운 요소를 추가할 수 있습니다. 그 인덱스와 이후의 인덱스의 요소들은 공간을 만들기 위해 뒤로 이동된다.

```swift
students.insert("Liam", at: 3)
// ["Ben", "Ivy", "Jordell", "Liam", "Maxime", "Shakia", "William"]
```

배열에서 요소를 제거하려면 `remove(at:)`, `removeSubrange(_:)` 및 `removeLast()` 메서드를 사용하십시오.

```swift
// Ben's family is moving to another state
students.remove(at: 0)
// ["Ivy", "Jordell", "Liam", "Maxime", "Shakia", "William"]
// William is signing up for a different class
students.removeLast()
// ["Ivy", "Jordell", "Liam", "Maxime", "Shakia"]
```

서브 스크립트에 새 값을 할당하여 기존 요소를 새 값으로 바꿀 수 있습니다.

```swift
if let i = students.firstIndex(of: "Maxime") {
    students[i] = "Max"
}
// ["Ivy", "Jordell", "Liam", "Max", "Shakia"]
```

## 배열의 크기 증가 <a id="growing-the-size-of-an-array"></a>

모든 배열은 그 내용을 담을 특정 양의 메모리를 보유합니다. 배열에 요소를 추가하고 그 배열이 예약된 용량을 초과하기 시작하면, 배열은 더 큰 메모리 영역을 할당하고 그 요소를 새로운 저장소에 복사합니다. 새 저장소는 이전 저장소 크기의 배수입니다. 이 기하급수적 성장 전략은 요소를 추가하는 것이 일정한 시간에 발생하여 많은 추가 작업의 성능을 평균화한다는 것을 의미합니다. 재할당을 트리거하는 추가 작업은 성능 비용이 있지만, 배열이 커질수록 점점 덜 자주 발생합니다.

대략 몇 개의 요소를 저장해야 하는지 알고 있다면, 중간 재할당을 피하기 위해 배열에 추가하기 전에 `reserveCapacity(_:)` 메서드를 사용하십시오. 용량과 카운트 속성을 사용하여 더 큰 저장 공간을 할당하지 않고 배열이 저장할 수 있는 요소 수를 결정하십시오.

대부분의 요소 유형의 배열에 대해, 이 저장소는 연속된 메모리 블록입니다. 클래스 또는 @objc 프로토콜 유형인 요소 유형을 가진 배열의 경우, 이 저장소는 연속된 메모리 블록 또는 NSArray의 인스턴스가 될 수 있습니다. NSArray의 임의의 하위 클래스는 배열이 될 수 있기 때문에, 이 경우 표현이나 효율성에 대한 보장은 없습니다.

# 배열의 복사본 수정 <a id="modifying-copies-of-arrays"></a>

각 배열에는 모든 요소의 값을 포함하는 독립적인 값이 있습니다. 정수 및 기타 구조와 같은 간단한 유형의 경우, 이는 한 배열에서 값을 변경할 때 해당 요소의 값이 배열의 사본에서 변경되지 않는다는 것을 의미합니다. 예를 들면:

```swift
var numbers = [1, 2, 3, 4, 5]
var numbersCopy = numbers
numbers[0] = 100
print(numbers)
// 출력 "[100, 2, 3, 4, 5]"
print(numbersCopy)
// 출력 "[1, 2, 3, 4, 5]"
```

배열의 요소가 클래스의 인스턴스인 경우, 처음에는 다르게 보일 수 있지만 의미론은 동일합니다. 이 경우, 배열에 저장된 값은 배열 외부에 있는 개체에 대한 참조입니다. 한 배열에서 개체에 대한 참조를 변경하면 해당 배열에만 새 개체에 대한 참조가 있습니다. 그러나 두 개의 배열에 동일한 개체에 대한 참조가 포함된 경우 두 배열 모두에서 해당 개체의 속성에 대한 변경 사항을 관찰할 수 있습니다. 예를 들면:

```swift
// 참조 의미론이 있는 정수 타입
class IntegerReference {
    var value = 10
}
var firstIntegers = [IntegerReference(), IntegerReference()]
var secondIntegers = firstIntegers

// 인스턴스에 대한 수정 사항은 두 배열 모두에서 볼 수 있습니다
firstIntegers[0].value = 100
print(secondIntegers[0].value)
// 출력 "100"

// 교체, 추가 및 제거가 여전히 보입니다
// 수정된 배열에서만
firstIntegers[0] = IntegerReference()
print(firstIntegers[0].value)
// 출력 "10"
print(secondIntegers[0].value)
// 출력 "100"
```

표준 라이브러리의 모든 가변 크기 컬렉션과 마찬가지로 배열은 복사 시 쓰기 최적화(copy-on-wirte)를 사용합니다. 배열의 여러 복사본은 복사본 중 하나를 수정할 때까지 동일한 저장소를 공유합니다. 그런 일이 발생하면, 수정되는 배열은 그 저장소를 고유하게 소유한 복사본으로 대체하고, 그 다음 그 자리에 수정됩니다. 복사량을 줄일 수 있는 최적화가 때때로 적용됩니다.

이는 배열이 다른 복사본과 스토리지를 공유하는 경우 해당 배열의 첫 번째 `mutating` 작업이 배열을 복사하는 비용이 발생한다는 것을 의미합니다. 저장소의 유일한 소유자인 배열은 그 자리에서 `mutating` 작업을 수행할 수 있습니다.

아래의 예에서, 숫자 배열은 동일한 저장소를 공유하는 두 개의 복사본과 함께 생성됩니다. 원본 숫자 배열이 수정되면 수정하기 전에 저장소의 고유한 복사본을 만듭니다. 두 사본이 원본 저장소를 계속 공유하는 동안 숫자에 대한 추가 수정이 이루어집니다.

```swift
var numbers = [1, 2, 3, 4, 5]
var firstCopy = numbers
var secondCopy = numbers

// 'numbers'를 위한 저장소는 여기에 복사됩니다
numbers[0] = 100
numbers[1] = 200
numbers[2] = 300
// 'numbers' 는 [100, 200, 300, 4, 5]
// 'firstCopy' 와 'secondCopy' 는 [1, 2, 3, 4, 5]
```
# Array 와 NSArray 사이 브릿징 <a id="bridging--between-array-and-nsarray"></a>

Array 대신 NSArray 인스턴스에서 데이터가 필요한 API에 액세스해야 하는 경우, type-cast 연산자(as)를 사용하여 인스턴스를 브릿지하십시오. 브릿징이 가능하려면 배열의 요소 유형이 클래스, @objc 프로토콜(Objective-C에서 가져오거나 @objc 속성으로 표시된 프로토콜) 또는 파운데이션 유형으로 브리지하는 유형이어야 합니다.

다음 예제는 write(to:atomically:) 메서드를 사용하기 위해 Array 인스턴스를 NSArray에 브릿징하는 방법을 보여줍니다. 이 예에서 색상 배열의 문자열 요소가 NSString으로 브릿지되기 때문에 색상 배열이 NSArray로 브릿지될 수 있습니다. 반면에 컴파일러는 moreColors 배열의 브릿징을 방지합니다. 왜냐하면 그 요소 유형은 Foundation 유형으로 브릿지되지 않는 `Optional<String>`이기 때문입니다.

```swift
let colors = ["periwinkle", "rose", "moss"]
let moreColors: [String?] = ["ochre", "pine"]

let url = URL(fileURLWithPath: "names.plist")
(colors as NSArray).write(to: url, atomically: true)
// true
(moreColors as NSArray).write(to: url, atomically: true)
// error: cannot convert value of type '[String?]' to type 'NSArray'
```

배열에서 NSArray로 연결하는 것은 배열의 요소가 이미 클래스 또는 @objc 프로토콜의 인스턴스인 경우 O(1) 시간과 O(1) 공간이 필요합니다; 그렇지 않으면 O(n) 시간과 공간이 필요합니다.

대상 배열의 요소 유형이 클래스 또는 @objc 프로토콜인 경우, NSArray에서 Array로 연결하는 것은 먼저 배열에서 copy(with:) (- copyWithZone: in Objective-C) 메서드를 호출하여 불변 복사본을 얻은 다음 O(1) 시간이 걸리는 추가 Swift 부기 작업을 수행합니다. 이미 불변인 NSArray 인스턴스의 경우, copy(with:)는 일반적으로 O(1) 시간에 동일한 배열을 반환합니다; 그렇지 않으면 복사 성능이 지정되지 않습니다. Copy(with:)가 동일한 배열을 반환하는 경우, NSArray 및 Array의 인스턴스는 두 개의 Array 인스턴스가 스토리지를 공유할 때 사용되는 동일한 copy-on-write 최적화를 사용하여 스토리지를 공유합니다.

대상 배열의 요소 유형이 파운데이션 유형으로 브릿지되는 비클래스 유형인 경우, NSArray에서 Array로의 브리징은 O(n) 시간 동안 연속 저장소에 대한 요소의 브릿징 복사본을 수행합니다. 예를 들어, NSArray에서 `Array<Int>`로의 브릿징은 그러한 복사를 수행합니다. 배열 인스턴스의 요소에 액세스할 때 더 이상의 브릿징이 필요하지 않습니다.

{% hint style="info" %} 노트

ContiguousArray 및 ArraySlice 유형은 브릿지되지 않습니다; 이러한 유형의 인스턴스는 항상 스토리지로 연된 메모리 블록을 가지고 있습니다. {% endhint %}

<hr class="topics">

## 주제 <a id="topics"></a>

<hr class="relationships">
## 연관 관계 <a id="relationships"></a>

<hr class="see-also">
## 같이 보기 <a id="see-also"></a>