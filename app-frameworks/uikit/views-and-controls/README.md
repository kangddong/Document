> 출처
> https://developer.apple.com/documentation/uikit/views_and_controls

# 뷰와 컨트롤
당신의 콘텐츠를 화면에 제시하고 그 콘텐츠로 허용되는 상호작용을 정의하세요.

## 개요
뷰와 컨트롤은 앱 사용자 인터페이스의 시각적 구성 요소입니다. 뷰와 컨트롤을 사용하여 화면에서 앱의 콘텐츠를 그리고 구성하세요.

<div align="center">
<img src = https://docs-assets.developer.apple.com/published/ca23391d9e/renderedDark2x-1662140003.png width="344" height="500">
</div>

뷰는 다른 뷰를 호스팅할 수 있습니다. 한 뷰를 다른 뷰 안에 삽입하면 호스트 뷰(_슈퍼뷰_ 라고 함)와 임베디드 뷰(_하위 뷰_ 라고도 함) 사이에 격리 관계가 생성됩니다. 뷰 계층은 보기를 더 쉽게 관리할 수 있게 해준다.

당신은 또한 뷰를 사용하여 다음 중 하나를 할 수 있습니다:

- 터치 및 기타 이벤트에 응답하십시오 (직접 또는 제스처 인식기와 협력하여).

- 코어 그래픽 또는 UIKit 클래스를 사용하여 사용자 지정 콘텐츠를 그리십시오.

- 드래그 앤 드롭 상호 작용을 지원합니다.

- 포커스 변화에 대응하십시오.

- 뷰의 크기, 위치 및 모양 속성을 애니메이션화하십시오.

UIView는 모든 뷰에 대한 루트 클래스이며 일반적인 동작을 정의합니다. UIControl은 사용자 상호 작용을 위해 설계된 버튼, 스위치 및 기타 뷰에 특정한 추가 동작을 정의합니다.

뷰와 컨트롤을 사용하는 방법에 대한 추가 정보는 [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/components/all-components)을 참조하십시오. UIKit 컨트롤의 예를 보려면 [UIKit Catalog: 뷰 및 컨트롤 생성 및 커스터마이징](https://developer.apple.com/documentation/uikit/mac_catalyst/uikit_catalog_creating_and_customizing_views_and_controls)을 참조하십시오.

<hr class="overview">


## 주제

### 기본 뷰
- UIView
- [UIKit Catalog: 뷰 및 컨트롤 생성 및 커스터마이징](https://developer.apple.com/documentation/uikit/mac_catalyst/uikit_catalog_creating_and_customizing_views_and_controls)
### 컨테이너 뷰

- [Collection views](app-frameworks/uikit/views-and-controls/collection-views/README.md)

