> 출처
> [https://developer.apple.com/documentation/uikit/app-and-environment](https://developer.apple.com/documentation/uikit/app-and-environment)

# 앱과 환경
라이프 사이클 이벤트와 앱의 UI 장면을 관리하고, 앱이 실행되는 특성과 환경에 대한 정보를 얻으십시오.

<hr class="header">
## 개요
iOS 13 이상에서는 한 사람이 앱 사용자 인터페이스의 여러 인스턴스를 동시에 생성 및 관리할 수 있으며, 앱 전환기를 사용하여 둘 사이를 전환할 수 있습니다. 아이패드에서, 사람은 또한 당신의 앱의 여러 인스턴스를 나란히 표시할 수 있습니다. UI의 각 인스턴스는 다른 콘텐츠를 표시하거나 동일한 콘텐츠를 다른 방식으로 표시합니다. 예를 들어, 한 사람은 특정 날짜를 보여주는 캘린더 앱의 인스턴스 하나를 표시하고, 전체 달을 보여주는 다른 인스턴스를 표시할 수 있습니다.

UIKit은 장치 설정, 인터페이스 설정 및 사용자 선호도의 조합을 반영하는 특성 컬렉션을 사용하여 현재 환경에 대한 세부 정보를 전달합니다. 예를 들어, 특성을 사용하여 현재 뷰 또는 뷰 컨트롤러에 대해 다크 모드가 활성화되어 있는지 여부를 감지합니다. 현재 환경을 기반으로 콘텐츠를 사용자 지정하려면 [UIView](https://developer.apple.com/documentation/uikit/uiview) 또는 [UIViewController](https://developer.apple.com/documentation/uikit/uiviewcontroller) 개체의 현재 특성 컬렉션을 참조하십시오. 특성 알림 변경을 수신하도록 할 때 다른 개체에서 [UITraitEnvironment](https://developer.apple.com/documentation/uikit/uitraitenvironment) 프로토콜을 채택하십시오.

<hr class="overview">

## 주제

### 라이프 사이클
[Managing your app’s life cycle](https://developer.apple.com/documentation/uikit/managing-your-app-s-life-cycle)
  앱이 포그라운드 또는 백그라운드에 있을 때 시스템 알림에 응답하고, 다른 중요한 시스템 관련 이벤트를 처리하세요.

[Responding to the launch of your app](https://developer.apple.com/documentation/uikit/responding-to-the-launch-of-your-app)
  앱의 데이터 구조를 초기화하고, 앱을 실행할 준비를 하고, 시스템의 실행 시간 요청에 응답합니다.

[`class UIApplication`](https://developer.apple.com/documentation/uikit/uiapplication)
	iOS에서 실행되는 앱을 위한 중앙 집중식 제어 및 조정 지점.

[`protocol UIApplicationDelegate`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate)
	앱의 공유 동작을 관리하는 일련의 방법.

[Scenes](https://developer.apple.com/documentation/uikit/scenes)
  앱 UI의 여러 인스턴스를 동시에 관리하고, 리소스를 UI의 적절한 인스턴스로 보냅니다.
### 기기 환경
[`class UIDevice`](https://developer.apple.com/documentation/uikit/uidevice)
	현재 장치의 표현.

[`class UIStatusBarManager`](https://developer.apple.com/documentation/uikit/uistatusbarmanager)
	상태 표시줄의 구성을 설명하는 개체.

### 적응성
[Automatic trait tracking](https://developer.apple.com/documentation/uikit/automatic-trait-tracking)
	자동 특성 추적을 지원하는 방법 또는 폐쇄 내에서 특성을 사용할 때 특성 변경에 대해 수동으로 등록할 필요성을 줄입니다.

[Responding to changing display modes on Apple TV](https://developer.apple.com/documentation/uikit/responding-to-changing-display-modes-on-apple-tv)
	장치의 화면 영역이 변경되면 이미지와 리소스를 동적으로 변경하십시오.

[`class UITraitCollection`](https://developer.apple.com/documentation/uikit/uitraitcollection)
	앱의 사용자 인터페이스에서 개별 요소에 대한 환경을 나타내는 데이터 모음.

[`protocol UITraitEnvironment`](https://developer.apple.com/documentation/uikit/uitraitenvironment)
	iOS 인터페이스 환경을 앱에서 사용할 수 있게 하는 일련의 방법.

[`protocol UITraitChangeObservable`](https://developer.apple.com/documentation/uikit/uitraitchangeobservable-67e94)
	특성 환경의 변화에 반응하여 코드를 호출하는 유형.

[`protocol UIMutableTraits`](https://developer.apple.com/documentation/uikit/uimutabletraits-13ja5)
	형질의 변할 수 있는 용기.

[`protocol UIAdaptivePresentationControllerDelegate`](https://developer.apple.com/documentation/uikit/uiadaptivepresentationcontrollerdelegate)
	프레젠테이션 컨트롤러와 함께 앱의 특성 변경에 대응하는 방법을 결정하는 일련의 방법.

[`protocol UIContentContainer`](https://developer.apple.com/documentation/uikit/uicontentcontainer)
	뷰 컨트롤러의 내용을 크기와 특성 변경에 맞게 조정하는 일련의 방법.

### 커스텀 특성

[`protocol UIMutableTraits`](https://developer.apple.com/documentation/uikit/uimutabletraits-13ja5)
	형질의 변할 수 있는 용기.

[`typealias UITrait`](https://developer.apple.com/documentation/uikit/uitrait-9423)
	특성 컬렉션에서 특성을 나타내는 유형.

[`protocol UITraitDefinition`](https://developer.apple.com/documentation/uikit/uitraitdefinition-64c15)
	특성 컬렉션에서 특성을 나타내는 유형.

### 아이패드
[Building a desktop-class iPad app](https://developer.apple.com/documentation/uikit/building-a-desktop-class-ipad-app)

iPadOS 16에서 스테이지 매니저, 문서 상호 작용, 텍스트 편집, 검색 등을 통한 멀티태스킹을 위한 데스크톱 수준의 개선 사항을 채택하여 iPad 앱의 사용자 경험을 최적화하십시오.

[Elevating your iPad app with a tab bar and sidebar](https://developer.apple.com/documentation/uikit/elevating-your-ipad-app-with-a-tab-bar-and-sidebar)
앱의 주요 부분에 빠르게 접근할 수 있는 작고 인체공학적인 탭 바와 심층 탐색을 위한 사이드바를 제공하십시오.

[Supporting desktop-class features in your iPad app](https://developer.apple.com/documentation/uikit/supporting-desktop-class-features-in-your-ipad-app)
데스크톱급 기능과 문서 지원을 추가하여 iPad 앱을 향상시키세요.

[Multitasking on iPad](https://developer.apple.com/documentation/uikit/multitasking-on-ipad)
멀티태스킹 API를 구현하여 앱을 iPadOS와 원활하게 통합하십시오.


### 가이드 접근
[`protocol UIGuidedAccessRestrictionDelegate`](https://developer.apple.com/documentation/uikit/uiguidedaccessrestrictiondelegate)
	iOS의 가이드 액세스 기능에 대한 사용자 지정 제한을 추가하는 데 사용하는 일련의 방법.

[`static func guidedAccessRestrictionState(forIdentifier: String) -> UIAccessibility.GuidedAccessRestrictionState`](https://developer.apple.com/documentation/uikit/uiaccessibility/guidedaccessrestrictionstate(foridentifier:))
	지정된 안내 액세스 제한에 대한 제한 상태를 반환합니다.

### 아키텍처
[Updating your app from 32-bit to 64-bit architecture](https://developer.apple.com/documentation/uikit/updating-your-app-from-32-bit-to-64-bit-architecture)
최신 버전의 운영 체제를 지원하도록 적용하여 앱이 예상대로 작동하는지 확인하십시오.

[`func UIApplicationMain(Int32, UnsafeMutablePointer<UnsafeMutablePointer<CChar>?>, String?, String?) -> Int32`](https://developer.apple.com/documentation/uikit/uiapplicationmain(_:_:_:_:)-1yub7)
	애플리케이션 객체와 애플리케이션 위임을 생성하고 이벤트 주기를 설정합니다.


## 같이보기

[Documents, data, and pasteboard](https://developer.apple.com/documentation/uikit/documents-data-and-pasteboard)
앱의 데이터를 정리하고 클립보드에서 그 데이터를 공유하세요.

[Resource management](https://developer.apple.com/documentation/uikit/resource-management)
앱 인터페이스를 구현하는 데 사용하는 이미지, 문자열, 스토리보드 및 펜촉 파일을 관리하십시오.

[App extensions](https://developer.apple.com/documentation/uikit/app-extensions)
앱의 기본 기능을 시스템의 다른 부분으로 확장하십시오.

[Interprocess communication](https://developer.apple.com/documentation/uikit/interprocess-communication)
사람들에게 활동 기반 서비스를 표시하세요.

[Mac Catalyst](https://developer.apple.com/documentation/uikit/mac-catalyst)
사용자가 Mac 기기에서 실행할 수 있는 iPad 앱 버전을 만드십시오.