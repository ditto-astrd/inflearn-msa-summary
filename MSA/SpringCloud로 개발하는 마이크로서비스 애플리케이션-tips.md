# BE
- `POST`로 객체 생성시, `HttpStatusCode`는 **200**이 아닌 **201**이 적합 (= 201 Created) 
- List vs Iterable
  ``` java
  Iterable<UserEntity> getAllUsers();
  List<UserEntity> getAllUsers();
  ```
  - Iterable<UserEntity>가 더 적절한 경우
    - 데이터의 순서나 중복 여부가 중요하지 않고, 그저 반복 가능하기만 하면 되는 경우
    - 반환 타입에 유연성을 두고 싶을 때, 즉 다양한 컬렉션 타입을 사용할 가능성이 있는 경우 (ex : Set, Map)
  - List<UserEntity>가 더 적절한 경우:
    - 결과가 List로 확정된 경우(대부분의 경우가 여기에 해당)
    - 순서가 중요하거나, 인덱스를 통해 특정 요소에 접근해야 할 필요가 있는 경우
    - 반환된 데이터가 자주 리스트 형태로 쓰이는 경우
- Entity의 직렬화
  ```java
    public class OrderEntity implements Serializable { //... }
  ```
  - JPA 2차 캐시를 사용하는 경우, 엔티티 객체는 캐시에 저장되기 전에 직렬화되어야 함 
  - 직렬화는 객체를 바이트 스트림으로 변환하여 메모리, 디스크, 또는 네트워크를 통해 객체를 저장하거나 전송하는 방법을 제공
  - 또한, 세션 클러스터링(특히 웹 애플리케이션에서)을 지원하려면 엔티티 객체를 세션과 함께 직렬화하여 다른 서버로 전송할 수 있어야 함

# github
- 로컬 플젝을 원격 플젝에 연동하는 방법
  1. git remove -v로 연동되어있는 github 확인
  2. 없을 경우 `git remote add origin github주소`로 원격 서버에 연동
  3. `git push --set-upstream origin` 현재 브랜치로 원격 푸시


# Linux
- brew list : brew로 설치한 목록들을 다 보여줌
