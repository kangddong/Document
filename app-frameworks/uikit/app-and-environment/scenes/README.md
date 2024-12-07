> 출처
> [https://developer.apple.com/documentation/uikit/scenes](https://developer.apple.com/documentation/uikit/scenes)

# 장면
앱 UI의 여러 인스턴스를 동시에 관리하고, 리소스를 UI의 적절한 인스턴스로 보냅니다.

<hr class="header">

## 개요
UIKit은 [UIWindowScene](https://developer.apple.com/documentation/uikit/uiwindowscene) 객체를 사용하여 앱 UI의 각 인스턴스를 관리합니다. 장면에는 UI의 하나의 인스턴스를 제시하기 위한 창과 뷰 컨트롤러가 포함되어 있습니다. 각 장면에는 UIKit과 앱 간의 상호 작용을 조정하는 데 사용하는 해당 [UIWindowSceneDelegate](https://developer.apple.com/documentation/uikit/uiwindowscenedelegate) 객체가 있습니다. 장면은 서로 동시에 실행되며 동일한 메모리와 앱 프로세스 공간을 공유합니다. 결과적으로, 단일 앱에 여러 장면과 장면 위임 객체가 동시에 활성화될 수 있습니다.

<div align="center">
<img src = https://docs-assets.developer.apple.com/published/2ca9357918eb89b8fdb96cf9e324b12a/media-3335652~dark@2x.png height="500">
</div>

[UIApplicationDelegate](https://developer.apple.com/documentation/uikit/uiapplicationdelegate) 객체에서 새 장면의 구성을 관리하세요.

<hr class="overview">

## 주제

### 주요
[Preparing your UI to run in the foreground](https://developer.apple.com/documentation/uikit/preparing-your-ui-to-run-in-the-foreground)
화면에 표시되도록 앱을 구성하세요.

[Preparing your UI to run in the background](https://developer.apple.com/documentation/uikit/preparing-your-ui-to-run-in-the-background)
앱이 정지될 준비를 하세요.


### 창 장면

[Supporting multiple windows on iPad](https://developer.apple.com/documentation/uikit/supporting-multiple-windows-on-ipad)
앱 인터페이스의 나란히 인스턴스를 지원하고 새 창을 만듭니다.

[`protocol UIWindowSceneDelegate`](https://developer.apple.com/documentation/uikit/uiwindowscenedelegate)
	장면에서 발생하는 앱 특정 작업을 관리하기 위해 사용하는 추가 메서드.

[`class UIWindowScene`](https://developer.apple.com/documentation/uikit/uiwindowscene)
	앱을 위해 하나 이상의 창을 관리하는 장면.

[`class UIScene`](https://developer.apple.com/documentation/uikit/uiscene)
	앱 사용자 인터페이스의 한 인스턴스를 나타내는 객체.

[`protocol UISceneDelegate`](https://developer.apple.com/documentation/uikit/uiscenedelegate)
	장면 내에서 발생하는 수명 주기 이벤트에 대응하기 위해 사용하는 핵심 메서드.


### 구성
[Specifying the scenes your app supports](https://developer.apple.com/documentation/uikit/specifying-the-scenes-your-app-supports)
각 장면을 관리하는 데 사용하는 개체와 초기 사용자 인터페이스를 포함하여 앱의 장면에 대해 시스템에 알려주십시오.

[`property list key UIApplicationSceneManifest`](https://developer.apple.com/documentation/bundleresources/information_property_list/uiapplicationscenemanifest)
	앱의 장면 기반 라이프 사이클 지원에 대한 정보.

[`class UISceneConfiguration`](https://developer.apple.com/documentation/uikit/uisceneconfiguration)
	특정 장면을 만들 때 UKit이 사용할 객체 및 스토리보드에 대한 정보.

[`class UISceneSession`](https://developer.apple.com/documentation/uikit/uiscenesession)
	앱의 장면 중 하나에 대한 정보를 포함하는 객체.

### 활성화와 파괴

[`class UISceneActivationConditions`](https://developer.apple.com/documentation/uikit/uisceneactivationconditions)
	UIKit이 현재 장면을 활성화할 때를 정의하는 조건 집합.

[`class ActivationRequestOptions`](https://developer.apple.com/documentation/uikit/uiscene/activationrequestoptions)
	장면과 관련된 세션을 활성화할 때 시스템이 사용하기를 원하는 정보를 포함하는 객체.

[`class UIWindowSceneDestructionRequestOptions`](https://developer.apple.com/documentation/uikit/uiwindowscenedestructionrequestoptions)
	앱에서 창 장면을 제거할 때 사용할 정보를 포함하는 객체.

[`class UISceneDestructionRequestOptions`](https://developer.apple.com/documentation/uikit/uiscenedestructionrequestoptions)
	앱에서 장면과 관련 세션을 영구적으로 제거하기 위해 UIKit에 전달하는 객체.


### 에러
[`enum Code`](https://developer.apple.com/documentation/uikit/uisceneerror/code)
	장면 문제에 대한 오류 코드.

[`struct UISceneError`](https://developer.apple.com/documentation/uikit/uisceneerror)
	장면을 만들거나 관리하는 동안 반환된 오류.

[`let UISceneErrorDomain: String`](https://developer.apple.com/documentation/uikit/uisceneerrordomain)
	장면 관련 오류에 대한 도메인.

<hr class="topics">
## 같이보기

### 라이프 사이클
[Managing your app’s life cycle](https://developer.apple.com/documentation/uikit/managing-your-app-s-life-cycle)
  앱이 포그라운드 또는 백그라운드에 있을 때 시스템 알림에 응답하고, 다른 중요한 시스템 관련 이벤트를 처리하세요.

[Responding to the launch of your app](https://developer.apple.com/documentation/uikit/responding-to-the-launch-of-your-app)
  앱의 데이터 구조를 초기화하고, 앱을 실행할 준비를 하고, 시스템의 실행 시간 요청에 응답합니다.

[`class UIApplication`](https://developer.apple.com/documentation/uikit/uiapplication)
	iOS에서 실행되는 앱을 위한 중앙 집중식 제어 및 조정 지점.

[`protocol UIApplicationDelegate`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate)
	앱의 공유 동작을 관리하는 일련의 방법.