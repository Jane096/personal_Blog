`synchronize` 라는 단어는 자바의 예약어 중 하나이다. 
즉, 변수명이나 클래스명으로 사용을 할 수가 없다. 
<br>
<br>

**Thread** 에서 synchronize 라는 단어는 아주 밀접한 
관계를 가지고 있다. 
**쓰레드에 안전하다** 라는 말이 바로 이 synchronize 
단어와 연결된다. 어떠한 클래스나 메서드가 쓰레드에 안전할려면 
이 예약어가 반드시 필요하다. 
<br>
<br>
<br>

## synchronize를 사용하는 두가지 방법

- 메서드 자체에 synchronize를 선언하는 방법
- 메서드 내에 특정 문장만 synchronize로 감싸는 방법

<br>
<br>
<br>

### 메서드를 synchronize로 선언하는 방법

```java
public void plus(int value) {
  amount += value;
}
```
<br>

위의 메서드를 synchronize로 선언하면 아래와 같이 바뀌게 된다.
<br>

```java
public synchronize void plus(int value) {
  amount += value;
}
```
<br>

이렇게 메서드에 synchronize가 선언되어 있다면 동일한 객체에 
여러개의 쓰레드가 접근해도 한 순간에는 하나의 쓰레드만이 해당 
메서드를 실행할 수 있게 된다. 
<br>
<br>
<br>

```java
public class Calculator {
  private int amount;
  
  public Calculator(){
    amount = 0;
  }

  public void plus(int value) {
    amount += value;
  }
  public void minus(int value) {
    amount -= value;
  }
  public int getAmount() {
    return amount;
  }
}
```
<br>

위의 클래스는 연산을 수행하는 클래스이다. amount라는 변수가 
선언되어 있고 각 메서드에서는 매개변수를 받아 덧셈이나 뺄셈을 수행한다. 
<br>

이 클래스의 객체를 매개변수로 받는 아래의 쓰레드가 있다.
<br>

```java
public class AmountThread extends Thread {
  private Calculator calc;
  private boolean addFlag;
  
  public AmountThread(Calculator calc, boolean addFlag) {
    this.calc = calc;
    this.addFlag = addFlag;
  }
  public void run() {
    for(int loop=0; loop < 10000; loop++) {
      if(addFlag) {
        calc.plus(1);
      }else {
        calc.minus(1);
      }
    }
  }
}
```
<br>

맨 처음 만든 `Calculator` 객체를 받아서 addFlag가 
true라면 1을 더하고 그 반대라면 1을 빼는 연산을 수행한다. 
그리고나서 해당 쓰레드는 종료가 된다. 
<br>

다음의 코드블럭과 같이 쓰레드를 실행시키는 `RunSync` 
클래스를 살펴보자 
<br>
<br>

```java
public class RunSync {
  public static void main(String[] args) {
    RunSync runSync = new RunSync();
    runSync.runCalculate();
  }
 
  public void runCalculate() {
    Calculator calc = new Calculator();
    AmountThread thread1 = new AmountThread(calc, true); 
    AmountThread thread2 = new AmountThread(calc, true); 
    
    thread1.start();
    thread2.start();
    
    try{
      thread1.join();
      thread1.join();
      System.out.println("Final value is "+calc.getAmount());
      
    } catch(InterruptedException e) {
      e.printStackTrace();
    }
  }
}
```
<br>

최종적으로 `RunCalculate` 가 수행된 이후에는 
20000이라는 결과값이 나와야 한다. 
하지만
<br>
<br>

```
Final Value is 19511 
```
<br>

이 결과값은 실행할 때 마다 계속 바뀔 것이다. 
> 쓰레드에서 반복하는 횟수가 적으면 적을수록 결과값은 정답에 
> 가깝겠지만, 반복하는 횟수가 많아질 수록 정답에서 점점 멀어지게 된다.

<br>

이렇게 결과값에 멀어지게 나오는 이유는 plus() 라는 메서드 
때문인데, 이 메서드는 다른 쓰레드에서 작업하고 있다고 하더라도, 
새로운 쓰레드에서 온 작업도 같이 처리하기 때문에 데이터가 꼬일 수 있다. 
<br>
<br>

```java
 public void plus(int value) {
    amount += value;
 }
```
<br>

value 값에 amount값을 더하는 작업은 간단해 보여도 내부적으로는 복잡하다.
<br>

```
amount = amount + value;
```
<br>

연산은 우측 항의 결과를 좌측 항에 있는 amount에 담는다. 
예를들면, 우측 항에 있는 amount가 1이고 value가 1일 경우, 
정상적인 경우라면 좌측 항의 결과는 2가 되어야 한다. 
<br>

그런데 좌측항에 2을 치환하기 전에 다른 쓰레드가 들어와서 이 
연산을 수행하려고 하기 때문에 아직 2가 되지 않은 상황의 `amount = 1` 
값에서 계산을 진행하니 결론적으로 결과값이 이상하게 되는 것이다. 
<br>
<br>

```java
 public synchronized void plus(int value) {
    amount += value;
 }
 public synchronized void minus(int value) {
    amount -= value;
 }
```
<br>

이렇게 쓰레드에 안전하게 `synchronized` 를 선언해주면 현재 
쓰레드가 끝날 때까지 기다렸다가 다음을 진행하기 때문에 결과는 항상 
**20000** 이 나오게 된다.
<br>
<br>
<br>
<br>
<br>
<br>
<br>












