자바 JDK8 부터 추가 된 기능 중에 `stream` 이라는 기능이 있다. 
영어로 직역하자면, **개울, 시내** / **줄기** / **(사람이나 차량등으로 이어진) 줄** 
이런 의미가 존재한다. 
<br>
<br>

## Stream은 언제 사용할까?

자바에서 `stream`은 **"무언가 연속 된 정보"** 를 처리하는데 사용한다. 
`stream` 이전에 연속된 정보를 처리하는 기능은 배열이나 컬렉션이다. 
<br>

`stream`은 배열에 직접적으로 사용이 불가능하다. 하지만 배열을 `List`로 변환하는 
`asList()`를 제공한다. 
<br>
<br>
<br>

## Stream의 구조

`stream`은 아래와 같은 구조를 가진다. 
<br>

```java
list.stream().filter(x -> x>10).count()
     생성        중개연산        종단연산
```
<br>

- 컬렉션의 목록을 스트림 객체로 변환한다. 스트림 객체는 `java.util.stream` 패키지의 
`Stream` 인터페이스를 말하며 `stream()` 메서드는 당연히 `Collection` 인터페이스에 선언되어 있다. 
- 중개연산: 생성된 스트림 객체를 사용해서 중개 연산 부분을 처리한다. 이 부분에서는 아무것도 
리턴하는 것이 없기 때문에 중개연산(intermediate operation) 이라고 말한다. 
- 종단연산: 중개연산에서 작업된 내용을 바탕으로 결과를 리턴하는 부분이다. 그래서 이 부분은
종단연산(terminal operation) 이라고 부른다. 

<br>
<br>

여기서 중개 연산은 반드시 필요한 부분은 아니다. 
그리고 `stream()`은 순차적으로 데이터를 처리한다. 만약 10개의 데이터가 있다면 
0~9까지의 인덱스를 순서대로 처리한다는 의미이다. 
<br>

`stream()` 보다 빠른 처리를 제공하는 `parallelStream()` 이라는 메서드도 제공이되는데 
병렬로 처리하는 까닭에 CPU도 많이 잡아먹고 몇개의 쓰레드로 처리할지도 보장이 안되기 때문에 
일반적인 웹 프로그램에서는 권장하지 않는다고 한다. 
<br>
<br>
<br>

## 많이 사용하는 메서드 map()

`map()`은 `filter()` 와 함께 중개연산에 속하는 기능이다. 
이 기능은 데이터를 특정 데이터로 변환하는 역할을 한다. 
다음과 같이 List가 있다고 가정해보자 
<br>

```java
List<Integer> intList = Arrays.asList(1,2,3,4,5,6,7,8,9,10);
```
<br>

위의 intList를 모두 3의 3배수로 변환해서 출력할려면 가장 기본적인 방법 중엔
for 루프가 있다. 
<br>
<br>

```java
private void multiplyWithFor(List<Integer> intList) {
  for(int value:intList) {
    int tmpValue = value * 3;
    System.out.println(tmpValue);
  }
}
```
<br>

이걸 stream을 이용해 보면 이렇게도 바꿀 수 있다. 
<br>
<br>

```java
intList.stream().forEach(value -> System.out.println(value * 3));
```
<br>

이제 스트림으로 값들의 3배를 출력할 수 있다. 하지만, 만약에 3배로 변환된 값들의 
합을 구한다고 생각하면 조금 복잡해질 수 있다. 이럴 때 스트림의 값 자체를 변경해버리는 
`map()` 을 사용하면 편리하다. 
<br>

```java
intList.stream().map(x -> x*3).forEach(System.out::println);
```
<br>

중간에 `map(x -> x*3)` 이라는 구문이 추가되었다. 이렇게 `map()`으로 변환이 되면 
해당 스트림의 다음 구문에 있는 내용도 바뀌어야 한다. 
즉, 이렇게 `map()`을 사용하면 스트림에서 처리하는 값들을 중간에 변경을 할 수가 있다. 
<br>
<br>

`map()`은 꼭 숫자만이 아니라 객체로 변환이 가능하다. 
<br>

```java
List<StudentDTO> studentList = new ArrayList<>();
studentList.add(new studentDTO("요다", 43, 99, 10);
studentList.add(new studentDTO("만두", 30, 71, 85);
studentList.add(new studentDTO("건빵", 32, 81, 75);
```
<br>

만약 이 `studentList`에서 이름만을 List로 빼내야 한다고 생각해보자.
대부분 for문을 사용하겠지만, 스트림을 사용하면 아래와 같이 표현할 수 있다. 
<br>
<br>

```java
List<String> nameList = studentList.stream()
     .map(student -> student.getName()).collect(Collectors.toList());
```
<br>

중간에 이렇게 `map()` 을 사용해서 학생의 이름을 뽑아냈고, 그 결과를 `collect()` 메서드를 사용하여 
`toList()`를 통해 List로 변환을 했다. 
<br>

`collect()`는 모든 값들을 한 곳으로 모으는 대표적인 **종단 연산** 이다. 그래서 이 메서드를 사용하면 
위의 코드블럭처럼 한꺼번에 List로 변환이 가능하다. 
















