## 1. 구조
### API Gateway
```yml
server:
  port: 8000
eureka:
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url:
      defaultZone: http://localhost:8761/eureka
spring:
  application:
    name: api-gateway-service
  cloud:
    gateway:
      default-filters:
        - name: GlobalFilter
          args:
            baseMessage: Spring Cloud Gateway GlobalFilter
            preLogger: true
            postLogger: true
      routes:
        - id: user-service
          uri: lb://USER-SERVICE
          predicates:
            - Path=/user-service/**
```
- API Gateway의 역할 1 
  - predicates에 명시된 /user-service로 요청이 들어올 경우 -> (uri) eureka에 등록된 USER-SERVICE로 라우팅

### Eureka(Service Discovery)
- 해당 서버는 서비스 디스커버리 역할을 위해 상시 켜져있어야 함
```yml
server:
  port: 8761

spring:
  application:
    name: discoveryservice
eureka:
  client:
    register-with-eureka: false
    fetch-registry: false

```

- 이 외에 서비스가 등록되는 프로젝트는 아래와 같이 `application.yml` 작성
```yml
server:
  port: 0   # 랜덤 포트

spring:
  application:
    name: user-service

eureka:
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url:
      defaultZone: http://127.0.0.1:8761/eureka
  instance:
    instance-id: ${spring.application.name}:${spring.application.instance_id:${random.value}}
```

## 2. API Gateway 특징
- http://192.168.219.100:62229/health-check 는 되지만 http://192.168.219.100:8000/user-service/health-check 는 안됨
- 전자는 (랜덤 포트로 등록된) `user-service` 프로젝트, 후자는 `api-gateway` 프로젝트
- Users Service의 URI와 API Gateway의 URI가 다름
  1. http://~:8000/user-service/health-check 접속
  2. predicates를 따라 -> uri: lb://USER-SERVICE -> user service 프로젝트에게 /user-service/health-check를 호출하게됨
  3. 알다시피 user-service에는 /health-check는 있어도 /user-service/health-check는 없음
