보통 **optional** 의 의미는 '선택적인' 이라는 의미이다.
자바에서도 의미 그대로 무언가를 선택적으로 처리할 수 있다. 
<br>

`Optional`은 functional 언어인 Haskell과 Scala에서 
제공하는 기능을 그대로 따온 것이다. 객체를 간편하게 처리하기 
위해서 만들어진 기능이라 보면 된다. 
<br>
<br>

```java
public final clss Optional<T> {
  extends Object
}
```
<br>

`Optional`선언부분을 보면 final키워드가 있고 Object를 
상속받았으며 Generic한 클래스임을 알 수 있다. 
<br>
<br>

`final`변수는 변경이 불가능 하지만, `final`로 선언했다고
해서 내용변경이 불가능한 것은 아니다. 대신, 추가적인 확장이 
불가능하기 때문에 자식 클래스도 당연히 만들 수 없다. 
<br>
<br>

`Optional`은 일종의 깡통이라고 생각하면 된다. 물건이 있을 
수도 있고, 없을 수도 있다. 그래서 기본적인 깡통을 만들기 위해 
`new Optional()` 이용해 객체를 생성하지 않는다. 
<br>
<br>

## 객체를 생성하는 방법

```java
private void createOptionalObjects() {
  Optional<String> emptyString = Optional.empty(); //데이터가 없는 Optional 객체를 생성하려면 empty()사용해야함
  String common = null;

  Optional<String> nullableString = Optional.ofNullable(); //만약 null이 추가될 수 있는 상황이라면 사용해야하는 메서드
  common = "common";

  Optional<String> commonString = Optional.of(common); //반ㄷ시 데이터가 들어가야 하는 상황이라면 사용해야하는 메서드
} 

```
<br>

이렇게 `Optional` 클래스의 객체를 생성하는 방법은 위의 
세가지이다. Optional 클래스가 비어있는지 아닌지를 판단하는 
메서드는 `isEmpty()` 와 `isPresent()`메서드가 있다. 















