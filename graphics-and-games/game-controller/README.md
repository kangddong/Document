
> 출처
> [https://developer.apple.com/documentation/gamecontroller/gccontroller](https://developer.apple.com/documentation/gamecontroller/gccontroller)
# Game Controller
게임에서 하드웨어 게임 컨트롤러를 지원하세요.

<hr class="overview">

## 개요 <a id="overview"></a>

게임 컨트롤러를 사용하여 물리적 또는 가상 게임 컨트롤러를 사용하여 앱과 상호 작용하는 사용자를 지원하십시오. 게임 컨트롤러에는 듀얼쇼크 4, 듀얼센스, 엑스박스와 같은 타사 제품과 마우스, 키보드, 시리 리모컨 및 레이싱 휠이 포함됩니다.


<div align="center">
<img src = https://docs-assets.developer.apple.com/published/fb79d6d9a6/renderedDark2x-1660837369.png width="500" height="auto">
</div>


게임 컨트롤러를 지원하려면 게임 컨트롤러 기능([GCSupportsControllerUserInteraction](https://developer.apple.com/documentation/bundleresources/information_property_list/gcsupportscontrolleruserinteraction) 속성)을 프로젝트에 추가하면 Xcode는 게임 컨트롤러 프레임워크를 자동으로 추가합니다. 
그런 다음, 서명 및 기능 창의 게임 컨트롤러 기능에서 앱이 지원하는 컨트롤러 유형([GCSupportedGameControllers](https://developer.apple.com/documentation/bundleresources/information_property_list/gcsupportedgamecontrollers) 속성)을 선택하십시오.

레이싱 휠 이외의 컨트롤러의 경우, 앱에서 게임 컨트롤러 입력을 처리하려면 다음 단계를 따르세요:

- 물리적 게임 컨트롤러 객체를 얻으려면, 사용자가 게임 컨트롤러를 연결하고 연결을 끊을 때 특정 알림을 등록하십시오. 
  또는, 사용자가 상호 작용할 수 있는 가상 컨트롤러를 표시할 수 있습니다.

- 그런 다음 물리적 또는 가상 컨트롤러에서 프로필 개체를 가져와 버튼, 트리거, 썸스틱 및 방향 패드와 같은 입력 요소에 액세스하십시오. 
  프로필은 앱에서 컨트롤러의 입력 요소의 하드웨어 세부 사항과 레이아웃을 캡슐화합니다.

- 입력을 처리하려면, 요소에서 직접 값을 가져오거나 사용자가 값을 변경할 때 콜백을 등록하십시오.
  visionOS에서 실행되는 앱은 그 사람이 앱의 창을 보고 있을 때만 입력 이벤트를 받습니다.

- 햅틱을 지원하는 컨트롤러의 경우, 컨트롤러의 액추에이터를 조작하는 엔진을 만들어 사용자에게 피드백을 제공할 수 있습니다.

사용자는 설정 및 환경 설정에서 게임 컨트롤러 요소를 다시 매핑할 수 있으므로 인터페이스에 올바른 입력 요소를 표시해야 합니다. [hasRemappedElements](https://developer.apple.com/documentation/gamecontroller/gcphysicalinputprofile/3867057-hasremappedelements) 속성이 참이면,
사용자는 요소를 다시 매핑하고 [mappedElementAlias(forPhysicalInputName:)](https://developer.apple.com/documentation/gamecontroller/gcphysicalinputprofile/3867058-mappedelementalias) 및 [mappedPhysicalInputNames(forElementAlias:)](https://developer.apple.com/documentation/gamecontroller/gcphysicalinputprofile/3867059-mappedphysicalinputnames) 메서드를 사용하여 실제 요소와 별칭 요소 간의 매핑을 얻을 수 있습니다.

macOS 앱에서 레이싱 휠 장치를 지원하려면, [Racing wheel device support](https://developer.apple.com/documentation/gamecontroller/racing_wheel_device_support) 을 참조하십시오.

<hr class="topics">

## 주제 <a id="topics"></a>

### Essentials <a id="essentials"></a>


<hr class="see-also">

## 같이 보기 <a id="see-also"></a>

### [관련된 문서](https://developer.apple.com/documentation/gamecontroller#related-documentation)

[Game Controller Programming Guide](https://developer.apple.com/library/archive/documentation/ServicesDiscovery/Conceptual/GameControllerPG/Introduction/Introduction.html#//apple_ref/doc/uid/TP40013276)