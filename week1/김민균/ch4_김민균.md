# Chapter 4

- The Abstraction: A Process
    
    프로그램을 실행하면 프로세스
    
    ㅏㅇ직도모르면탈모
    
    프로세스는 메모리에 적재되어 있으며, 그 공간이 곧 해당 프로세스의 address space이다.
    
    program counter(PC 또는 IP)가 가리키는 위치가 곧 실행 중인 프로세스의 코드이다.
    
    이외에도 stack pointer, frame pointer 등이 해당 프로세스의 parameter들, return address, 지역변수가 담겨 있는 영역을 지정해 준다.
    
- Process API
    
    다음과 같은 종류의 API들은 대부분의 현대적인 OS에서 지원한다.
    
    - Create : 프로세스 만들기
    - Destroy : 프로세스 강제로 끝내기
    - Wait : 프로세스 끝나기를 기다리기
    - Miscellaneous Control : Destroy나 Wait이 아닌 형식으로 프로세스 컨트롤하기(일시정지 등).
    - Status : 프로세스 정보 얻기
- Process Creation: Detail Time
    
    프로그램이 어떻게 프로세스가 되는가?
    
    프로그램은 executable format으로 디스크에 저장되어 있다. 이를 실행하기 위해서는 run-time stack(또는 그냥 stack), heap 영역을 할당하고, file descriptor 초기화 등 여러 초기화 작업을 거쳐야 한다.
    
    이후 프로세스에 CPU를 할당받으면 실행이 시작된다.
    
- Process states
    
    기본적인 Process의 상태는 다음과 같이 나타낼 수 있다.
    
    - Running : 프로그램은 프로세서 내에서 실행 중이다.
    - Ready : OS가 실행하도록 하지 않았을 뿐, 언제든지 실행 가능한 상태이다.
    - Blocked : I/O operation 등의 상황으로 인해 프로세스 실행 재개가 불가능한 상태
    
    실제로 프로세스는 scheduler에 의해 상태 전환이 이루어진다. scheduler는 Ready 상태를 Running으로 바꾸고, 실행 중인 프로세스를 일시정지 시키는 등의 동작이 가능하다.
    
- Data Structure
    
    context switch, 즉 프로세스 간 전환 상황에서 각 프로세스는 레지스터 등 CPU의 여러 상태 정보를 저장할 필요가 있다.
    
    그런 당신을 위해 준비한 xv6 Proc Structure
    
    프로세스의 레지스터, 메모리 시작/끝 주소, ID 등을 간편하게 저장하세요
    
    이를 잘 활용한 Structure를 만들어 프로세스 정보를 저장할 수 있다.