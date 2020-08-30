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

<br>
<br>

```java
private void checkOptionalData() {
  System.out.println(Optional.of("present").isPresent()); //첫번째
  System.out.println(Optional.ofNullable(null).isPresent()); //두번째
}
```
<br>

첫번째는 true를, 두번째는 false를 리턴하게 되어있다. 
만약 값을 꺼내고 싶다면 `get()`, `orElseGet()`, `orElse()`, `orElseThrow()` 를 사용하면
데이터를 리턴받을 수 있다. 

<br>
<br>

```java
private void getOptionalData(Optional<String> data) throws Exception {
  String defaultValue = "default";
  String result1 = data.get(); //가장 많이 사용되는 메서드, 데이터가 없다면 null 리턴
  String result2 = data.orElse(defaultValue); //값이 없다면 이 메서드를 사용하여 기본값을 설정할 수 있다.
  
  Supplier<String> stringSupplier = new Supplier<String>() {
    @Override
    public String get() {
      return "java!";
    }
  };
  
  String result3 = data.orElseGet(stringSupplier); //Supplier<T>라는 인터페이스를 활용하는 방법으로 orElseGet을 사용할 수 있다.
  Supplier<Exception> ExceptionSupplier = new Supplier<Exception>() {
    @Override 
    public Exception get() {
      return new Exception();
    }
  };
  String result4 = data.orElseThrow(exceptionSupplier); //데이터가 없어 예외발생시키고 싶은 경우 사용할 수 있다.
}
```
<br>

`Supplier<T>` 는 람다 표현식에서 사용하려는 용도로 만들어졌고, `get()` 메서드가 선언이 되어 있다. 

<br>
<br>
<br>

## Optional이 필요한 경우는 언제일까?

`Optional`클래스는 null처리보다 간편하게 하기 위해 만들어진 클래스이다. 
개발자의 실수로 `NullPointerException`을 발생시킬 수 있는데 Optional을 이용하면 
보다 간편하고 명확하게 처리가 가능해진다.

> 하지만, Optional 클래스를 잘못 사용하면 `NoSuchElementException`이 
> 발생할 수 있으니 조심하도록 하자













