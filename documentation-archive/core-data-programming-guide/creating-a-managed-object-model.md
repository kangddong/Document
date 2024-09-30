
> 출처
> [https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/KeyConcepts.html#//apple_ref/doc/uid/TP40001075-CH30-SW12](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/KeyConcepts.html#//apple_ref/doc/uid/TP40001075-CH30-SW12)


코어 데이터의 기능의 대부분은 애플리케이션의 엔티티, 속성 및 그들 사이의 관계를 설명하기 위해 생성한 스키마에 달려 있습니다. Core Data는 [NSManagedObjectModel]()의 인스턴스인 관리 대상 모델이라고 불리는 스키마를 사용합니다. 일반적으로, 모델이 풍부할수록, 더 나은 코어 데이터가 당신의 애플리케이션을 지원할 수 있습니다.

관리되는 객체 모델을 통해 Core Data는 영구 저장소의 레코드에서 애플리케이션에서 사용하는 관리되는 객체로 매핑할 수 있습니다. 이 모델은 엔티티 설명 개체([NSEntityDescription]()의 인스턴스)의 모음입니다. 엔티티 설명은 엔티티(데이터베이스의 테이블이라고 생각할 수 있음)를 이름, 애플리케이션에서 엔티티를 나타내는 데 사용되는 클래스 이름, 그리고 어떤 속성(속성 및 관계)을 가지고 있는지에 대해 설명합니다.

### 엔티티 생성과 속성 <a id="Creating an Entity and Its Properties"></a>

Xcode에서 새 프로젝트를 시작하고 템플릿 선택 대화 상자를 열면 핵심 데이터 사용 확인란을 선택합니다. 코어 데이터 모델의 소스 파일이 템플릿의 일부로 생성됩니다. 그 소스 파일은 확장자가 `.xcdatamodeld`일 것이다. 네비게이터 영역에서 해당 파일을 선택하여 핵심 데이터 모델 편집기를 표시합니다.

**엔티티 생성하기** <a id="To create an entity"></a>

1. Add Entity 클릭.
    네비게이터 영역의 엔티티 목록에 제목 없는 새로운 엔티티가 나타납니다.
2. 제목 없는 새로운 엔티티 선택하기.
3. 데이터 모델 인스펙터의 엔티티 창에서 엔티티 이름을 입력하고 리턴을 누릅니다.

**엔터티의 속성 및 관계를 만들기** <a id="To create attributes and relationships for the entity**"></a>

1. 새 엔티티를 선택한 상태에서, 해당 섹션 하단의 추가 버튼(+)을 클릭하십시오..
    새로운 제목 없는 속성 또는 관계(일반적으로 속성이라고 함)가 편집기 영역의 속성 또는 관계 섹션에 추가됩니다.
2. 새로운 제목 없는 속성을 선택하세요.
    속성 설정은 데이터 모델 속성의 관계 창 또는 속성 창에 표시됩니다.
3. 속성에 이름을 지정하고, Return을 누르세요.
    속성 또는 관계 정보가 편집기 영역에 나타납니다.

[Employee entity in the Xcode Data Model editor](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/KeyConcepts.html#//apple_ref/doc/uid/TP40001075-CH30-SW5) 직원을 설명하는 생년월일, 이름 및 시작 날짜. 속성과 함께 직원이라는 엔티티를 보여줍니다

**그림 2-1**  Xcode 데이터 모델 편집기 내 Employee 엔티티

<div align="center">
<img src = https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/Art/Model_Editor_2x.png width="500" height="auto">
</div>


이 시점에서 당신은 모델에 엔티티를 생성했지만, 어떠한 데이터도 생성하지 않았습니다. 데이터는 나중에 애플리케이션을 실행할 때 생성됩니다. 이러한 엔티티는 관리 대상체([NSManagedObject]() 인스턴스) 생성의 기초로 귀하의 애플리케이션에서 사용됩니다.

### 엔티티 정의하기 <a id="Defining an Entity"></a>

이제 엔티티의 이름을 지정했으니, 데이터 모델 인스펙터의 엔티티 창에서 더 정의합니다. [Entity pane in the Data Model inspector](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/KeyConcepts.html#//apple_ref/doc/uid/TP40001075-CH30-SW3) 보기

**그림 2-2**Entity pane in the Data Model inspector

<div align="center">
<img src = https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/Art/Entity_Inspector_2x.png width="250" height="auto">
</div>

### 엔티티 이름과 클래스 이름 <a id="Entity Name and Class Name"></a>

엔티티 이름과 클래스 이름([NSManagedObject]()의 하위 클래스)은 동일하지 않다는 점에 유의하십시오. 데이터 모델의 엔티티 구조는 클래스 계층 구조와 일치할 필요가 없습니다. 그림 2-2는 MO 접미사와 함께 Objective-C의 권장 클래스 이름 패턴이 있는 클래스 이름을 보여줍니다. 엔티티 이름과 클래스 이름이 필요합니다.

### 추상 엔티티 <a id="Abstract Entities"></a>

해당 엔티티의 인스턴스를 생성하지 않을 경우 엔티티가 추상적이라고 지정하십시오. 그 자체로 인스턴스화되어서는 안 되는 공통 엔티티의 전문화(상승)를 나타내는 다수의 엔티티가 있는 경우 일반적으로 엔티티를 추상화합니다. 예를 들어, 직원 엔티티에서 Person을 추상 엔티티로 정의하고 구체적인 하위 엔티티(직원 및 고객)만 인스턴스화할 수 있도록 지정할 수 있습니다. 데이터 모델 인스펙터의 엔티티 창에서 엔티티를 추상으로 표시함으로써, 코어 데이터에 직접 인스턴스화되지 않을 것임을 알리는 것입니다.

### 엔티티 상속 <a id="Entity Inheritance"></a>

엔티티 상속은 클래스 상속과 유사한 방식으로 작동하며, 같은 이유로 유용합니다. 유사한 엔티티가 여러 개 있는 경우, 공통 속성을 상위 엔티티라고도 알려진 슈퍼 엔티티로 인수분해할 수 있습니다. 여러 엔티티에서 동일한 속성을 지정하는 대신, 하나의 엔티티에서 정의할 수 있으며, 하위 엔티티는 이를 상속합니다. 예를 들어, 이름과 성 속성으로 개인 엔티티를 정의할 수 있으며, 이러한 속성을 상속하는 하위 엔티티 직원과 고객을 정의할 수 있습니다. 이 레이아웃의 예는 그림 2-3에 나와 있습니다. 오른쪽 하단 모서리에 있는 편집기 스타일 버튼을 클릭하여 레이아웃 다이어그램을 표시합니다.

많은 경우, 하위 엔티티를 나타내는 클래스가 상속하는 엔티티에 해당하는 사용자 지정 클래스를 구현합니다. 모든 엔티티에 공통적인 비즈니스 로직을 여러 번 구현하는 대신, 한 곳에서 구현하면 하위 클래스에 의해 상속됩니다.

{% hint style="info" %} 노트

SQLite 영구 저장소로 작업할 때 엔티티 상속에 주의하십시오. 다른 엔티티로부터 상속받은 모든 엔티티는 SQLite의 동일한 테이블 내에 존재합니다. SQLite 영구 저장소 설계의 이러한 요소는 성능 문제를 일으킬 수 있습니다.

{% endhint %}

**그림 2-3** 엔티티 상속 다이어그램

<div align="center">
<img src = https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/Art/Entity_Inheritence_2_2x.png width="500" height="auto">
</div>


### 속성 관계 정의하기 <a id="Defining Attributes and Relationships"></a>

엔티티의 속성은 가져온 속성(있는 경우)을 포함하여 속성과 관계입니다. 다른 특징들 중에서도, 각 속성에는 이름과 유형이 있습니다. 속성 이름은 [NSObject]() 또는 `NSManagedObject`의 매개 변수 없는 메서드 이름과 같을 수 없습니다. 예를 들어, 속성에 "설명"이라는 이름을 부여할 수 없습니다([NSPropertyDescription]() 참조).

일시적인 속성은 모델의 일부로 정의하지만 엔티티 인스턴스 데이터의 일부로 영구 저장소에 저장되지 않는 속성입니다. 코어 데이터는 일시적인 속성에 대한 변경 사항을 추적하므로 실행 취소 작업을 위해 기록됩니다. 계산된 값과 파생된 값을 유지하는 것을 포함하여 다양한 목적으로 일시적인 속성을 사용합니다.



{% hint style="info" %} 노트

모델링되지 않은 정보를 사용하는 임시 속성에 대한 변경을 취소하는 경우, Core Data는 이전 값으로 설정된 액세스 권한을 호출하지 않고 스냅샷 정보를 업데이트합니다.

{% endhint %}

**그림 2-4** 데이터 모델 인스펙터 내 속성 패널 <a id="Attribute pane in the Data Model inspector"></a>
<div align="center">
<img src = https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/Art/Attribute_Inspector_2x.png width="300" height="auto">
</div>

### 속성 <a id="Attributes"></a>

속성을 정의하려면, 핵심 데이터 모델 편집기에서 선택하고 핵심 데이터 모델 속성의 속성 창에서 값을 지정하십시오; <a href="#Attribute pane in the Data Model inspector">데이터 모델 인스펙터 내 속성 패널</a>을 참조하십시오. Core Data는 기본적으로 문자열, 날짜 및 정수(각각 [NSString](), [NSDate]() 및 [NSNumber]()의 인스턴스로 표시됨)와 같은 다양한 속성 유형을 지원합니다.

속성이 선택 사항이라고 지정할 수 있습니다. 즉, 값을 가질 필요는 없습니다. 그러나 일반적으로, 특히 숫자 값의 경우, 그렇게 하지 마십시오. 일반적으로 속성에 정의된 기본값이 0인 필수 속성을 사용하면 더 나은 결과를 얻을 수 있습니다. 그 이유는 SQL이 Objective-C의 `nil`과 달리 `NULL`에 대한 특별한 비교 동작을 가지고 있기 때문입니다. 데이터베이스의 `NULL`은 0과 동일하지 않으며, 0에 대한 검색은 `NULL` 열과 일치하지 않습니다. 게다가, 데이터베이스의 `NULL`은 빈 문자열이나 빈 데이터 블롭과 동일하지 않다.

### 관계 and Fetched Properties <a id="Relationships and Fetched Properties"></a>

관계를 정의하려면, 핵심 데이터 모델 편집기에서 선택하고, 데이터 모델 속성의 관계 창에서 값을 지정하십시오. <a href="#Relationship in the Data Model inspector">데이터 모델 인스펙터 내 관계 패널</a>

**그림 2-5** 데이터 모델 인스펙터 내 관계 패널 <a id="Relationship in the Data Model inspector"></a>

<div align="center">
<img src = https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/Art/Relationship_Inspector_2x.png width="300" height="auto">
</div>


Core Data는 일대일 및 일대다 관계, 그리고 가져온 속성을 지원합니다. Fetched 속성은 약한 일방통행 관계를 나타냅니다. 직원 및 부서 영역에서, 부서의 가져온 속성은 "최근 고용"일 수 있습니다(직원은 최근 고용 관계와 반대가 없습니다).

유형 팝업 메뉴는 관계가 일대일 유형 관계인지 또는 일대다 유형 관계인지를 정의합니다. 관계는 한 번에 한 방향에서 정의됩니다. 다대다 관계를 만들려면, 이대다 관계를 만든 다음 서로 반대로 설정해야 합니다.

대상 팝업 메뉴는 코드에서 관계에 액세스할 때 반환되는 개체(또는 개체)를 정의합니다. 관계가 일대일으로 정의된 경우, 단일 객체(또는 관계가 선택 사항인 경우 `nil`)가 반환됩니다. 관계가 일대다로 정의되면, 집합이 반환됩니다 (또는 관계가 선택 사항일 수 있는 경우 다시 `nil`).

인버스 팝업 메뉴는 관계의 나머지 절반을 정의합니다. 각 관계는 한 방향에서 정의되기 때문에, 이 팝업 메뉴는 두 관계를 함께 결합하여 완전한 양방향 관계를 만듭니다.

[Creating Managed Object Relationships](documentation-archive/core-data-programming-guide/creating-managed-object-relationships.md)에 관계는 더 자세히 설명되어 있습니다.