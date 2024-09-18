
> 출처
> [https://developer.apple.com/documentation/gamecontroller/gccontroller](https://developer.apple.com/documentation/gamecontroller/gccontroller)
# GCController
실제 게임 컨트롤러, 가상 컨트롤러 또는 컨트롤러의 스냅샷의 표현.

```swift
class GCcontroller : NSObject
```

<hr class="overview">

## 개요 <a id="overview"></a>

이 클래스는 사용자가 게임 중에 상호 작용하는 실제 또는 가상 컨트롤러를 나타냅니다. 실제 컨트롤러는 장치에 직접 또는 무선으로 연결되는 물리적 컨트롤러입니다. 실제 컨트롤러는 형태에 적합하거나 장치에 밀착될 수 있으므로 플레이어는 두 가지 모두에서 동시에 컨트롤을 사용할 수 있습니다. 가상 컨트롤러는 실제 컨트롤러의 소프트웨어 에뮬레이션입니다.

당신은 컨트롤러를 발견한 다음, 게임 플레이 중에 그 컨트롤러의 입력을 처리합니다. [`controllers()`](https://developer.apple.com/documentation/gamecontroller/gccontroller/1458871-controllers) 메서드를 사용하여 현재 연결된 컨트롤러를 가져옵니다. 필요한 경우 [`startWirelessControllerDiscovery(completionHandler:)`](https://developer.apple.com/documentation/gamecontroller/gccontroller/1458879-startwirelesscontrollerdiscovery) 메서드를 사용하여 무선 컨트롤러에 연결하십시오.

이 프레임워크는 여러 개의 연결된 게임 컨트롤러를 지원합니다. 멀티플레이어 게임에서 어떤 플레이어가 컨트롤러를 사용하고 있는지 확인하려면, [`playerIndex`](https://developer.apple.com/documentation/gamecontroller/gccontroller/1458885-playerindex) 속성을 확인하고 필요한 경우 설정하세요. 싱글 플레이어 게임의 경우, [`current`](https://developer.apple.com/documentation/gamecontroller/gccontroller/3547188-current) 속성을 사용하여 플레이어가 적극적으로 사용하는 컨트롤러를 얻으십시오.

컨트롤러의 프로파일은 컨트롤러의 버튼, 패드, 축 및 기타 입력 요소에 대한 세부 사항을 캡슐화합니다. [`extendedGamepad`](https://developer.apple.com/documentation/gamecontroller/gccontroller/1458883-extendedgamepad)와 같은 프로필 속성 중 하나를 사용하여 컨트롤러의 프로필을 얻은 다음 요소의 입력을 처리합니다.

게임 루프의 각 반복에서 입력 요소의 값을 얻거나, 해당 값이 변경될 때 콜백을 수신하도록 핸들러를 설정할 수 있습니다. 예를 들어, [`GCExtendedGamepad`](https://developer.apple.com/documentation/gamecontroller/gcextendedgamepad) 프로필의 [`leftThumbstick`](https://developer.apple.com/documentation/gamecontroller/gcextendedgamepad/1522564-leftthumbstick) 속성을 사용하여 thumbstick 상태를 얻으십시오. [`valueChangedHandler`](https://developer.apple.com/documentation/gamecontroller/gcextendedgamepad/1522464-valuechangedhandler) 속성을 사용하여 프로파일에서 변경되는 입력 값을 처리하기 위해 구현하는 핸들러를 설정하십시오.

또는 [`capture()`](https://developer.apple.com/documentation/gamecontroller/gccontroller/3181207-capture) 메서드를 사용하여 실제 또는 가상 컨트롤러의 스냅샷을 만들 수 있습니다. 스냅샷은 현재 요소 값을 가진 순간에 컨트롤러의 복사본입니다. 스냅샷을 만드는 것은 성능에 영향을 미칠 수 있으며, 시간이 지남에 따라 스냅샷이 최신 상태로 유지되지 않습니다. 다른 유형의 컨트롤러와 달리 스냅샷에서 요소의 값을 설정할 수 있습니다.


<hr class="topics">

## 주제 <a id="topics"></a>

<hr class="relationships">

## 연관 관계 <a id="relationships"></a>

<hr class="see-also">

## 같이 보기 <a id="see-also"></a>