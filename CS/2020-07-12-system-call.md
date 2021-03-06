---
title: "[운영체제] 운영체제의 간단한 구조 "
layout: single    
read_time: true    
comments: true   
categories: 
 -  
toc: true    
toc_sticky: true    
toc_label: contents    
description: 커널모드와 사용자모드의 차이와 사용자모드에서 커널모드를 호출해 사용하는 법
last_modified_at: 2020-07-12       
---

## 운영체제 구조

운영체제의 큰 구조

- 커널모드 : 파일을 읽기나 쓰기, 화면에 메세지를 출력하는 등 많은 부분을 관여
- 사용자 모드 : 유저가 접근할 수 있는 영역의 제한이 있는 모드, 이 모드에서는 프로그램 자원의 접근이 불가능하다


> 프로세스가 실행되는 동안 프로세스는 수없이 사용자모드 <-> 커널모드를 왔다갔다 하며 실행을 하게 된다.
> open()이란 라이브러리를 호출할 때에도 시스템 콜에 의해 커널모드로 넘어가 open을 호출하며 유저모드로 리턴값을 반환해준다.


<br>
<br>
<br>


### 시스템 콜

응용프로그램이 운영체제 기능을 요청하기 위해서 사용하는 것으로 운영체제가 제공한다.     
커널의 기능을 사용자 모드에서 사용할 수 있도록 함, 통상적으로는 여러 종류로 나뉘어져 있다.
쉘(shell)이 커널과 사용자 사이의 인터페이스를 제공해 쉘 명령어로 운영체제의 기능을 호출할 수 있다. 

<br>
<br>
<br>


#### 시스템 콜의 유형

- 프로세스 제어(끝내기, 중지, 적재, 실행..등)
- 파일조작(파일 생성, 삭제, 열기, 닫기, 읽기, 쓰기....)
- 장치관리(장치요구, 장치 방출, 장치 속성획득, 속성설정)
- 정보 유지(시간과 날짜 설정, 시스템 데이터 설정과 획득)
- 통신(통신 연결의 생성, 제거, 메세지 송 수신, 상태 정보전달)


<br>
<br>
<br>




### 쉘(Shell)

영어로 직역하자면 '껍데기'이다. 즉, 운영체제는 쉘을 통해 사용자 인터페이스를 제공한다.     
운영체제는 컴퓨터 하드웨어와 응용프로그램을 관리하고 
우리가 흔히 알고있는 터미널 환경이 CLI환경이고 GUI는 마우스가 나오며 생긴
인터페이스 이다. 
<br>
<br>
<br>




### 커널(Kernel)

영어로 직역하면 '중심'의 의미를 담고있으며, 특정한 권한이 없이는 접근이나 사용이 불가능하다.    
자원의 효율적인 관리를 위해 파일의 입출력이나 프로세스 관리 등 운영체제의 기능을 담당하는 중요한 일을 수행한다. 
이에 접근하기 위해 제공되는 것이 **시스템 콜(system call)** 이다(일종의 다리역할)

<br>
<br>
<br>


### API(Application Programming Inteface) 

사용자 뿐만 아니라 응용프로그램을 위해서도 인터페이스가 운영체제로부터 제공이된다. 

응용프로그램을 사용하거나 만들면서 운영체제의 무언가를 요청할 일이 많기 때문에 API라는 형태로 응용프로그램을 위한 인터페이스를 제공한다. 

주로 라이브러리 형태의 함수로 제공이된다 ex)  **open()** (이와 비슷한 방식으로) 

API는 각 언어별로 운영체제 기능 호출 인터페이스 함수인 것이다. (즉, 내부에서는 시스템 콜을 호출하는 형태로 만들어지는게 일반적이다.)

<br>
<br>
<br>
<br>
<br>
<br>
