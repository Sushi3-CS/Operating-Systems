# 5. 막간: 프로세스 API
## Summary
> 핵심 질문: 프로세스를 생성하고 제어하는 방법

UNIX는 프로세스를 생성하기 위하여 `fork()`와 `exec()` system call을 사용함

자신이 생성한 프로세스가 종료되기를 기다리기 원할 때 `wait()`을 사용함

## 5.1 fork() 시스템 콜

프로세스 생성에 fork() 시스템 콜이 사용됨

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
	printf("hello world (pid: %d) \n", (int) getpid());
	int rc = fork();
	if(rc < 0) {
		fprintf(stderr, "fork failed\n");
		exit(1);
	}else if(rc == 0) {
		printf("hello, I am child (pid: %d) \n", (int) getpid());
	}else {
		(main)
		printf("hello, I am parent of %d (pid: %d) \n", rc,(int) getpid());
	}
	return 0;
}
```
```
1. 프로그램 시작 시, hello world 와 프로세스 식별자(pid)가 출력됨
   - pid: 프로세스를 지칭하기 위해 사용
2. `fork()`를 호출. 생성된 프로세스는 호출한 프로세스의 복사본
   - 새로 생성된 프로세스: 자식 프로세스, 생성한 프로세스: 부모 프로세스
     - 자식 프로세스 != 부모프로세스
   - 자신의 address space, register, PC 값을 가짐
   - fork()의 반환값이 다름: 부모는 생성된 자식 프로세스의 PID, 자식은 0
```
- CPU scheduler
  - 실행할 프로세스를 선택
  - 어느 프로세스가 먼저 실행될 지 모르는 nondeterminism으로 인해 멀티 쓰레드 프로그램에서 문제 발생

## 5.2 wait() 시스템 콜

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main(int argc, char *argv[])
{
	printf("hello world (pid: %d) \n", (int) getpid());
	int rc = fork();
	if(rc < 0) {
		fprintf(stderr, "fork failed\n");
		exit(1);
	} else if(rc == 0) { // 자식 프로세스
		printf("hello, I am child (pid: %d) \n", (int) getpid());
	} else { // 부모 프로세스
		(main)
		int rc_wait = wait(NULL);
		printf("hello, I am parent of %d (rc_wait: %d, pid: %d) \n", rc, rc_wait, (int) getpid());
	}
	return 0;
}
```

- 부모 프로세스가 자식 프로세스의 종료를 대기하기 위해 `wait()` 시스템 콜을 호출
- 자식 프로세스가 종료되면 wait()는 리턴

이 코드에서는 항상 자식 프로세스가 먼저 출력을 수행함.

## 5.3 exec() 시스템 콜

자기 자신이 아닌 다른 프로그램을 실행해야할 때 사용함
- fork()는 자신의 복사본을 생성, exec()은 다른 프로그램 실행

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/wait.h>

int main(int argc, char *argv[])
{
	printf("hello world (pid: %d) \n", (int) getpid());
	int rc = fork();
	if(rc < 0) { //fork 실패
		fprintf(stderr, "fork failed\n");
		exit(1);
	}else if(rc == 0) { // 자식 프로세스
		printf("hello, I am child (pid: %d) \n", (int) getpid());
		char *myargs[3];
		myargs[0] = strdup("wc"); //프로그램 'wc'
		myargs[0] = strdup("p3.c");	//인자: 단어 셀 파일
		myargs[0] = NULL; // 배열 끝 표시
		execvp(myargs[0], myargs); // wc tlfgod
		printf("this shouldn't print out");
	}else { // 부모 프로세스
		int rc_wait = wait(NULL);
		printf("hello, I am parent of %d (rc_wait: %d, pid: %d) \n", rc, wc, (int) getpid());
	}
	return 0;
}
```
```
1. 실행 파일 이름과 약간의 인자가 주어지면, 해당 실행 파일의 code와 static data를 읽어들여 현재 실행 중인 프로세스의 코드 세그먼트와 정적 데이터 부분을 덮어씀
2. heap과 stack 및 프로그램 다른 주소공간들로 다시 초기화 됨
3. 운영체제는 프로세스의 인자를 전달하여 프로그램을 실행
4. 새로운 프로세스를 생성하는 것이 아니라 현재 실행 중인 프로그램을 다른 실행 중인 프로그램으로 대체
```
## 5.4 왜, 이런 API를?

UNIX의 쉘을 구현하기 위해 `fork()`와 `exec()`을 분리해야 함. 그래야만 쉘이 `fork()`를 호출하고 `exec()`를 호출하기 전에 코드를 실행할 수 있음. 이때 실행하는 코드에서 프로그램 환경 설정과 다양한 기능을 준비함.

- 입력/출력 재지정
- 파이프 등

## 5.5 프로세스 제어와 사용자

프로세스 제어는 시그널 형태로 제공됨 &rarr; 작업 중단, 계속 실행, 종료
