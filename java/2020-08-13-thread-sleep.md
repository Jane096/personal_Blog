 `Thread` 클래스에서 대부분 해당 쓰레드를 위한 것이 아닌 
JVM에 있눈 쓰레드를 관리하기 위한 용도로 사용된다. 그러나 
`sleep()` 메서드는 예외적으로 제공해주는 메서드 중 하나이다.
<br>
<br>

### sleep()
 - sleep(long mills) : 매개변수로 넘어온 시간 (1/1000초) 만큼 대기한다.
 - sleep(long mills, int nanos) : 첫번째 매개변수로 넘어온 시간 + 두번째 매개변수로 넘어온 시간
   (1/1000000000초) 만큼 대기한다.

<br>
<br>
<br>

`run()` 메서드가 끝나지 않으면 애플리케이션은 끝나지 않는다.
밑의 코드를 참고하자
<br>

```java
public class EndlessThread extends Thread {
  public void run() {
    while(true) {
      try {
        System.out.println(System.currentTimeMills());
        Thread.sleep(1000);
      } catch (InterruptedException e) {
        e.printStackTrace();
      }
    }
  }
}
```
<br>

`run()` 메서드를 확인해보면, while문이 무한대로 돌게끔 
설정을 해놓았다. 
> while문 안에서 현재시간을 밀리초 단위로 
> 출력하게 하고 `Thread` 클래스의 `sleep()` 메서드를 **static** 
> 하게 호출하여 1초간 멈추게 설정을 했다. 

<br>
<br>

한가지 더 고려해야할 점은, `Thread.sleep()` 메서드를 사용할 때는 
항상 `try-catch` 문으로 감싸주어야 한다. 
그리고 catch에서 항상 `InterruptedException`을 잡아주어야 한다.
<br>

> 왜냐하면 `sleep()` 메서드는 적어도 
> `InterruptedException`을 던질 수도 있다고 선언되어 있기 때문이다.
> 물론 그냥 Exception을 써도 무방하다 

<br>
<br>

```java
public class RunEndlessThread() {
  public static void main(String[] args) {
    RunEndlessThread sample = new RunEndlessThread();
    sample.endless();
  }
  public void endless() {
    EndlessThread thread = new EndlessThread();
    thread.start(); 
  }
}
```

<br>

```
출력결과 

1479339714270
1479339715270
1479339716270
1479339717270
1479339718270
.
.
.
.


```
<br>

이렇게 `main()` 메서드의 수행이 끝나더라도 `main()` 메서드나 
다른 메서드에서 시작한 쓰레드가 종료하지 않으면 해당 자바 프로세스는 
끝나지 않는다. 
<br>

> 하지만 데몬 쓰레드(Demon Thread) 에서는 예외적으로 
> 종료를 시킬 수 있다! 

