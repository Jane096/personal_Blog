## 제너릭 선언시 사용하는 타입의 범위 지정하는 방법

제너릭을 사용할 때, <> 안에는 어떤 타입을 넣어도 상관이 없다. 그러나 
**wildcard**로 사용하는 타입은 제한이 가능하다.

<br>
<br>

**?** 대신 `? extends 타입`의 형태로 써준다면 해당 타입으로 제한을 걸 수 있다. 

<br>

```java
public class Car {
  protected String name;
  
  public Car(String name) {
    this.name = name;
  }
  
  public String toString() {
    return "Car name="+name;
  }
}
```

<br>

`Car` 클래스를 상속받은 `Bus` 클래스를 살펴보자

```java
public class Bus extends Car {
  public Bus(String name) {
    super(name);
  }
  
  public String toString() {
    return "Bus name=" + name;
  }
}
```

<br>

`CarWildcardSample` 클래스를 만들어 컴파일이 잘 되는지 확인해보자
<br>
<br>

```java
public class CarWildcarSample {
  public static void main(String args[]) {
    CarWildcardSample sample = new CarWildcardSample();
    sample.callBoundedWildcardMethod();
  }
  
  public void callBoundedWildcardMethod() {
    WildcardGeneric<Car> wildcard = new WildcardGeneric<Car>();
    wildcard.setWildcard(new Car("Mustang"));
    boundedWildcardMethod(wildcard);
  }
  
  public void boundedWildcardMethod(WildcardGeneric<? extends Car> c) {
    Car value = c.getWildcard();
    System.out.println(value);
  }
}
```

<br>

원래 wildcard 형태인 ? 는 어떤 타입이 오더라도 상관이 없다. 그러나 이렇게
**? extends Car** 라고 형태를 바꿔서 입력해주게 되면 `Car`를 상속받은 모든 클래스를 사용할 수 있다는 의미이다. 
즉, 이외의 타입으로 제너릭을 선언한 객체가 넘어올 수 없고, 무조건 **Car** 클래스와 관련있는 클래스만이 넘어올 수 있다.
<br>
<br>

`main()` 메서드에서 `callBoundedWildcardMethod()` 를 호출하도록 실행하면 아래와 같은 결과를 얻게 된다. 
<br>

```console
Car name = Mustang
```

<br>
<br>
<br>
<br>
<br>





















