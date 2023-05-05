# 안전한 호출과 엘비스 연산자

## 안전한 호출

- ?.로 메서드를 호출 할경우, null이 아닐경우에만 메서드를 호출한다.
```kotlin
val s1: String? = null
val length = if(s1 != null) s1.length else null
//위 아래 구문이 동일하다고 볼 수 있다.
val length = s1?.length
```
## 엘비스 연산자

- 만약, ?.의 대상이 null일 경우 처리를 하고 싶다면 엘비스 연산자를 사용한다.
```kotlin
val s1: String? = null
val length = s1?: "---" //s1이 null이면 "---"을 반환한다.
val s2: String? = "abc"
val length2 = s2?: "---" //s2가 null이 아니면 s2를 반환한다.
```

- 연쇄 호출의 경우 안전한 호출을 사용하면, 중간 과정에서의 값이 null일 경우 모든 호출이 무시된다.
```kotlin
class Person(val name: String, val friend:Person? = null)

fun main() {
    val alice = Person("Alice")
    alice.friend?.friend?.name //alice의 친구가 null이므로, null이 반환된다.
    alice.friend?: Person("Bob") //alice의 친구가 null이므로, "Bob"이 반환된다.
}
```