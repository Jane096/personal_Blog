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

이번엔 callBusBondedWildcardMethod() 를 다음과 같이 추가하고 컴파일을 해보도록 하자
<br>

```java
public void callBusWildcardMethod() {
  WildcardGeneric<Bus> wildcard = new WildcardGeneric<Bus>();
  wildcard.setWildcard(new Bus("6900"));
  boundedWildcardMethod(wildcard);
}
```

<br>

이렇게 메서드를 추가해도 아래와 같이 결과가 잘 나오며 컴파일에 문제가 없다.
<br>

```console
Bus name = 6900
```

<br>

이와 같이 **? extends type** 과 같은 것을 **Bounded Wildcard** 라고 부른다. 
Bound 라는 영어의미는 "경계" 라고 해석할 수 있어, 매개 변수로 넘어오는 제너릭의 
**타입의 경계**를 지정한다고 생각하면 된다. 

<br>

하지만 wildcard와 마찬가지로 Bounded Wildcard 또한 값을 할당할 수 없으니 꼭 
조회용 매개 변수로만 사용해야 한다.

<br>
<br>
<br>
<br>
<br>





















