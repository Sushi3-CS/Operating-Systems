# Chapter 8

- MLFQ : Basic Rules
    
    MLFQ는 각 Job에 Priority를 두어, 여러 개의 Queue에 분류해 둔다. 높은 Priority를 가진 Queue에 담긴 Job을 먼저 실행하며, 동일한 Queue의 Job은 RR 방식을 따라 실행한다.
    
    즉, MLFQ에서 가장 중요한 것은 priority를 결정하는 것이다.
    
- How to Change Priority
    
    약간의 Rule을 추가하자.
    
    - 처음 들어온 Job은 그 행동을 알아보기 위해 가장 높은 우선순위에서 시작한다.
    - 만약 RR 방식으로 실행하며 정해진 time slice를 모두 채운다면 우선순위를 내린다. 그렇지 않고 I/O 행동을 위해 time slice를 모두 채우지 못한다면 그대로 내버려 둔다.
    
    그러면 모든 job들은 RR에 따라 어느 정도 fair하게 동작하며, I/O가 자주 일어나는 job이 높은 priority를 가짐에 따라 더욱 효율적인 동작이 가능하다.
    
    다만, 몇 가지 문제가 남아 있다.
    
    - Starvation - 위 규칙에 따르면 CPU만 사용하는 Job들은 실행할수록 우선순위가 낮아진다. 즉, 긴 시간 동안 실행되는 Job은 선택될 확률이 지나치게 줄어든다.
    - 규칙 악용 - 중간중간 CPU를 일부러 내려놓으면 높은 우선순위를 유지할 수 있다.
    - 실행 패턴 변화 - CPU만 쓰다가 I/O를 실행하게 되더라도 높은 우선순위로 이동할 수 없다.
- The Priority Boost
    
    일정 시간마다 모든 job들을 최상위 priority로 올린다. 이러면 모든 job은 최소한의 시간 동안은 작동이 보장된다.
    
- Better Accounting
    
    어떤 job이 time slice를 모두 사용하였는가가 아닌, 정해진 만큼 시간을 쓴다면 priority가 낮아진다.