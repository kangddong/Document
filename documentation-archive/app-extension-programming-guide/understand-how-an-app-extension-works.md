> 출처
> [https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/ExtensionOverview.html#//apple_ref/doc/uid/TP40014214-CH2-SW2](https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/ExtensionOverview.html#//apple_ref/doc/uid/TP40014214-CH2-SW2)
# 앱 확장 프로그램 작동 이해하기

<hr class="overview">

앱 확장 프로그램은 앱이 아닙니다. 특정 확장 포인트에 의해 정의된 정책을 준수하는 구체적이고 범위가 좋은 작업을 구현합니다.

## 앱 확장 프로그램의 생명주기 <a id="An App Extension’s Life Cycle"></a>

앱 확장 프로그램은 앱이 아니기 때문에 수명 주기와 환경이 다릅니다. 대부분의 경우, 확장은 사용자가 앱의 UI 또는 전환된 활동 컨트롤러에서 선택할 때 실행됩니다. 사용자가 앱 확장 프로그램을 선택하기 위해 사용하는 앱을 호스트 앱이라고 합니다. 호스트 앱은 확장에 제공된 컨텍스트를 정의하고 사용자 행동에 대한 응답으로 요청을 보낼 때 확장 수명 주기를 시작합니다. 확장은 일반적으로 호스트 앱에서 받은 요청을 완료한 직후 종료됩니다.

예를 들어, 사용자가 OS X 호스트 앱에서 일부 텍스트를 선택하고, 공유 버튼을 활성화하고, 공유 목록에서 앱 확장 프로그램을 선택하여 소셜 공유 웹사이트에 텍스트를 게시하는 데 도움을 준다고 상상해 보십시오. 호스트 앱은 선택한 텍스트를 포함하는 요청을 확장에 발행하여 사용자의 선택에 응답합니다. 이 상황의 일반화된 버전은 그림 2-1의 1단계에 나와 있습니다.

**그림 2-1** 앱 확장 프로그램의 기본 수명 주기
<div align="center">
<img src = https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/Art/app_extensions_lifecycle_2x.png width="500" height="auto">
</div>

그림 2-1의 2단계에서 시스템은 호스트 앱의 요청에서 식별된 앱 확장을 인스턴스화하고 그들 사이의 통신 채널을 설정합니다. 앱 확장 프로그램은 호스트 앱의 컨텍스트 내에서 뷰를 표시한 다음 호스트 앱의 요청에서 받은 항목을 사용하여 작업을 수행합니다(이 예에서 확장은 선택한 텍스트를 수신합니다).

그림 2-1의 3단계에서 사용자는 앱 확장 프로그램에서 작업을 수행하거나 취소하고 이를 해제합니다. 이 조치에 대한 응답으로, 확장 프로그램은 사용자의 작업을 즉시 수행하거나 필요한 경우 이를 수행하기 위해 백그라운드 프로세스를 시작함으로써 호스트 앱의 요청을 완료합니다. 호스트 앱은 확장 프로그램의 보기를 찢고 사용자는 호스트 앱 내에서 이전 컨텍스트로 돌아갑니다. 확장 프로그램의 작업이 완료되면, 즉시든 나중에든, 결과는 호스트 앱으로 반환될 수 있습니다.

앱 확장 프로그램이 작업을 수행한 직후(또는 이를 수행하기 위해 백그라운드 세션을 시작), 4단계와 같이 시스템은 확장을 종료합니다.

## 앱 확장 프로그램은 어떻게 통신하는가 <a id="How an App Extension Communicates"></a>

앱 확장은 주로 호스트 앱과 통신하며, 트랜잭션 처리를 연상시키는 용어로 그렇게 합니다: 호스트의 요청과 확장의 응답이 있습니다. 그림 2-2는 실행 중인 확장 프로그램, 이를 실행한 호스트 앱 및 포함된 앱 간의 관계에 대한 단순화된 보기를 보여줍니다.

**그림 2-2** 앱 확장 프로그램은 호스트 앱과만 직접 통신합니다.
<div align="center">
<img src = https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/Art/simple_communication_2x.png width="500" height="auto">
</div>

앱 확장과 그 포함 앱 사이에는 직접적인 통신이 없습니다; 일반적으로, 포함 확장이 실행되는 동안에는 포함 앱이 실행되지도 않습니다. 앱 확장의 포함된 앱과 호스트 앱은 전혀 통신하지 않습니다.

일반적인 요청/응답 거래에서 시스템은 호스트 앱을 대신하여 앱 확장을 열어 호스트가 제공하는 확장 컨텍스트에서 데이터를 전송합니다. 확장 프로그램은 사용자 인터페이스를 표시하고, 일부 작업을 수행하며, 확장의 목적에 적합한 경우 데이터를 호스트에 반환합니다.

그림 2-2의 점선은 앱 확장과 그 포함 앱 사이에 사용 가능한 제한된 상호 작용을 나타냅니다. 오늘 위젯(다른 앱 확장 유형 없음)은 [NSExtensionContext](https://developer.apple.com/documentation/foundation/nsextensioncontext) 클래스의 [openURL:completionHandler:](https://developer.apple.com/documentation/foundation/nsextensioncontext/1416791-open) 메서드를 호출하여 시스템에 포함 앱을 열도록 요청할 수 있습니다. 그림 2-3의 읽기/쓰기 화살표에 표시된 바와 같이, 모든 앱 확장과 그 포함 앱은 비공개로 정의된 공유 컨테이너의 공유 데이터에 액세스할 수 있습니다. 확장 프로그램, 호스트 앱 및 포함 앱 간의 통신에 대한 전체 어휘는 그림 2-3에 간단한 형식으로 표시됩니다.

**그림 2-3** 앱 확장 프로그램은 포함된 앱과 간접적으로 통신할 수 있습니다.
<div align="center">
<img src = https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/Art/detailed_communication_2x.png width="600" height="auto">
</div>


{% hint style="info" %}  **노트**
장면 뒤에서, 시스템은 프로세스 간 통신을 사용하여 호스트 앱과 앱 확장이 함께 작동하여 응집력 있는 경험을 가능하게 합니다. 확장 포인트와 시스템에서 제공하는 상위 수준의 API를 사용하기 때문에 코드에서 이 기본 통신 메커니즘에 대해 생각할 필요가 없습니다.
{% endhint %}

## 앱 확장 프로그램에 사용할 수 없는 API

시스템에서 집중된 역할 때문에, 앱 확장 프로그램은 특정 활동에 참여할 수 없습니다. 앱 확장 프로그램은 다음을 할 수 없습니다:

- [sharedApplication](https://developer.apple.com/documentation/uikit/uiapplication/1622975-shared) 개체에 액세스하므로 해당 개체의 어떤 메서드도 사용할 수 없습니다.

- `NS_EXTENSION_UNAVAILABLE `매크로 또는 유사한 가용성 매크로 또는 사용할 수 없는 프레임워크의 API로 헤더 파일에 표시된 API를 사용하십시오.
  예를 들어, iOS 8.0에서는 HealthKit 프레임워크와 EventKit UI 프레임워크를 앱 확장에 사용할 수 없습니다.

- iOS 기기에서 카메라 또는 마이크에 액세스 (iMessage 앱은 다른 앱 확장 프로그램과 달리 [NSCameraUsageDescription](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW24) 및 [NSMicrophoneUsageDescription](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW25) `Info.plist` 키를 올바르게 구성하는 한 이러한 리소스에 액세스할 수 있습니다)

- 오래 실행되는 백그라운드 작업 수행
  이 제한의 세부 사항은 이 문서의 확장 포인트 장에 설명된 바와 같이 플랫폼에 따라 다릅니다.
  (앱 확장은 [NSURLSession](https://developer.apple.com/documentation/foundation/urlsession) 개체를 사용하여 업로드 또는 다운로드를 시작할 수 있으며, 해당 작업의 결과는 컨테이너 앱에 보고됩니다.)

- AirDrop을 사용하여 데이터 수신
  (앱 확장은 [UIActivityViewController](https://developer.apple.com/documentation/uikit/uiactivityviewcontroller) 클래스를 사용하여 앱과 동일한 방식으로 AirDrop을 사용하여 데이터를 보낼 수 있습니다.)
