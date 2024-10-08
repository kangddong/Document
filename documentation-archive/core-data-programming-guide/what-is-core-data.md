
> 출처
> [https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/index.html#//apple_ref/doc/uid/TP40001075-CH2-SW1](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/index.html#//apple_ref/doc/uid/TP40001075-CH2-SW1)
# What Is Core Data?

코어 데이터는 애플리케이션의 모델 레이어 개체를 관리하는 데 사용하는 프레임워크입니다. 영속성을 포함하여 개체 수명 주기 및 개체 그래프 관리와 관련된 일반적인 작업에 대한 일반화되고 자동화된 솔루션을 제공합니다.

코어 데이터는 일반적으로 모델 레이어를 지원하기 위해 작성하는 코드의 양을 50~70% 감소시킵니다. 이는 주로 구현, 테스트 또는 최적화할 필요가 없는 다음과 같은 내장 기능 때문입니다.

- 변경 추적 및 기본 텍스트 편집을 넘어 실행 취소 및 다시 실행에 대한 내장 관리.
- 개체 간의 관계의 일관성 유지를 포함하여 변화 전파의 유지.
- 객체의 지연 로딩, 부분적으로 구체화된 미래(장애), 오버헤드를 줄이기 위한 copy-on-write 데이터 공유.
- 속성 값의 자동 검증. 관리되는 객체는 표준 키-값 코딩 검증 방법을 확장하여 개별 값이 허용 범위 내에 있는지 확인하여 값의 조합이 의미가 있도록 합니다.
- 스키마 변경을 단순화하고 효율적인 인플레이스 스키마 마이그레이션을 수행할 수 있는 스키마 마이그레이션 도구.
- 사용자 인터페이스 동기화를 지원하기 위해 애플리케이션의 컨트롤러 계층과의 선택적 통합.
- 메모리와 사용자 인터페이스에서 데이터를 그룹화, 필터링 및 구성합니다.
- 외부 데이터 저장소에 개체를 저장하기 위한 자동 지원.
- 정교한 쿼리 편집. SQL을 작성하는 대신, NSPredicate 객체를 가져오기 요청과 연관시켜 복잡한 쿼리를 만들 수 있습니다.
- 자동 멀티라이터 충돌 해결을 지원하기 위한 버전 추적 및 낙관적 잠금.
- macOS 및 iOS 도구 체인과의 효과적인 통합.

{% hint style="info" %} 노트

이 문서는 편의와 명확성을 위해 직원 데이터베이스 스타일의 예를 사용합니다. 그것은 풍부하지만 쉽게 이해할 수 있는 문제 영역을 나타냅니다. 그러나 핵심 데이터 프레임워크는 데이터베이스 스타일의 애플리케이션에 국한되지 않으며 클라이언트-서버 동작에 대한 기대도 없습니다. 프레임워크는 스케치와 같은 벡터 그래픽 애플리케이션이나 Keynote와 같은 프레젠테이션 애플리케이션의 기초만큼 유용합니다.
{% endhint %}