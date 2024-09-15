# 목차
1. API Gateway Service (Spring Cloud Gateway)
2. Netflix Ribbon (Deprecated)
3. Netflix Zuul (Deprecated) -> Spring Cloud Gateway

## 1. API Gateway Service (Spring Cloud Gateway)
- 라우팅 설정에 따라 Client 대신 End Point로 요청하여 응답을 받으면 Client에 전달해주는 일종의 **Proxy** 역할
- 외부 요청에 대해 적절한 형태로 가공하여 데이터를 전달할 수 있다는 장점 존재
- 구체적인 특징
  - 인증 및 권한 부여
  - 서비스 검색 통합
  - 응답 캐싱
  - 정책, 회로 차단기 및 QoS 재시도
  - 속도 제한
  - 부하 분산
  - 로깅, 추적, 상관 관계
  - 헤더, 쿼리 문자열 및 청구 변환
  - IP 허용 목록에 추가
- 참고로 `Consul`는 서비스 검색 통합, 부하 분산, IP 허용 목록 추가 관점에서 API Gateway 기능과 공통되지만, `Consul` 자체는 API Gateway가 아닌 Service Discovery 영역에 해당      

## 2. Netflix Ribbon (Deprecated)
- Client Side Load Balancer
  - 서비스 이름으로 호출
  - Health Check
- 그러나 비동기 호출이 지원되지 않아서, 최근에는 잘 사용되지 않음 (Netflix에서도 maintenance 상태)
  - Spring Cloud Load Balancer가 많이 쓰임   
- ip, port 번호가 아닌 msa 서비스 명칭으로 외부 API 호출 가능

## 3. Netflix Zuul (Deprecated)
- Routing, API Gateway 역할
- 그러나 Netflix Ribbon과 마찬가지로 현재는 Maintenance 상태
  - Spring Cloud Gateway가 많이 쓰임
- 동기가 디폴트고, 2.X 버전부터는 비동기를 지원한다고 하지만 Spring 환경 연동성과의 이슈가 있음 -> Spring에서 자체적으로 Spring Cloud Gateway를 만듦
