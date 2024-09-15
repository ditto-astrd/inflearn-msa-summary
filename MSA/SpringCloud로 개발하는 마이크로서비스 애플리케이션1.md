# 목차
1. MSA 개념
2. Monolithic vs MSA
3. MSA와 RESTful

## 1. MSA 개념
### Antifragile (외부 시스템에 변화에도 지속적이고 안정적인 서비스의 운영이 가능)
- Auto Scaling (자동 확장성)
  - ex ) 쇼핑몰의 경우, 비수기때는 서버의 개수를 줄이고 성수기일때는 서버의 개수를 늘림
- MicroServices
- Chaos Engineering
- Continous Deployments
  - CI (지속적 통합), CD (지속적 배포)
  - 카나리 배포, 블루그린 배포 

### Cloud Native Architecture
- 확장 가능한 아키텍처
  - 시스템의 수평적 확장에 유연
  - 확장된 서버로 시스템의 부하 분산, 가용성 보장
  - 시스템 또는 서비스 어플리케이션 단위의 패키지 (컨테이너 기반 패키지)
  - 모니터링
- 탄력적 아키텍처
  - 서비스 생성 - 통합 - 배포, 비즈니스 환경 변화에 대응 시간 단축
  - 분할된 서비스 구조
- 장애 격리
  - 특정 서비스에 오류가 발생해도 다른 서비스에 영향을 주지 않음
- Container 가상화
  - 가볍고 빠르게 운영 가능

## 2. Monolithic vs MSA
### Monolithic
- FE, BE, 모든 서비스가 한 프로젝트로 유기적으로 구성됨

### MSA
- 모든 서비스가 개별 프로젝트로 쪼개어짐
- 어떤 서비스에 변경이 있을때, 해당 서비스에서만 개발 및 배포가 이루어져서 다른 서비스에 영향을 최소화 함
- 서비스간의 결합도를 낮추어 변화에 능동적으로 대응
- DB가 아닌 API 호출을 통해 데이터를 활용하고, 회원가입 API에 이슈가 있을 경우 장애가 전파되지 않고 우회할 수 있는 방법을 제공

### MSA가 최고인가?
- NO
- MSA 도입전에 아래 내용들의 고려가 필요됨
  - 변화가 얼마나 자주 일어나는지
  - 독립적인 확장성이 필요되는 환경인지
  - Polyglot이 지원되는지 (다양한 언어, DB로 개발하는게 가능한 환경인지)
  - [12 Factors](https://12factor.net/)에 부합하는지

### MSA vs SOA
- 어디까지 서비스를 공유하는지
- REST 방식을 사용하는지 (SOA는 SOAP 사용) 

## 3. MSA와 RESTful
### RESTful의 조건
1. 아래 레벨중 2, 3에 의거함
  - LEVEL 0
     - REST 스타일로 SOAP WEB Service를 표현
     - ex : http://server/getPosts
  - LEVEL 1
     - 적절한 URI와 함께 자원을 표현
       - ex : http://server/accounts/10
  - LEVEL 2
    - LEVEL1 + HTTP Methods (ex : GET, PUT, POST, DELETE)
  - LEVEL 3
    - LEVEL2 + HATEOAS
    - DATA + NEXT POSSIBLE ACTIONS
2. Response Status를 전달 해야함
  - 200, 404, 400, 201, 401 ...
3. 복수 형태의 URI 사용
  - prefer `/users` to `/user`
  - prefer `/users/1` to `/user/1`
4. 동사보다는 명사 형태의 URI 사용    

----
- MSA 표준 구성 요소 : [CNCF](https://landscape.cncf.io/)
