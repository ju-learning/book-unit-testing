# 🗂 예제 자료

- [매닝출판사 도서정보 페이지](https://www.manning.com/books/unit-testing)
- [에이콘출판사 깃허브](https://github.com/AcornPublishing/unit-testing)
- 기타 온라인 자료
    - 저자 블로그: https://enterprisecraftsmanship.com/
    - 단위테스트 온라인 과정: https://unittestingcourse.com/

# 📝 강의 내용 정리

> 1부 더 큰 그림
> 

# 1장 단위 테스트의 목표

- 단위 테스트를 배우는 것은 테스트 프레임워크나 목 라이브러리(mocking library) 등과 같은 기술적인 부분을 익히는 것에 그치치 않고, 단순히 테스트를 작성하는 것보다 더 큰 범주

## 1.1 단위 테스트 현황

- 지난 20년간 단위 테스트를 적용할 것을 독려하는 분위기가 자리잡았으며, 이제 대부분의 회사에서 필수로 간주될 정도로 독려하는데 성공
- 그냥 쓰고 버리는 프로젝트가 아니라면, 단위 테스트는 늘 적용해야 한다
- 논쟁은 이제 “단위테스트를 작성해야 하는가?” 에서 “좋은 단위테스트란 무엇인가?” 로 바뀌었고, 이는 여전히 매우 혼란스러움

## 1.2 단위 테스트의 목표

- 단위 테스트와 코드 설계의 관계
    - 코드를 단위테스트 하기 어렵다면 코드 개선이 반드시 필요하다는 것을 의미
    - 보통 강결합(tight coupling) 코드에서 저품질이 나타나는데, 여기서 강결합은 제품 코드가 서로 충분히 분리되지 않아서 따로 테스트하기 어려움을 말함
- 단위 테스트의 목표는 무엇인가? → **소프트웨어 프로젝트의 지속 가능한 성장을 가능하게 하는것**이 핵심 목표

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a39bd53e-344e-45cd-8584-eb70a70d53c4/Untitled.jpeg)

- 처음 개발을 시작할때는 잘못된 아키텍처 결정이 없고, 걱정할만한 코드가 없지만 시간이 점점 지나면서 개발 속도가 현저히 느려지고 심지어 전혀 진행하지 못할 정도로 느려질 수 있다
- 이렇게 개발 속도가 빠르게 감소하는 현상을 소프트웨어 엔트로피(software entropy) 라고도 한다
- 지속적인 정리와 리팩터링 등과 같은 적절한 관리를 하지 않고 방치하면 시스템이 점점 더 복잡해지고 무질서해진다
- 이럴때 테스트는 안전망 역할을 하며, 대부분의 회귀(regression) 에 대한 보험을 제공하는 도구라 할 수 있다
    - 회귀란? 특정 코드 수정 이후에 기능이 의도한 대로 작동하지 않는경우이며, 소프트웨어 버그와 동의어로 사용할 수 있다
- 한가지 단점은 개발 초기에 테스트코드 작성의 노력이 필요하다는 점
- 테스트는 지속성과 확장성이 핵심이며, 이를 통해 장기적으로 개발속도를 유지할 수 있음

### 1.2.1 좋은 테스트와 좋지 않은 테스트를 가르는 요인

- 단위 테스트가 프로젝트 성장에 도움이 되는 것은 맞지만, 잘못 작성한 테스트는 여전히 프로젝트의 성장을 방해하는 요소
- 모든 코드에 테스트를 작성할 필요는 없다. 일부 테스트는 아주 중요하고 소프트웨어 품질에 매우 많은 기여를 하지만, 그밖의 테스트는 그렇지 않다
- 테스트의 가치와 유지비용 요소
    - 기반 코드(비즈니스 코드) 를 리팩터링할 때 테스트도 함께 리팩터링 하라
    - 각 코드 변경 시 테스트를 실행하라
    - 테스트가 잘못된 경고를 발생시킬 경우 처리하라
    - 기반 코드가 어떻게 동작하는지 이해하려고 할 때는 테스트를 읽는데 시간을 투자하라
- 지속 가능한 프로젝트의 성장을 위해서는 “고품질 테스트”에만 집중해야 함
- 제품코드(비즈니스) vs 테스트코드
    - 코드가 더 많아질수록, 소프트웨어 내의 잠재적인 버그에 노출되는 표면적이 넓어지고 유지비가 증가함
    - 테스트 코드도 결국 “코드” 이므로 다다익선 이 아님 → 따라서 가능한 적은코드로 확실하게 문제를 해결하는 것이 좋음
    - 테스트도 결국 “애플리케이션의 정확성을 보장하는 것을 목표” 로 하는 문제해결 코드의 일부로 봐야함 → 테스트 역시 버그에 취약하며 유지보수 해야함

## 1.3 테스트 스위트 품질 측정을 위한 커버리지 지표

- 커버리지 지표: 테스트 스위트가 소스 코드를 얼마나 실행하는지에 대한 백분율
- 커버리지 지표는 테스트 스위트의 품질을 평가하는데 자주 사용되고 일반적으로 숫자가 높을수록 좋지만, 현실은 그리 간단하지 않음
- 커버리지 지표는 중요한 피드백을 주더라도 테스트 스위트 품질을 효과적으로 측정하는 데 사용될 수 없다
- 즉, 커버리지 지표는 괜찮은 부정 지표이지만, 좋지 않은 긍정 지표이다
    - 너무 낮은 커버리지는 “테스트가 충분치 않다” 는 좋은 증거는 맞음
    - 하지만, 커버리지가 높다고해서 “양질의 테스트가 많다”는 증거는 될 수 없음

### 1.3.1 코드 커버리지 지표에 대한 이해

- 가장 많이 사용되는 지표는 코드 커버리지(code coverage) 가 있으며, 테스트 커버리지(test coverage) 로도 불린다

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dd1f455d-1ac1-45c0-b690-0bfe1efba0c7/Untitled.jpeg)

- 코드 커버리지는 코드 수가 적을수록 커버리지가 점점 높아지는데, 이는 테스트 스위트나 기반 코드베이스의 유지보수성이 변경되지 않는다(==코드가 적다고 코드가 더 좋아지는게 아님)

### 1.3.2 분기 커버리지 지표에 대한 이해

- 다른 커버리지 지표는 분기 커버리지(branch coverage)
- 분기 커버리지는 코드 커버리지의 단점을 극복하는데 도움이 되므로, 더 정확한 결과를 제공한다

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/024b1522-1e3c-456b-8c2a-0bc876717ab9/Untitled.jpeg)

- 분기 커버리지 지표는 분기 개수만 다루며, 해당 분기를 구현하는데 얼마나 코드가 필요한지 고려하지 않음
- 같은 if 문을 작성해도 코드커버리지는 if 문 내부의 코드 행 수를, 분기 커버리지는 if 문의 분기 개수(조건 수) 를 판단

### 1.3.3 커버리지 지표에 관한 문제점

- 어떤 커버리지 지표도 의존할 수 없는 이유
    - 테스트 대상 시스템의 모든 가능한 결과를 검증한다고 보장할 수 없음
    - 외부 라이브러리의 코드 경로를 고려할 수 있는 커버리지는 없음
- 커버리지 지표가 의미가 있으려면 모든 측정 지표(assert문) 을 검증해야 하는데, 모든 대상 코드에 대한 결과를 철저히 검증하는 것이 테스트를 신뢰하거나 좋은 테스트 의 기준이 아님 → 좋은테스트는 “유지보수” 가 생명
- 모든 커버리지 지표가 테스트 대상 시스템이 메서드를 호출할 때 외부 라이브러리가 통과하는 코드 경로를 고려하지 않음
- 커버리지 지표로 테스트가 철저하고 테스트가 충분한지는 전혀 알 수 없음

### 1.3.4 특정 커버리지 숫자를 목표로 하기

- 예시) 병원 환자의 체온이 높으면 열이 난다는 것을 의미하며 이는 유용한 관찰(==낮은 커버리지), 그러나 병원이 환자의 적절한 체운을 목표로 해서는 안됨(==잘못된 커버리지 목표)
- 중요) 커버리지 지표는 좋은 부정 지표 이지만, 나쁜 긍정 지표다
- 단, 시스템 핵심부분은 커버리지를 높게 두는 것이 좋다

## 1.4 무엇이 성공적인 테스트 스위트를 만드는가?

- 어떻게 테스트 스위트의 품질을 정확하게 측정할까? → 믿을 만한 방법은 스위트 내 각 테스트를 하나씩 따로 평가하는 것
- 중요) 성공적인 테스트 스위트의 특성
    - 개발 주기에 통합돼 있다
    - 코드베이스에서 가장 중요한 부분만을 대상으로 한다
    - 최소한의 유지비로 최대의 가치를 끌어낸다

### 1.4.1 개발 주기에 통합돼 있음

- 모든 테스트는 개발 주기에 통합돼야 함
- 이상적으로는 코드가 변경될 때마다 아무리 작은 것이라도 실행해야 함

### 1.4.2 코드베이스에서 가장 중요한 부분만을 대상으로 함

- 테스트가 주는 가치는 테스트 구조 뿐만 아니라 검증하는 코드에도 있음
- 대부분의 애플리케이션에서 가장 중요한 부분은 비즈니스로직(도메인 모델) 이 있는 부분
- 비즈니스 로직 테스트가 시간 투자 대비 최고의 수익을 낼 수 있음
- 그외의 코드들
    - 인프라 코드
    - 데이터베이스나 서드파티 시스템과 같은 외부 서비스 및 종속성 (e.g. repository, feignclient)
    - 모든 것을 하나로 묶는 코드 (e.g. mapper)
- 인프라 코드 같은건 중요 알고리즘이 있을 수 있으므로 이럴땐 테스트를 많이 하는것이 좋다
- 통합 테스트와 같이 일부 테스트는 도메인 모델을 넘어 코드베이스의 중요하지 않은 부분을 포함해 시스템의 전체 동작을 확인할 수 있음
- 가장 기본은 “도메인 모델” 이며, 도메인 모델의 코드베이스도 중요한 부분과 그렇지 않은 부분을 분리해야 함

### 1.4.3 최소 유지비로 최대 가치를 끌어냄

- 단위 테스트에서 가장 어려운 부분은 최소 유지비로 최대 가치를 달성하는것이며, 이는 이책에서 말하려는 핵심
- 유지비를 상회하는 테스트만 스위트에 유지하는 것이 중요
    - 가치 있는 테스트와 가치 없는 테스트 식별하기
    - 가치 있는 테스트 작성하기
- 가치 있는 테스트를 작성하려면 코드 설계 기술도 알아야 하며 따라서 책 내용의 상당부는 코드 설계를 설명함
- 단위 테스트와 기반 코드는 서로 얽혀 있으므로 코드베이스에 노력을 많이 기울이지 않으면 가치 있는 테스트를 만들기 힘듦

## 1.5 이 책을 통해 배우는 것

- 테스트 스위트 내의 모든 테스트를 분석하는 데 사용할 수 있는 기준틀을 설명 (이것이 기초) → ~4장
- 단위 테스트 기술과 실천을 살펴봄 → 4~6장
- 소프트웨어 개발자는 어떤 결정이 내려진 이유를 정확히 설명할 수 없다면 설계 결정에 대해 완전히 인정받지 못한다

## 요약

- 코드베이스에 변경이 생길때마다 무질서(엔트로피) 도 증가하며 코드는 점점 더 나빠지는 경향이 있고, 테스트는 이러한 경향을 뒤집을 수 있다
- 테스트는 안전망 역할을 하며, 대부분의 회귀에 대한 보험을 제공하는 도구
- 단위 테스트를 작성하는 것이 중요하며, 그중에서도 “좋은 단위테스트” 를 작성하는 것이 중요하다
- 단위 테스트의 궁극적인 목표는 “소프트웨어 프로젝트가 지속적으로 성장하게 하는 것”
- 각각의 테스트는 비용과 편익 요소가 있으므로 모든 테스트를 똑같이 작성 할 필요는 없다
    - 테스트 스위트 내에 가치 있는 테스트만 남기고 모두 제거하라
    - 애플리케이션과 테스트 코드는 모두 자산이 아니라 부채다
- 단위 테스트를 할 수 없는 코드는 품질이 좋지 못함을 뜻하지만, 단위테스트를 할 수 있다고해서 좋은코드라는 증거는 아니다
- 마찬가지로 커버리지도 낮다는 것은 문제의 징후지만, 높다고해서 테스트 스위트의 품질이 높다는 것은 아니다
- 분기 커버리지로 테스트 스위트의 완전성에 대해 더 나은 인사이트를 얻을 수 있지만, 테스트 스위트가 충분한지는 여전히 알 수 없다
- 특정 커버리지 숫자를 부과하면 동기부여가 잘못된 것 → 커버리지를 위한 테스트를 짤 가능성이 있음
- 시스템의 핵심 부분에 커버리지를 높게 갖는것은 좋지만, 이 높은 수준을 요건으로 삼는것은 좋지 않다
- 성공적인 테스트 스위트의 조건
    - 개발주기에 통합돼 있음
    - 코드베이스의 핵심 부분을 대상으로 함
    - 최소한의 유지비로 최대한의 가치를 끌어냄
- 단위 테스트의 목표를 달성하기 위한 유일한 방법
    - 좋은 테스트와 좋지 않은 테스트를 구별하는 방법을 배운다
    - 테스트를 리팩터링하여 더 가치있게 만든다

# 2장 단위 테스트란 무엇인가

- 단위 테스트에 접근하는 방법은 두가지 견해로 “고전파(classical school)” 와 “런던파(London school)” 로 나뉘었다
    - 고전파: 모든 사람이 단위 테스트와 테스트 주도 개발에 원론적으로 접근하는 “고전” 방식
    - 런던파: 런던 프로그래밍 커뮤니티에서 시작
- “단위 테스트” 의 정의가 이 둘을 구분짓는 열쇠
- 이 책에선 개인적으로 “고전파” 를 선호

## 2.1 ‘단위 테스트’의 정의

- (중요하지 않은 것들은 제외한) 단위 테스트의 가장 중요한 세가지 속성
    - 작은 코드 조각(단위라고도 함)을 검증
    - 빠르게 수행
    - 격리된 방식으로 처리하는 자동화된 테스트
- “빠른 단위 테스트” 란 매우 주관적인 척도이므로, 실행 시간이 충분하다면 테스트가 충분히 빠르다는 뜻
- 격리 문제는 단위 테스트의 고전파와 런던파를 구분할 수 있게 해주는 근원적 차이
- 고전파 vs 런던파
    - 고전적 접근법은 Detroit(디트로이트) 라고도 하며, 단위 테스트에 대한 고전주의적 접근법임, 켄트백의 “테스트주도 개발” 책을 추천
    - 런던 스타일은 mockist(목 추종자) 로 불린다

### 2.1.1 격리 문제에 대한 런던파의 접근

- 런던파에서는 테스트 대상 시스템을 협력자(collaborator) 에게서 격리하는 것을 “격리된 방식” 이라고 말한다
- 즉, 하나의 클래스가 다른 클래스에 의존하면 이 “모든” 의존성을 테스트 대역(test double) 로 대체해야 대상 클래스에만 집중할 수 있다고 함
- 이 방법의 이점들
    - 테스트가 실패하면 코드베이스의 어느 부분이 고장 났는지 확실히 알 수 있음 → 다른 의존성을 모두 대체 했기 때문에 테스트가 실패하면 테스트 대상이 문제인 것
    - 객체 그래프(object graph) 를 분할할 수 있음 → 의존성을 가진 코드베이스를 테스트하는 것은 어렵지만, 대역을 사용하면 추가 의존성을 주입하지 않고도 테스트 할 수 있음 (단위 테스트 준비를 크게 줄일 수 있음)
    - 프로젝트 전반적으로 한 번에 한 클래스만 테스트를 할 수 있음 (테스트 스위트 구조를 간단히 할 수 있음) → 각각의 클래스는 각각의 테스트 단위로 테스트 하기 때문

### 2.1.2 격리 문제에 대한 고전파의 접근

- 런던 스타일은 테스트 대역(목) 으로 테스트 대상 코드 조각을 분리해서 격리요구 사항을 맞춤
- 단위 테스트에서 “작은 코드 조각을 검증” 한다는 뜻에도 다양한 해석이 가능하지만, 일반적으로 한 번에 한 클래스로 테스트하는 지침을 따르려고 노력해야 함
- 단위테스트는 서로 격리해서 실행해야 테스트를 어떤 순서든 가장 적합한 방식으로 실행할 수 있으며 서로의 결과에 영향을 미치지 않는다
- 각각의 테스트를 격리하는 것은 여러 클래스가 모두 메모리에 상주하고 공유 상태에 도달하지 않는 한, 여러 클래스를 한 번에 테스트 해도 괜찮다는 뜻
- 고전파에선 테스트 간에 공유 상태를 일으키는 의존성에 대해서만 테스트 대역을 사용한다
- 공유 의존성, 비공개 의존성, 프로세스 외부 의존성 + 공유 의존성과 휘발성 의존성
    - 공유 의존성(shared dependency): 테스트 간에 공유되고 서로의 결괴에 영향을 미칠 수 있는 수단을 제공하는 의존성 (e.g. 정적 가변 필드 (static fields), 데이터베이스)
    - 비공개 의존성(private dependency): 공유하지 않는 의존성
    - 프로세스 외부 의존성(out-of-process dependency): 애플리케이션 실행 프로세스 외부에서 실행되는 의존성이며, 아직 메모리에 없는 데이터에 대한 프록시(proxy, 가짜객체) (e.g. 외부 API, 데이터베이스)
    - 휘발성 의존성은 공유 의존성과 비슷하지만 다음 중 하나를 나타내는 의존성이다
        - 개발자 머신에 기본 설치된 환경 외에 런타임 환경의 설정 및 구성을 요구 (e.g. 데이터베이스는 환경마다 “기본”으로 설치되어있지 않음)
        - 비결정적 동작(nondeterministic behavior) 을 포함한다 (e.g. `Math.random()` 같은 난수생성기나 현재날짜 `now()` 처럼 각 호출에 대해 다른 결과를 제공)
    - e.g.
        - 데이터베이스는 “프로세스외부+공유 의존성” 이지만, 각 테스트 실행전 도커 컨테이너로 데이터베이스를 시작하도록 인스턴스를 분리하면 테스트끼리 공유하지 않기 때문에 “프로세스외부+공유하지않는 의존성” 이다
        - 싱글턴(singleton) 의존성은 각 테스트에서 새 인스턴스를 만들 수 있기만 하면 공유되지않고, 인스턴스는 하나지만 테스트는 이 패턴을 따르지 않으므로 “비공개 의존성” 이다
        - 난수 생성기는 휘발성(임시 데이터) 지만, 각 테스트에 별도의 인스턴스를 제공할 수 있으므로 공유 의존성이 아니다
- 공유 의존성은 테스트 대상 클래스 간이 아니라 단위 테스트 간에 공유한다
- 공유 의존성을 대체하는 또 다른 이유는 테스트 실행 속도를 높이는 데 있음
    - 데이터베이스나 파일 시스템 등의 공유 의존성에 대한 호출은 비공개 의존성에 대한 호출보다 더 오래 걸림
    - 이러한 호출을 포함하는 공유 의존성을 가진 테스트는 단위테스트에서 통합테스트 영역으로 넘어감
- 단위가 반드시 클래스에 국한될 필요는 없음, 공유 의존성이 없는 한 여러 클래스를 묶어서 단위 테스트 할 수도 있음

## 2.2 단위 테스트의 런던파와 고전파

- 단위테스트를 각각 런던파는 “테스트 대상 시스템에서 협력자를 격리하는것”, 고전파는 “단위 테스트끼리 격리하는 것” 으로 본다
- 정리하면 아래에 대한 의견 차이가 있음
    - 격리 요구 사항
    - 테스트 대상 코드 조각(단위) 의 구성요소
    - 의존성 처리

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/605a7a12-61eb-4416-b9cd-a2fe586838d5/Untitled.jpeg)

### 2.2.1 고전파와 런던파가 의존성을 다루는 방법

- 테스트 대역을 어디에서나 흔히 사용할 수 있지만, 런던파는 테스트에서 일부 의존성을 그대로 사용할 수 있도록 함
- 불변 객체(절때 변하지 않는 객체) 는 교체하지 않아도 됨
    - `RemoveInventory(Product.Shampoo, 5)` 라는 구문에서 ‘5’ 라는 숫자는 변수조차 사용하지 않는다
    - 이러한 불변 객체를 값 객체(value object) 또는 값(value) 라고 하며, 주요 특징은 각각의 정체성이 없고 내용에 의해서만 식별 된다는 것
    - 값 객체는 내용(값)이 동일하다면 무엇을 사용해도 되며, 인스턴스를 서로 바꿔 사용할 수 있다
    - 추가적인 궁금증은 https://enterprisecraftsmanship.com/posts/entity-vs-value-object-the-ultimate-list-of-differences/ 를 참조

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/046351b6-f4df-44a0-bef4-7b44c3f5284b/Untitled.jpeg)

- (런던파와 고전파가 단위테스트에서 의존성들을 어떻게 생각하는가에 대한 그림)
- 모든 공유 의존성은 변경 가능하지만, 변경 가능한 의존성을 공유하려면 여러 테스트에서 재사용돼야 한다
- 협력자 vs 의존성
    - 협력자(collaborator) 는 공유하거나 변경 가능한 의존성
        - 데이터베이스는 공유 의존성이므로 “데이터베이스 접근 권한” 을 제공하는 협력자다
        - 주입받는 객체 (e.g. Store) 도 시간에 따라 상태가 변할 수 있기 때문에 협력자다
        - 숫자 5 같은 불변객체는 의존성이지만 협력자는 아니다 (값 객체다)
    - 일반적인 클래스는 “협력자” 와 “값” 이라는 두가지 유형의 의존성으로 동작
- 중요) 모든 프로세스 외부 의존성이 공유 의존성의 범주에 속하는 것이 아님 → 공유 의존성은 거의 프로세스 외부에 있긴 하지만, 반대로 모든 외부 프로세스가 공유 의존성은 아니라는 뜻

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8120ee7e-faae-4375-bde2-93e2b6d87ad7/Untitled.jpeg)

- 테스트가 반환하는 데이터에 영향을 미칠 수 없으면 공유가 아니다
- 대부분의 경우 테스트 속도를 높이려면 테스트 대역으로 교체해야 하지만, 프로세스 외부 의존성이 충분히 빠르고 연결이 안정적이면 테스트에서 그대로 사용해도 괜찮다
- (책에서 달리 명시하지 않는 한, 공유 의존성과 프로세스 외부 의존성이라는 용어는 같다. 왜냐면 실제 프로젝트에서 프로세스 외부가 아닌 공유의존성의 거의 없기 때문)

## 2.3 고전파와 런던파의 비교

- 복습하면 고전파와 런던파 간의 주요 차이는 단위 테스트의 정의에서 격리를 어떻게 다루는지에 있다
- (개인적으로 저자는 고전파의 단위테스트를 선호 → 목을 사용하는 테스트는 고전적인 테스트보다 지속 가능한 성장을 달성하는데 더 불안정한 경향이 있기 때문)
- 런던파의 이점
    - 입자성(granularity) 이 좋다 → 테스트가 세밀해서(fine-grained) 한번에 한 클래스씩만 확인하기 때문
    - 서로 연결된 클래스의 그래프가 커져도 테스트 하기 쉽다 → 의존성이 대역으로 대체되기 때문에
    - 테스트가 실패하면 어떤 기능에서 실패한건지 명확히 알 수 있다 → 협력자가 없기때문에 해당 클래스의 기능에서만 오류가 발생함

### 2.3.1 한 번에 한 클래스만 테스트 하기

- 단위 테스트를 런던파는 클래스 단위로 간주한다
- 객체지향 프로그래밍 경력을 가진 개발자들은 보통 클래스를 모든 코드베이스의 기초에 위치한 원자 빌딩 블록(atomic building block) 으로 간주하므로 자연스럽게 클래스를 “테스트에서 검증할 원자단위” 로 취급하게 한다
- 팁) 테스트는 코드의 단위로 검증하면 안되고 문제 영역에 의미가 있는(비즈니스 담당자가 유용하다고 인식할 수 있는) 동작의 단위로 검증해야 한다
- 사실 좋은 코드 입자성을 목표로 하는것은 도움이 되지않고 테스트가 “단일 동작 단위를 검증” 한다면 좋은 테스트다
- 테스트는 프로그래머가 아닌 일반 사람들에게 응집도가 높고 의미가 있는, “해결하는 데 도움이 되는 문제에 대한 이야기”를 들려줘야 한다
- 실제 동작 대신 개별 클래스를 목표로 테스트하면, 테스트가 이상하게 보이기 시작한다
    - e.g. 강아지를 부르면 내게 온다 vs 강아지를 부르면 먼저 앞발을 내밀고 뒷발을 움직이고 앞발을 다시 내려놓고 뒷발을 내려놓고 꼬리를 흔들고 …

### 2.3.2 상호 연결된 클래스의 큰 그래프를 단위 테스트하기

- 실제 협력자(의존성) 을 대신 목을 사용하면 클래스를 쉽게 테스트 할 수 있다
- 이것을 고전파로 시행하면 대상 시스템 전체 객체 그래프(의존성들) 을 전부 셋팅해야해서 작업량이 많을 수 있다
- (이런것들은 사실이지만) 상호 연결된 클래스의 크고 복잡한 그래프를 작성하는 방법을 찾는것보다 이러한 클래스 그래프들이 만들어지지 않도록 설계하는것이 선행되어야 한다
- 대개 클래스 그래프가 커진 것은 코드 설계 문제의 결과다
- 코드 조각을 단위테스트 하는 능력은 비교적 높은 정확도로 코드 저품질을 예측함
- 목을 사용해서 이러한 복잡한 객체 그래프를 쉽게 테스트 하는것은 문제를 감추기만 할 뿐 근본적인 원인을 해결하지는 못한다

### 2.3.3 버그 위치 정확히 찾아내기

- 런던 스타일 테스트가 있는 시스템에 버그가 생기면, 보통 SUT에 버그가 포함한 테스트만 실패한다 vs 고전방식이면 오작동하는 클래스를 참조하는 모든 클래스의 테스트가 실패하게 된다
- 하나의 버그가 전체 시스템에 걸쳐 테스트 실패를 야기하는 것은 원인을 찾기 어렵지만, 마지막으로 수정한 부분이 알아내는것은 크게 어렵지 않으므로 큰 문제가 되지 않는다
- 또한, 하나의 버그가 많은 테스트를 실패로 만들었다면 이는 수정한 코드가 전체 시스템에 의존하는 (큰 가치가 있는) 중요한 코드임을 시사하므로 가치가 있다

### 2.3.4 고전파와 런던파 사이의 다른 차이점

- 위에서 설명하지 않은 런던파와 고전파 사이의 남아있는 두가지 차이점
    - 테스트 주도 개발(Test-Driven Development; TDD) 를 통한 설계 방식
    - 과도한 명세(over-specification) 문제

# 📋 메모

- 관련 추천 도서
    - [도메인 주도 설계 - 에릭 에반스](https://www.yes24.com/Product/Goods/5312881)
    - 

# 🔠 찾아보기

- 안티 패턴(anti-pattern): 처음에는 괜찮은 것 같지만 미래에 문제를 야기하는 패턴
- 테스트 스위트(Test suite)
    - https://en.wikipedia.org/wiki/Test_suite
    - https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=netrance&logNo=110184403382
- [테스트 대상 시스템(System Under Test; SUT)](https://en.wikipedia.org/wiki/System_under_test)
- 테스트 대상 메서드(Method Under Test; MUT): 테스트에서 호출한 SUT의 메서드
    - MUT 는 흔히 SUT 와 동의어로 사용하지만, 일반적으로 MUT 는 메서드를, SUT 는 클래스 전체를 가리킨다
-
