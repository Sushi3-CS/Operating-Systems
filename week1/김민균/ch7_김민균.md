# Chapter 7

- Workload assumptions
    
    다음과 같은 가정을 생각하자.
    
    - 각 job들은 동일한 시간 동안 실행된다.
    - 모든 job들은 동시에 시작한다.
    - 일단 시작한 job은 완료를 위해 실행된다.
    - IO 동작 등이 없이 오직 CPU만 사용한다.
    - 각 job들의 실행 시간들은 알려져 있다.
- Scheduling Metrics
    
    Turnaround time - Job이 실행을 마친 시간(T_completion)과 시스템에 도착한 시간(T_arrival)과의 차이
    
    Fairness - Job이 얼마나 기다리느냐, starvation이 얼마나 발생하느냐의 척도. 모든 Job들은 Schedular에 의해 공평하게 선택받아야 한다.
    
- First In, First Out
    
    Queue와 비슷한 형식의 Schedular이다.
    
    약간이라도 먼저 도착한 Job이 먼저 실행되는 방식이다.
    
    그러나, 하나의 Job이 아주 긴 실행 시간을 가진다면 그 이후 짧은 시간의 job들이 오랫동안 기다려야 해서 Turnaround time이 지나치게 커지는 문제가 발생한다.
    
    Convoy effect(화물차 효과 - 느린 차가 앞서 가면 그 뒤의 차 역시 느려진다).
    
- Shortest Job First(SJF, 시진핑)
    
    동시에 도착한 job들이 있다면, 이들 중 실행 시간이 가장 짧은 것부터 실행한다.
    
    다만, 실행 시간이 긴 게 먼저 들어와 실행되고 있다면, 여전히 convoy effect가 발생할 수 있다.
    
- Shortest Time to Completion First
    
    어떠한 job이 도착한 경우, 가장 빨리 끝낼 수 있는 것부터 시작한다.
    
    이는 가장 optimal한 방식이다.
    
- New Metric : Response Time
    
    Response time은 해당 프로세스가 처음 실행되는 시간과 도착한 시간 간의 차이이다.
    
    즉, 프로세스가 얼마나 빠른 시간 내에 실행을 시작하는지를 나타낸다.
    
- Round Robin
    
    CPU를 특정 시간 간격으로 나누어 프로세스에 순서대로 돌려준다. 즉, 정해진 시간(time slice)만큼 Job을 실행하고, 그 시간이 지나면 Job을 전환한다.
    
    이러한 scheduling은 fair하고, response time이 작다는 장점이 있지만, STCF에 비해 turnaround time은 늘어난다.
    
- Incorporating I/O
    
    앞선 가정에서 모든 Job들은 CPU만을 사용한다고 하였다.
    
    다만, 실제로는 여러 상황에서 I/O를 기다리게 된다 - 다른 장치의 입력, 네트워킹 등…
    
    따라서 하나의 프로세스가 I/O 동작 중이라면 OS는 이를 확인해 해당 프로세스에 갈 자원을 다른 프로세스에 돌릴 수 있다.
    
    I/O 동작이 끝난다면 OS는 이를 확인해 다시 해당 프로세스에 자원을 할당해야 한다.
    
- No More Oracle
    
    앞서 STCF는 해당 프로세스가 끝날 때까지 걸리는 시간을 확실히 알 수 있었다.
    
    물론, 실제로는 그렇지 않아 STCF나 SJF을 제대로 실행시킬 수 없다.
    
    또한, RR에서 time slice를 어떻게 설정할지도 정해야 한다.