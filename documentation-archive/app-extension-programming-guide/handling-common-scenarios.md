
> 출처
> [https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/ExtensionScenarios.html#//apple_ref/doc/uid/TP40014214-CH21-SW1](https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/ExtensionScenarios.html#//apple_ref/doc/uid/TP40014214-CH21-SW1)
# Handling Common Scenarios

<hr class="overview">

앱 확장 프로그램 작업을 수행하는 사용자 지정 코드를 작성할 때, 많은 유형의 익스텐션에 공통적인 몇 가지 시나리오를 처리해야 할 수도 있습니다. 이 장의 코드와 권장 사항을 사용하여 솔루션을 구현하는 데 도움이 됩니다.

## 공유 코드에 임베디드 프레임워크 사용하기 <a id="Using an Embedded Framework to Share Code"></a>

앱 확장 프로그램과 포함 앱 간에 코드를 공유하기 위해 임베디드 프레임워크를 만들 수 있습니다. 예를 들어, 사진 편집 확장 및 포함 앱에 사용할 이미지 필터를 개발하는 경우, 필터 코드를 프레임워크에 넣고 프레임워크를 두 대상 모두에 삽입합니다.

일부 API는 앱 확장 프로그램에서 사용할 수 없음에 설명된 대로 임베디드 프레임워크에 [앱 확장 프로그램에 사용할 수 없는 API](https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/ExtensionOverview.html#//apple_ref/doc/uid/TP40014214-CH2-SW6)가 포함되어 있지 않은지 확인하십시오. 이러한 API를 포함하는 사용자 지정 프레임워크가 있는 경우, 포함된 앱에서 안전하게 연결할 수 있지만 해당 코드를 앱의 포함된 확장과 공유할 수는 없습니다. 앱 스토어는 그러한 프레임워크에 연결되거나 사용할 수 없는 API를 사용하는 모든 앱 확장 프로그램을 거부합니다.

임베디드 프레임워크를 사용하도록 앱 확장 프로그램을 구성하려면 대상의 "Require Only App-Extension-Safe API" 빌드 설정을 예로 설정하십시오. 그렇지 않은 경우, Xcode는 "dylib에 대한 링크는 애플리케이션 확장에서 사용하기에 안전하지 않습니다"라는 경고를 표시하여 그렇게 하도록 상기시켜줍니다.

{% hint style="info" %}
**중요** 임베디드 프레임워크에 연결되는 포함 앱은 arm64(iOS) 또는 x86_64(OS X) 아키텍처 빌드 설정을 포함해야 합니다. 그렇지 않으면 App Store에서 거부됩니다. ([Creating an App Extension](documentation-archive/app-extension-programming-guide/creating-an-app-extension.md)에 설명된 바와 같이, 모든 앱 확장에는 적절한 64비트 아키텍처 빌드 설정이 포함되어야 합니다.)
{% endhint %}

Xcode 프로젝트를 구성할 때, 파일 복사 빌드 단계에서 임베디드 프레임워크의 대상으로 "프레임워크"를 선택해야 합니다.

{% hint style="info" %}
**중요**
항상 복사 파일 빌드 단계 대상으로 "프레임워크"를 선택하십시오. 대신 "공유 프레임워크" 대상을 선택하면, 앱 스토어는 당신의 제출을 거부할 것입니다.
{% endhint %}

iOS 7 또는 이전 버전을 실행하는 사용자에게 포함된 앱을 사용할 수 있도록 만들 수 있지만, iOS 8 이상에서 실행할 때 임베디드 프레임워크를 안전하게 연결하기 위한 예방 조치를 취해야 합니다. 자세한 내용은 [iOS의 이전 버전에 포함 앱 배포](https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/ExtensionScenarios.html#//apple_ref/doc/uid/TP40014214-CH21-SW3)를 읽으십시오.

임베디드 프레임워크를 만들고 사용하는 방법에 대한 자세한 내용은 https://developer.apple.com/videos/wwdc/2014에서 볼 수 있는 WWDC 2014 비디오 "현대 프레임워크 구축"을 시청하세요.

## 컨테이너 앱 간 데이터 공유하기 <a id="Sharing Data with Your Containing App"></a>

앱 확장 번들이 포함된 앱의 번들 안에 중첩되어 있더라도, 실행 중인 앱 확장과 포함된 앱은 서로의 컨테이너에 직접 접근할 수 없습니다.

{% hint style="info" %}
**배경지식** 컨테이너에 대해 알아보려면, [파일 시스템 프로그래밍 가이드](https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40010672)에서 [iOS 파일 시스템](https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/FileSystemOverview/FileSystemOverview.html#//apple_ref/doc/uid/TP40010672-CH2-SW12)를 읽어보세요.
{% endhint %}

그러나 데이터 공유를 활성화할 수 있습니다. 예를 들어, 앱 확장과 그 포함 앱이 미리 렌더링된 자산과 같은 하나의 큰 데이터 세트를 공유하도록 허용하고 싶을 수도 있습니다.

데이터 공유를 활성화하려면 Xcode 또는 개발자 포털을 사용하여 포함된 앱 및 포함된 앱 확장에 대한 앱 그룹을 활성화하십시오. 다음으로, 포털에 앱 그룹을 등록하고 포함 앱에 사용할 앱 그룹을 지정하십시오. 앱 그룹 작업에 대해 알아보려면 [앱 그룹에 앱 추가](https://developer.apple.com/library/archive/documentation/Miscellaneous/Reference/EntitlementKeyReference/Chapters/EnablingAppSandbox.html#//apple_ref/doc/uid/TP40011195-CH4-SW19)를 참조하십시오.

앱 그룹을 활성화한 후, 앱 확장과 그 포함 앱은 모두 [NSUserDefaults](https://developer.apple.com/library/archive/documentation/LegacyTechnologies/WebObjects/WebObjects_3.5/Reference/Frameworks/ObjC/Foundation/Classes/NSUserDefaults/Description.html#//apple_ref/occ/cl/NSUserDefaults) API를 사용하여 사용자 기본 설정에 대한 액세스를 공유할 수 있습니다. 이 공유를 활성화하려면 [initWithSuiteName:]([initWithSuiteName:](https://developer.apple.com/documentation/foundation/userdefaults/1409957-init)) 메서드를 사용하여 공유 그룹의 식별자를 전달하여 새로운 `NSUserDefaults` 개체를 인스턴스화하십시오. 예를 들어, 공유 확장은 다음과 같은 코드를 사용하여 사용자가 가장 최근에 사용한 공유 계정을 업데이트할 수 있습니다.


```objc
// Create and share access to an NSUserDefaults object
NSUserDefaults *mySharedDefaults = [[NSUserDefaults alloc] initWithSuiteName: @"com.example.domain.MyShareExtension"];`

// Use the shared user defaults object to update the user's account`
[mySharedDefaults setObject:theAccountName forKey:@"lastAccountName"];`
```

```swift
let mySharedDefaults = UserDefaults.init(suiteName: "com.example.domain.MyShareExtension")
mySharedDefaults.set(value: theAccountName, forKey: "lastAccountName")
```

그림 4-1은 확장과 그 포함 앱이 공유 컨테이너를 사용하여 데이터를 공유하는 방법을 보여줍니다.

**그림 4-1** 앱 확장의 컨테이너는 포함된 앱의 컨테이너와 구별됩니다.
<div align="center">
<img src = https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/Art/app_extensions_container_restrictions_2x.png width="500" height="auto">
</div>

{% hint style="info" %}
**중요** 앱 확장 프로그램이 [NSURLSession](https://developer.apple.com/documentation/foundation/urlsession) 클래스를 사용하여 백그라운드 업로드 또는 다운로드를 수행하는 경우 공유 컨테이너를 설정해야 확장 프로그램과 포함된 앱 모두 전송된 데이터에 액세스할 수 있습니다. 백그라운드에서 업로드 또는 다운로드를 수행하는 방법을 배우려면 [업로드 및 다운로드 수행](https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/ExtensionScenarios.html#//apple_ref/doc/uid/TP40014214-CH21-SW2)을 참조하십시오.
{% endhint %}

공유 컨테이너를 설정할 때, 포함된 앱과 데이터 공유에 참여할 수 있는 각 포함된 앱 확장은 공유 컨테이너에 대한 읽기 및 쓰기 액세스 권한을 가집니다. 데이터 손상을 피하기 위해, 당신은 데이터 액세스를 동기화해야 합니다.

공유 컨테이너에서 데이터 액세스를 조정하는 데 도움이 되도록 코어 데이터, SQLite 또는 Posix 잠금 장치를 사용하십시오.

## 웹페이지 접근하기 <a id="Accessing a Webpage"></a>

## 업로드 그리고 다운로드 수행하기

## 공유 혹은 액션 확장 프로그램을 위한 지원 데이터 유형 선언하기

공유 또는 작업 확장에서 일부 유형의 데이터는 작업할 수 있지만 다른 데이터는 작업할 수 없습니다. 사용자가 지원하는 유형의 데이터를 선택한 경우에만 호스트 앱이 확장을 제공하도록 하려면 확장의 Info.plist 속성 목록 파일에 NSExtensionActivationRule 키를 추가하십시오. 또한 이 키를 사용하여 확장이 처리할 수 있는 각 유형의 최대 항목 수를 지정할 수 있습니다.

확장이 실행되면 시스템은 NSExtensionActivationRule 키의 값을 확장 항목의 첨부 속성의 정보와 비교합니다. 이 키와 함께 사용할 수 있는 키의 전체 목록은 액션 확장 키를 참조하십시오.

예를 들어, 공유 확장이 최대 10개의 이미지, 하나의 영화 및 하나의 웹 페이지 URL을 지원할 수 있다고 선언하려면 NSExtensionAttributes 키 값에 대해 다음 사전을 사용할 수 있습니다.

```xml
<key>NSExtensionAttributes</key>
    <dict>
        <key>NSExtensionActivationRule</key>
    <dict>
        <key>NSExtensionActivationSupportsImageWithMaxCount</key>
        <integer>10</integer>
        <key>NSExtensionActivationSupportsMovieWithMaxCount</key>
        <integer>1</integer>
        <key>NSExtensionActivationSupportsWebURLWithMaxCount</key>
        <integer>1</integer>
    </dict>
</dict>
```

특정 데이터 유형을 지원하지 않는 경우, 해당 키의 값에 0을 사용하거나 NSExtensionActivationRule 사전에서 키를 제거하십시오.

{% hint style="info" %}
**메모** 공유 또는 iOS 액션 확장 프로그램이 웹 페이지에 액세스해야 하는 경우, 0이 아닌 값으로 `NSExtensionActivationSupportsWebPageWithMaxCount` 키를 포함해야 합니다. (자바스크립트를 사용하여 확장 프로그램에서 웹 페이지에 액세스하는 방법을 배우려면  <a href="#Accessing a Webpage">웹 페이지 액세스 접근하기</a>를 참조하십시오.)
{% endhint %}

`NSExtensionActivationRule` 사전의 키는 일반적인 앱 확장의 필터링 요구를 충족시키기에 충분합니다. `public.url`과 `public.image`를 구별하는 것과 같이 더 복잡하거나 더 구체적인 필터링을 해야 하는 경우, 술어문을 만들 수 있습니다. 그런 다음, `NSExtensionActivationRule` 키의 값으로 술어를 나타내는 맨 문자열을 사용하십시오. (런타임에, 시스템은 이 문자열을 [NSPredicate](https://developer.apple.com/documentation/foundation/nspredicate) 객체로 컴파일합니다.)

예를 들어, 앱 확장 항목의 첨부 속성은 다음과 같은 PDF 파일을 지정할 수 있습니다.
```objc
{extensionItems = ({
    attachments = ({
        registeredTypeIdentifiers = (
            "com.adobe.pdf",
            "public.file-url"
        );
    });
})}
```

앱 확장이 정확히 하나의 PDF 파일을 처리할 수 있도록 지정하려면 다음과 같은 술어 문자열을 만들 수 있습니다.

```objc
SUBQUERY (
    extensionItems,
    $extensionItem,
    SUBQUERY (
        $extensionItem.attachments,
        $attachment,
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.adobe.pdf"
    @count == $extensionItem.attachments.@count
).@count == 1
```

다음은 더 복잡한 술어 문장의 예입니다:

```objc
SUBQUERY (
    extensionItems,
    $extensionItem,
    SUBQUERY (
        $extensionItem.attachments,
        $attachment,
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "org.appextension.action-one" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "org.appextension.action-two"
    ).@count == $extensionItem.attachments.@count
).@count == 1
```

이 문은 [NSExtensionItem](https://developer.apple.com/documentation/foundation/nsextensionitem) 개체의 배열을 반복하고, 각 확장 항목의 [attachment](https://developer.apple.com/documentation/foundation/nsextensionitem/1416690-attachments) 배열을 두 번째로 반복합니다. 각 첨부 파일에 대해, 술어는 첨부 파일의 각 표현에 대한 균일한 유형 식별자(UTI)를 평가합니다. 첨부 표현 UTI가 두 개의 서로 다른 지정된 UTI(각 `UTI-CONFORMS-TO` 연산자의 오른쪽에 볼 수 있음) 중 하나를 준수하는 경우, 최종 비교 테스트를 위해 해당 UTI를 수집합니다. 앱 확장에 지원되는 UTI와 함께 정확히 하나의 확장 항목 첨부 파일이 제공된 경우 마지막 줄은 `TRUE`를 반환합니다.

개발 중에만 `TRUEPREDICATE` 상수(항상 `true`로 평가됨)를 스텁 술어 문으로 사용하여 술어 문을 구현하기 전에 코드 경로를 테스트할 수 있습니다.


{% hint style="info" %}
**중요** 앱 스토어에 포함된 앱을 제출하기 전에 `TRUEPREDICATE` 스텁 술어의 모든 사용을 기능 술어 문 또는 `NSExtensionActivationRule` 키로 교체해야 합니다. 포함된 앱의 앱 확장이 `TRUEPREDICATE` 문자열을 포함하는 경우, 해당 앱은 거부됩니다.
{% endhint %}

술어문 구문에 대해 자세히 알아보려면, [술어 프로그래밍 가이드](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Predicates/AdditionalChapters/Introduction.html#//apple_ref/doc/uid/TP40001789)의 [술어 형식 문자열 구문](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Predicates/Articles/pSyntax.html#//apple_ref/doc/uid/TP40001795)을 참조하십시오.
## ### Deploying a Containing App to Older Versions of iOS