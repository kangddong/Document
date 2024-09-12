> 출처
> https://developer.apple.com/documentation/uikit/views_and_controls/collection_views

# 컬렉션 뷰
구성 가능하고 고도로 사용자 정의 가능한 레이아웃을 사용하여 중첩된 뷰를 표시합니다.

## 개요
컬렉션 뷰는 사진 앱의 사진 그리드와 같은 정렬된 콘텐츠 세트를 관리하고 시각적으로 표시합니다.

<div align="center">
<img src = https://docs-assets.developer.apple.com/published/4623993d5d/renderedDark2x-1627683112.png width="250" height="auto">
</div>

컬렉션 뷰는 다음을 포함한 다양한 개체 간의 협업입니다.

- **셀**. 셀은 각 콘텐츠에 대한 시각적 표현을 제공합니다.

- **레이아웃**. 레이아웃은 컬렉션 보기에서 콘텐츠의 시각적 배열을 정의합니다.

- **데이터 소스 개체**. 이 개체는 [`UICollectionViewDataSource`](https://developer.apple.com/documentation/uikit/uicollectionviewdatasource) 프로토콜을 채택하고 컬렉션 뷰에 대한 데이터를 제공합니다.

- **대리인 개체**. 이 개체는 [`UICollectionViewDelegate`](https://developer.apple.com/documentation/uikit/uicollectionviewdelegate) 프로토콜을 채택하고 선택 및 강조 표시와 같은 컬렉션 뷰의 콘텐츠와의 사용자 상호 작용을 관리합니다.

- 컬렉션 뷰 컨트롤러. 일반적으로 컬렉션 보기를 관리하기 위해 [`UICollectionViewController`](https://developer.apple.com/documentation/uikit/uicollectionviewcontroller) 개체를 사용합니다. 다른 뷰 컨트롤러도 사용할 수 있지만 일부 컬렉션 관련 기능이 작동하려면 컬렉션 뷰 컨트롤러가 필요합니다.

<hr class="overview">


## 주제

### 뷰
- UICollectionView
- UICollectionViewController
### 데이터

### 셀

### 레이아웃

### 선택 관리
### 드래그 앤 드랍

