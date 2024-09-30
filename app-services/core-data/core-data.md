
> 출처
> [https://developer.apple.com/documentation/coredata](https://developer.apple.com/documentation/coredata)
# Core Data
단일 장치에서 데이터를 지속하거나 캐시하거나 CloudKit으로 데이터를 여러 장치에 동기화합니다.

<hr class="overview">

## 개요 <a id="overview"></a>

Core Data를 사용하여 오프라인 사용을 위해 애플리케이션의 영구 데이터를 저장하고, 임시 데이터를 캐시하고, 단일 장치에서 앱에 실행 취소 기능을 추가하십시오. 단일 iCloud 계정에서 여러 장치에서 데이터를 동기화하기 위해 Core Data는 자동으로 스키마를 CloudKit 컨테이너에 미러링합니다.

코어 데이터의 데이터 모델 편집기를 통해 데이터의 유형과 관계를 정의하고 각각의 클래스 정의를 생성합니다. 코어 데이터는 런타임에 객체 인스턴스를 관리하여 다음과 같은 기능을 제공할 수 있습니다.

### 영속성

Core Data는 개체를 저장소에 매핑하는 세부 사항을 추상화하여 데이터베이스를 직접 관리하지 않고 Swift 및 Objective-C에서 데이터를 쉽게 저장할 수 있도록 합니다.

<div align="center">
<img src = https://docs-assets.developer.apple.com/published/74bfc36784/CD-Persistence~dark@2x.png width="250" height="auto">
</div>

### 개별 및 일괄 변경 실행 취소 및 다시 실행

Core Data의 실행 취소 관리자는 변경 사항을 추적하고 개별적으로, 그룹으로 또는 한 번에 롤백할 수 있어 앱에 실행 취소 및 다시 실행 지원을 쉽게 추가할 수 있습니다.

<div align="center">
<img src = https://docs-assets.developer.apple.com/published/9232e513a7/CD-Undo~dark@2x.png width="500" height="auto">
</div>

### 백그라운드 데이터 타스크

백그라운드에서 JSON을 객체로 파싱하는 것과 같은 잠재적으로 UI 차단 데이터 작업을 수행하십시오. 그런 다음 결과를 캐시하거나 저장하여 서버 왕복을 줄일 수 있습니다.

<div align="center">
<img src = https://docs-assets.developer.apple.com/published/a903db10e0/CD-BackgroundTask~dark@2x.png width="250" height="auto">
</div>


### 뷰 동기화

코어 데이터는 또한 테이블 및 컬렉션 뷰에 대한 데이터 소스를 제공함으로써 뷰와 데이터를 동기화하는 데 도움이 됩니다.
### 버전기록 및 마이그레이션

코어 데이터에는 앱이 발전함에 따라 데이터 모델을 버전화하고 사용자 데이터를 마이그레이션하는 메커니즘이 포함되어 있습니다.

<hr class="topics">

## 주제 <a id="topics"></a>

### 주요 <a id="essentials"></a>

코어 데이터 모델 생성하기
Define your app’s object structure with a data model file.

### 데이터 모델링 <a id="data-modeling"></a>

### 불러오기 요청들 <a id="fetch-requests"></a>

### SwiftData 마이그레이션 및 공존 <a id="SwiftData-migration and-coexistence"></a>

### CloudKit 미러링 <a id="cloudkit-mirroring"></a>

### 변경 진행 <a id="change-processing"></a>

### 백그라운드 실행 <a id="background-tasks"></a>

### 주요 <a id="essentials"></a>

### 데이터 모델 마이그레이션 <a id="data-model-migration"></a>

### 관련 타입들 <a id="related-types"></a>

<hr class="relationships">

## 연관 관계 <a id="relationships"></a>

<hr class="see-also">

## 같이 보기 <a id="see-also"></a>