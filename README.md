# 운영체제 스터디

![OSTEP.jpg](./cover_image.jpg)

## 📖 교재

- **Operating Systems: Three Easy Pieces (OSTEP)**

- [원서](https://pages.cs.wisc.edu/~remzi/OSTEP/) | [한글 번역서](https://product.kyobobook.co.kr/detail/S000001732402)

## 📜 스터디 진행 방식

- [깃헙 Repository]()에 각자 각 장별로 공부한 내용을 정리합니다.
- 단, 바로 main 브랜치에 push 하는 것이 아니라 PR을 생성해서 다른 팀원들에게 review 요청합니다.
- 다른 팀원들이 모두 approve 하면 PR merge해주세요.
- 각자 다른 팀원들 글을 review 하면서 잘못되었거나 부족해 보이는 부분에 대해 부담없이 comment로 보충하고 토의했으면 좋겠습니다.
- 오프라인 미팅은 매주 일요일 오후 14시에 진행합니다.
- 미팅은 진도별로 각자 공부했던 내용에 대해 공유하는 자리입니다.
- 발표에 대한 자세한 내용은 아래를 참고해주세요.

## 🎙 발표

- 각 장별로 (사이즈가 작으면 여러장) 한 명씩 발표하되, 발표자 제외 다른 팀원들도 물론 공부해와야 합니다.
- 발표 길이는 길지 않아도 무방합니다. (훑는 정도여도 무방, 발표 부담을 줄이기 위해)
- 발표 부담을 줄이는 대신, 모든 팀원들이 각 장별로 공부한 내용에 대해 할 말들을 좀 준비해왔으면 좋을 것 같습니다.

| Week | 일정          | 내용                                                         | 발표자                   | 교재 챕터 |
| ---- | ------------- | ------------------------------------------------------------ | ------------------------ | --------- |
| 1    | 9/11          | Introduction to Operating Systems, The Process, Process API<br/>Limited Direct Execution, Scheduling: Introduction, MLFQ | 1. 김현준<br />2. 방형욱 |           |
| 2    | 9/18          | Scheduling: Proportion Share, Multiprocessor Scheduling, Address Spaces<br/>Memory API, Address Translation, Segmentation | 1. 김민균<br />2. 김건희 |           |
| 3    | 9/25          | Free-Space Management, Paging: Introduction<br/>Paging: Faster Translations, Smaller Tables, Mechanisms<br/>Swapping: Policies, Concurrency, Thread API | 1. 박정환<br />2. 박성현 |           |
| 4    | 10/9 (비대면) | Locks, Lock-based Concurrent Data Structures<br/>Condition Variables, Semaphores | 1. 김현준<br />2. 방형욱 |           |
| 5    | 10/16         | Common Concurrency Problems, I/O Devices<br/>Hard Disk Drives, RAIDs | 1. 김민균<br />2. 김건희 |           |
| 6    | 10/30         | File and Directories, File System Implementation<br/>Locality and The Fast File System, Crash Consistency<br/>Log-structured File Systems, Flash-based SSDs | 1. 박정환<br />2. 박성현 |           |





## 🗂 GitHub File Convention

- 각 챕터별 디렉토리에 각자 정리한 내용을 올려주세요.
- 디렉토리명은 해당 챕터명입니다. (e.g. `Chapter 3 - 가상화에 관한 대화`)
- markdown 파일은 `chap1_읍읍읍.md`으로 생성해주세요.
- markdown에 필요한 에셋들은 챕터별 디렉토리 안에 asset 디렉토리를 따로 생성해서 거기에 올려주세요.

## 🖋 PR

- PR 만드실 때 브랜치는 master에서 `chap1_읍읍읍`으로 생성해주세요.
- PR title 이나 commit title 은 자유롭게 작성해주세요.

## 🥤불참 패널티

- 불참 OR 해당 주차 학습을 못했을 시 해당 주차 혹은 그 다음 주차에 커피 한잔씩 돌리기