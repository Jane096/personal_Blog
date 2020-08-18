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
  public StateThread(Object monitor) { //매개변수로 monitor라는 이름의 객체를 받아 인스턴스 변수로 선언
    this.monitor = monitor;
  }
  public void run() { //쓰레드를 실행중인 상태로 만들기 위해 간단하게 루프로 String 객체 생성
    try {
      for(int loop=0; loop<10000; loop++) {
        String a = "A";
      }
      
      synchronized(monitor) { //wait() 호출
        monitor.wait();
      }
      
      System.out.println(getName()+" is notified.");
      Thread.sleep(1000); //wait()이 끝나면 1초간 대기 후 종료
    } catch (InterruptedException e) {
      e.printStackTrace();
    }
  }
}
```
<br>

밑에는 쓰레드를 실행시킬 코드들이다.

```java
public class RunObjectThreads {
  public static void main(String[] args) {
    RunObjectThreads sample = new RunObjectThreads();
    sample.checkThreadState2();
  }
  
  public void checkThreadState2() {
    Object monitor = new Object(); //StateThread에 매개변수로 넘겨줄 monitor라는 Object클래스 생성
    StateThread thread = new StateThread(monitor);
    
    try{
      System.out.println("thread state=" + thread.getState());
      thread.start(); //쓰레드 객체 생성 후 시작
      System.out.println("thread state(after start)=" + thread.getState());
      
      Thread.sleep(100);
      System.out.println("thread state(after 0.1 sec)=" + thread.getState());
      
      synchronized(monitor) {
        monitor.notify(); //monitor객체에 notify() 호출
      }
      
      Thread.sleep(100);
      System.out.println("thread state(after notify)=" + thread.getState());
      
      thread.join(); //쓰레드가 종료될 때까지 기다린 후 상태 출력
      System.out.println("thread state(after join)=" + thread.getState());
    } catch (InterruptedException e) {
      e.printStackTrace();
    }
  }
}
```
<br>

```
출력결과

thread state=NEW
thread state(after start)=RUNNABLE
thread state(after 0.1 sec)=WAITING
Thread-0 is notified
thread state(after notify)=TIMED_WAITING
thread state(after join)=TERMINATED
```

<br>

`wait()` 메서드가 호출되면 쓰레드의 상태는 WAITING이 된다. 
이 WAITING 상태에서 누군가 깨워주어야 하는데 그 기능을 담당하는 것이 
`notify()` 이다. `interrupt()` 메서드를 호출하여 대기 상태에서 벗어나게 할 수 있지만, 
`notify()` 메서드로 호출해야 `InterruptedException`이 발생하지 않고 `wait()` 이후의 
문장도 정상적으로 수행된다. 
<br>
<br>
<br>


## notifyAll()

여러개의 객체가 `wait()` 상태라면 `synchronized block`
에 `notify()` 를 객체의 갯수만큼 선언해서 풀어줘도 되지만
`notifyAll()` 이라는 기능도 제공해준다. 
<br>

말그대로 `wait()` 상태의 모든 객체를 깨워준다는 의미로 
여러개를 notify할 경우 `notifyAll()` 이 훨씬 좋은 방법이니 
알아두도록 하자 
<br>
<br>
<br>
<br>
<br>
<br>
<br>














