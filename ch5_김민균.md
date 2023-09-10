# Chapter 5

- fork
    
    각각의 프로세스에는 Process Identifier, 즉 PID가 존재한다.
    
    프로세스 내에서 fork를 실행하면 OS는 이와 거의 유사한 새로운 프로세스 하나를 실행한다. 새로운 프로세스는 fork가 호출된 시점에서부터 실행을 시작한다.
    
    fork의 반환값이 0이면 이는 child process, 즉 새로운 프로세스임을 의미한다. 0이 아닌 양수이면 반환값이 곧 child process의 PID이며, 음수이면 fork 함수 에러이다.
    
    child와 parent 간의 실행 순서는 결정되지 않았다. Scheduler의 상태에 따라 비결정적인 형태로 실행되기에, 일종의 Concurrency 문제가 발생할 수 있다.
    
- wait
    
    wait 함수가 실행되면 해당 프로세스는 child의 실행이 끝날 때까지 기다린다. 반환값은 child process의 PID이다.
    
- exec
    
    다른 프로그램을 실행한다.
    
- Motivating the API
    
    왜 fork와 exec는 분리되어 있는가? → shell은 fork 이후에, exec 이전에 실행된다.
    
    즉, 무언가 프로그램을 실행할 때, fork를 사용해 새로운 프로세스를 만들고, 이후 exec를 사용해 쉘에서 실제 command를 실행한다.
    
    <aside>
    🕊️ prompt> wc p3.c > newfile.txt
    
    </aside>
    
    위 명령어를 보자. 프로그램 wc의 출력은 newfile.txt에 저장된다.
    
    이에 따르면 child process가 생성된 이후, shell은 exec로 명령어가 실행되기 이전 standard output을 닫은 후 newfile.txt로 연결한다.
    
- Process Control and Users
    
    fork, exec, wait을 제외하고도 UNIX System에는 여러 interface가 존재한다.
    
    예를 들어, kill은 process에 signal을 보내 정지시키거나, 강제로 종료하는 등 여러 행동이 가능하다.
    
    이러한 signal들은 여러 외부 입력에 대한 처리를 가능하게 한다. 프로그램 내에 signal system call을 사용해 구현할 수 있다.
    
- Useful Tools
    - ps : 프로세스 실행 상황
    - top : 프로세스 표기 및 리소스 상황
    - killall : 모든 프로세스 종료