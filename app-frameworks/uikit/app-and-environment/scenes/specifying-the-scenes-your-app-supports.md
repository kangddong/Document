> 출처
> [https://developer.apple.com/documentation/uikit/specifying-the-scenes-your-app-supports](https://developer.apple.com/documentation/uikit/specifying-the-scenes-your-app-supports)

# 앱이 지원하는 장면 지정하기

각 장면을 관리하는 데 사용하는 객체와 초기 사용자 인터페이스를 포함하여 앱의 장면에 대해 시스템에 알려주십시오.

<hr class="header">
## 개요

iOS 13 이상에서 사용자는 앱 UI의 여러 복사본을 만들고 앱 전환기에서 그 사이를 전환할 수 있습니다. 아이패드에서 사용자는 앱 UI의 복사본을 다른 복사본과 나란히 표시할 수도 있습니다. 앱 UI의 각 복사본에 대해 장면 객체를 사용하여 화면에 UI를 표시하는 창, 뷰 및 뷰 컨트롤러를 관리합니다.

사용자가 새로운 장면을 요청할 때, UIKit은 해당 장면 객체를 생성하고 초기 설정을 처리합니다. 그렇게 하기 위해, UIKit은 당신이 제공하는 정보에 의존합니다. 앱은 지원하는 장면 유형과 해당 장면을 관리하는 데 사용하는 개체를 선언해야 합니다. 앱의 Info.plist 파일에서 정적으로 또는 런타임에 동적으로 수행할 수 있습니다.

{% hint style="warning" %}
**중요**
장면은 옵트인이지만, 앱 UI의 여러 복사본을 동시에 표시하려면 해당 장면을 지원해야 합니다.
{% endhint %}

### 프로젝트 세팅에서 장면 지원 활성화

앱은 앱의 구성 설정을 업데이트하여 장면에 명시적으로 선택해야 합니다.

1. Xcode 프로젝트를 여세요.
2. 앱 타겟의 General 설정으로 이동합니다.
3. 배포 정보 섹션에서 "Supports multiple windows" 체크박스를 활성화하십시오.

다중 창 옵션을 활성화하면 Xcode가 앱의 Info.plist 파일에 [UIApplicationSceneManifest](https://developer.apple.com/documentation/bundleresources/information_property_list/uiapplicationscenemanifest) 키를 추가합니다. 이 키의 존재는 당신의 앱이 장면을 지원한다는 것을 시스템에 알려줍니다. 이 키의 값은 사전이며, 처음에는 [UIApplicationSupportsMultipleScenes](https://developer.apple.com/documentation/BundleResources/Information-Property-List/UIApplicationSceneManifest/UIApplicationSupportsMultipleScenes) 키만 포함합니다.

[UIApplicationSupportsMultipleScenes](https://developer.apple.com/documentation/BundleResources/Information-Property-List/UIApplicationSceneManifest/UIApplicationSupportsMultipleScenes) 키의 값은 시스템이 당신의 앱이 실제로 여러 동시 장면을 지원하는지 여부를 알려줍니다. Xcode는 처음에 이 키의 값을 true로 설정하지만, 한 번에 하나의 장면만 표시하려면 기능을 비활성화할 수 있습니다. 여러 장면을 지원하려면 장면이 서로 간섭하지 않도록 추가 작업이 필요합니다. 예를 들어, 당신의 장면이 동일한 공유 데이터 구조를 사용하는 경우, 앱 데이터의 무결성을 유지하기 위해 해당 구조에 대한 액세스를 조정해야 합니다.

### 각 장면에 대한 세부사항 구성하기 <a name="scene_supprot" />

UIKit은 귀하가 제공하는 정보를 사용하여 앱의 장면 생성을 처리합니다. 이 정보를 제공하는 가장 간단한 방법은 앱의 Info.plist 파일에 있습니다:

1. Xcode 프로젝트를 열고 Info.plist 파일을 선택하세요.

2. 애플리케이션 장면 매니페스트 항목의 더하기(+) 버튼을 클릭하세요. 이 항목은 [UIApplicationSceneManifest](https://developer.apple.com/documentation/bundleresources/information_property_list/uiapplicationscenemanifest) 키에 해당합니다. 존재하지 않는 경우, <a href="scene_supprot">프로젝트 세팅에서 장면 지원 활성화</a>에 설명된 대로 추가하십시오.

3. 나타나는 메뉴에서, Scene Configuration을 선택하세요.

4. Scene Configuration 항목에서 더하기(+) 버튼을 클릭하십시오.

5. Application Session Role을 선택하여 앱에 메인 장면을 추가하세요.

6. 제공된 항목에 장면 세부 사항을 입력하십시오.

대부분의 앱은 하나의 메인 장면만 필요하지만, 여러 장면을 추가하고 각각 다르게 구성할 수 있습니다. 예를 들어, 알림 관련 콘텐츠를 표시하기 위해 특별히 두 번째 장면을 포함할 수 있습니다. UIKit은 각 장면에 대해 다음과 같은 정보를 요구합니다:

- [UIWindowScene](https://developer.apple.com/documentation/uikit/uiwindowscene)인 장면의 클래스 이름.

- 당신의 앱이 장면을 관리하는 데 사용하는 사용자 지정 위임 개체의 클래스 이름. 클래스는 [UIWindowSceneDelegate](https://developer.apple.com/documentation/uikit/uiwindowscenedelegate) 프로토콜을 채택해야 합니다.

- 당신의 앱이 내부적으로 장면을 식별하기 위해 사용하는 고유한 이름.

- 장면의 초기 UI를 포함하는 스토리보드의 이름. .storyboard 파일 이름 확장자 없이 이름을 지정하십시오.

장면을 구성하는 방법에 대한 자세한 내용은 [UISceneConfigurations](https://developer.apple.com/documentation/bundleresources/information_property_list/uiapplicationscenemanifest/uisceneconfigurations)를 참조하십시오.

### 장면을 위한 인터페이스 생성하기

스토리보드를 사용하여 장면의 UI를 지정합니다. [UISceneStoryboardFile](https://developer.apple.com/documentation/BundleResources/Information-Property-List/UIApplicationSceneManifest/UISceneConfigurations/UIWindowSceneSessionRoleApplication/UISceneStoryboardFile) 키에 할당한 스토리보드에는 장면에 표시하려는 초기 뷰 컨트롤러가 포함되어 있습니다. UIKit은 장면 객체를 만드는 것 외에도 장면에 대한 창을 자동으로 생성하고 스토리보드에서 초기 뷰 컨트롤러를 설치합니다. [UIWindowSceneDelegate](https://developer.apple.com/documentation/uikit/uiwindowscenedelegate) 객체의 방법을 사용하여 프로그래밍 방식으로 해당 뷰 컨트롤러를 교체할 수 있습니다.

{% hint style="warning" %}
**중요**
스토리보드에서 초기 뷰 컨트롤러를 지정하는 것을 잊지 마세요. UIKit은 UI를 구성할 때 이 뷰 컨트롤러의 존재에 의존합니다.
{% endhint %}

### 장면의 구성 동적으로 변경하기

실제로 장면 개체를 만들기 전에 UIKit은 앱 위임의 [`application(_:configurationForConnecting:options:)`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/application(_:configurationforconnecting:options:)) 메서드를 호출하여 장면 관련 세부 사항을 변경할 수 있도록 합니다. 이 방법을 사용하여 UIKit이 제공하는 옵션에 따라 장면 구성을 조정할 수 있습니다. 예를 들어, 시스템이 당신의 장면에 알림 응답을 전달할 때, 당신은 알림 관련 인터페이스로 다른 스토리보드를 지정할 수 있습니다.

동적으로 장면을 구성하지 않는 경우 UIKit은 앱의 Info.plist 파일에 있는 정보를 사용하여 장면을 만듭니다.

### 장면 기반 수명 주기 의미론 채택

장면에 대한 지원을 추가하면 앱이 라이프 사이클 이벤트에 반응하는 방식이 변경됩니다. 장면이 없는 앱에서, 앱 위임 객체는 전경 또는 배경으로의 전환을 처리합니다. 앱에 장면 지원을 추가하면 UIKit이 그 책임을 장면 위임 개체로 옮깁니다. 장면 수명 주기는 서로 독립적이며 앱 자체와 독립적이므로 장면 위임 개체가 전환을 처리해야 합니다.

앱이 iOS 12도 지원하는 경우, 앱 위임 및 장면 위임 개체 모두에서 수명 주기 전환을 처리할 수 있습니다. UIKit은 하나의 위임 개체만 알립니다. iOS 13 이상에서 UIKit은 장면 위임 개체를 알립니다. iOS 12 및 이전 버전에서는 UIKit이 앱 대리자에게 알립니다.

라이프 사이클 이벤트를 처리하는 방법에 대한 정보는 [앱의 라이프 사이클 관리](https://developer.apple.com/documentation/uikit/managing-your-app-s-life-cycle)를 참조하십시오.


<hr class="overview">

## 주제

### 구성

[Specifying the scenes your app supports](https://developer.apple.com/documentation/uikit/specifying-the-scenes-your-app-supports)
각 장면을 관리하는 데 사용하는 개체와 초기 사용자 인터페이스를 포함하여 앱의 장면에 대해 시스템에 알려주십시오.

[`property list key UIApplicationSceneManifest`](https://developer.apple.com/documentation/bundleresources/information_property_list/uiapplicationscenemanifest)
	앱의 장면 기반 라이프 사이클 지원에 대한 정보.

[`class UISceneConfiguration`](https://developer.apple.com/documentation/uikit/uisceneconfiguration)
	특정 장면을 만들 때 UKit이 사용할 객체 및 스토리보드에 대한 정보.

[`class UISceneSession`](https://developer.apple.com/documentation/uikit/uiscenesession)
	앱의 장면 중 하나에 대한 정보를 포함하는 객체.