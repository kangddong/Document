> 출처
> [https://developer.apple.com/documentation/combine/observableobject](https://developer.apple.com/documentation/combine/observableobject)

# ObservableObject
객체가 변경되기 전에 방출되는 게시자가 있는 객체 유형.
```swift
protocol ObservableObject : AnyObject
```

<hr class="header">

## 개요

기본적으로 ObservableObject는 @Published 속성이 변경되기 전에 변경된 값을 방출하는 [objectWillChange](https://developer.apple.com/documentation/combine/observableobject/objectwillchange) 게시자를 합성합니다.

```swift
class Contact: ObservableObject {
    @Published var name: String
    @Published var age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }

    func haveBirthday() -> Int {
        age += 1
        return age
    }
}

let john = Contact(name: "John Appleseed", age: 24)
cancellable = john.objectWillChange
    .sink { _ in
        print("\\(john.age) will change")
}
print(john.haveBirthday())
// Prints "24 will change"
// Prints "25"
```


<hr class="overview">

## 주제

### 변경 방출하기
[`var objectWillChange: Self.ObjectWillChangePublisher`](https://developer.apple.com/documentation/combine/observableobject/objectwillchange)
	객체가 변경되기 전에 발행하는 게시자.
	**필수** 기본 구현 제공됨. 

[`associatedtype ObjectWillChangePublisher : Publisher= ObservableObjectPublisher`](https://developer.apple.com/documentation/combine/observableobject/objectwillchangepublisher)
	객체가 변경되기 전에 방출되는 게시자의 유형.
	**필수**

<hr class="topics">

## 같이보기

### 관찰 가능한 객체

[`class ObservableObjectPublisher`](https://developer.apple.com/documentation/combine/observableobjectpublisher)
	관찰 가능한 개체의 변경 사항을 게시하는 게시자.