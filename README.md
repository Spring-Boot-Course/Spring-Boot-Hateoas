# HATEOAS

현재 리소스와 연관된 링크 정보를 클라이언트에게 제공한다.

```java
/*
*   Method 호출에 대한 Relation(링크)를 담아서 Resource<T>형으로 반환
*/

Resource<Hello> helloResource = new Resource<>(hello);
helloResource.add(linkTo(methodOn(SampleController.class).hello()).withSelfRel());
return helloResource;
```
그에 대한 Test Code 작성
```java
@Test
public void hello() throws Exception {
    mockMvc.perform(get("/hello"))
            .andDo(print())
            .andExpect(status().isOk())
            .andExpect(jsonPath("$._links.self").exists());
}
```

Hateoas 반환 예시

```json
{
  "_links" : {
    "self" : {
      "href" : "http://localhost:8080"
    }
  }
}
```