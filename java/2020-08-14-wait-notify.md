**Thread** 클래스에 선언된 메서드 중에서 쓰레드를 통제하는 
메서드가 있다. 주로 `Object` 클래스에 선언되어 있는 메서드인데, 
`wait()` 과 `notify()`, `notifyAll()` 이 해당한다.
<br>
<br>

## wait()

`wait()`은 진행 중인 쓰레드를 대기상태로 만드는 메서드이다. 
`wait()`에서 깨어나기 위해 제공하는 메서드가 `notify()` 
`notifyAll()` 이다. 

<br>

```java
public class StateThread extends Thread {
  private Object monitor;

  //constructor
  public StateThread() {
    this.monitor = monitor;
  }
  public voif tu
}
```
