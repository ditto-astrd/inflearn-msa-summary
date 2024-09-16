# 목차
1. Server vs Servlet
2. Filter

## 1. Server vs Servlet
- WAS를 `Netty`로 사용시 `ServerHttpRequest` `ServerHttpResponse`을 사용
- `ServletHttp`가 아닌 이유는 지금 사용중인 내장서버는 `Netty`
- 기존의 `Tomcat`은 동기 방식이지만, `Netty`는 비동기 방식
- Spring WebFlux도 마찬가지

## 2. Filter
- Gateway Client -> Gateway Handler -> Global Filter -> Custom Filter -> Logging Filter -> Proxied Service
``` java
  // OrderedGatewayFilter.java
  public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
    return this.delegate.filter(exchange, chain);
  }
```
- `ServerHttpRequest` `ServerHttpResponse` 객체를 사용할 수 있도록 도와주는게 `ServerWebExchange` 
- `GatewayFilterChain`은 **PreChain**, **PostChain**등과 연결시켜 작업을 도움
