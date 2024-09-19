
> 출처
> [https://developer.apple.com/documentation/gamecontroller/gccontroller](https://developer.apple.com/documentation/gamecontroller/gccontroller)
# Social
표준 시스템 인터페이스를 사용하여 지원되는 소셜 네트워킹 서비스에 콘텐츠를 게시합니다.

<hr class="overview">

## 개요 <a id="overview"></a>

iOS 및 macOS에서 이 프레임워크는 HTTP 요청을 생성하기 위한 템플릿을 제공합니다. iOS에서만, 소셜 프레임워크는 사용자를 대신하여 요청을 게시하기 위한 일반화된 인터페이스를 제공합니다.

이 프레임워크를 사용하는 일반적인 방법은 다음과 같습니다.

- 네트워크 세션을 만드세요.

- 사용자를 위한 활동 피드를 받으세요.

- 새로운 게시물을 만드세요.

- 게시물에 속성을 설정하고, 첨부 파일을 추가하는 등.

- 활동 피드에 게시물을 게시하세요.


<hr class="topics">

## 주제 <a id="topics"></a>
### 구성 인터페이스 <a id="compositional-interface"></a>

[`class SLComposeServiceViewController`](https://developer.apple.com/documentation/social/slcomposeserviceviewcontroller)
	사용자가 소셜 미디어 게시물을 작성할 수 있도록 공유 앱 확장에서 제공하는 뷰 컨트롤러.

[`class SLComposeViewController`](https://developer.apple.com/documentation/social/slcomposeviewcontroller)
	사용자가 소셜 미디어 게시물을 작성할 수 있도록 하는 뷰 컨트롤러.

### 서버 통신 <a id="server-communication"></a>

[`class SLRequest`](https://developer.apple.com/documentation/social/slrequest)
	소셜 미디어 서비스와 통신하기 위해 HTTP 요청을 구성하는 데 사용하는 개체.