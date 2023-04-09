# 2023 기술 면접 스터디
DB, OS, 네트워크 스터디

<details>
<summary>:fire: 스터디 목표</summary>
<div markdown="1">
    <ul>
           <li>스터디원 전원이 매주 6가지 키워드에 대해 공부해오고, 그 중 1가지 키워드씩 발표를 진행함으로써 CS 지식을 복습한다.</li>
           <li>질문하고, 답변하는 연습을 한다.</li>
    </ul>
</div>
</details>

<details>
<summary>:star: 스터디 방식</summary>
<div markdown="1">
    <ul>
           <li>매주 토요일 24시까지 : git에 담당 파트 내용 올리고 PR</li>
           <li>매주 일요일 24시까지 : 다른 스터디원들의 자료 확인 후 댓글로 질문 달기 (질문에 대한 답변은 스터디 질의 응답 시간에 제공)</li>
           <ul>
               <li>마지막으로 댓글단 사람이 merge 하기</li>
           </ul>
           <li>매주 월요일 12시 ~ 14시 : 스터디 진행</li>
           <ul>
               <li>준비해온 자료로 내용 설명 및 발표 (5분~10분)</li>
               <li>질의 응답 (10분~15분)</li>
           </ul>
       </ul>
</div>
</details>

<details>
<summary>:white_check_mark: 스터디 규칙</summary>
<div markdown="1">
    <ul>
           <li>매주 브랜치 파서 아래와 같은 형식으로 담당 파트 내용 올리고 PR 올리기</li>
            <pre><code>
Operating System(dir)
|____README.md (과목당 기본 마크다운 파일)
|
|____트랜잭션(dir)
             |____README.md
             |____img1.png
             |____img2.png
             </code></pre>
           <li>브랜치명은 <code>Week#-깃헙아이디</code> -> 예시: <code>Week1-ssssujini99</code></li>
           <li>PR명은 <code>Week#-제목</code> -> 예시: <code>Week1-트랜잭션</code></li>
           <li>커밋명은 <code>Docs: #주차 과목 - 주제</code> -> 예시: <code>Docs: 1주차 Operating System - 스레드 안전</code></li>
    </ul>
</div>
</details>

<details>
<summary>:raising_hand: 팀원</summary>
<div markdown="1">
    <table>
  <thead align="center">
    <tr>
      <td><b>김담원</b></td>
      <td><b>김성겸</b></td>
      <td><b>신예진</b></td>
      <td><b>이수진</b></td>
      <td><b>이지은</b></td>
      <td><b>추서연</b></td>
    </tr>
  </thead>
  <tbody align="center">
    <tr>
      <td><img src="https://avatars.githubusercontent.com/u/106096303?v=4" width=200px></a></td>
      <td><img src="https://avatars.githubusercontent.com/u/76910498?v=4" width=200px></a></td>
      <td><img src="https://avatars.githubusercontent.com/u/78442839?v=4" width=200px></a></td>
      <td><img src="https://avatars.githubusercontent.com/u/71487608?v=4" width=200px></a></td>
      <td><img src="https://avatars.githubusercontent.com/u/97334255?v=4" width=200px></a></td>
      <td><img src="https://avatars.githubusercontent.com/u/83302344?v=4" width=200px></a></td>
    </tr>
  </tbody>
</table>
</div>
</details>

<details>
<summary> 🔖 레퍼런스 </summary>
<div markdown="1">
    <ul>
        <li>https://github.com/gyoogle/tech-interview-for-developer</li>
        <li>https://github.com/WeareSoft/tech-interview</li>
        <li>https://github.com/shinhee-rebecca/2022-cs-study</li>
    </ul>
</div>
</details>

## :computer: OS
- [프로세스와 스레드의 차이(Process vs Thread)](https://github.com/23-study/23-CS-Study/tree/main/Operating%20System/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EC%99%80%20%EC%8A%A4%EB%A0%88%EB%93%9C%EC%9D%98%20%EC%B0%A8%EC%9D%B4(Process%20vs%20Thread))
- [멀티 프로세스 대신 멀티 스레드를 사용하는 이유](https://github.com/23-study/23-CS-Study/tree/main/Operating%20System/%EB%A9%80%ED%8B%B0%20%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%20%EB%8C%80%EC%8B%A0%20%EB%A9%80%ED%8B%B0%20%EC%8A%A4%EB%A0%88%EB%93%9C%EB%A5%BC%20%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%20%EC%9D%B4%EC%9C%A0)
- [스레드 안전(Thread-Safety)](https://github.com/23-study/23-CS-Study/tree/main/Operating%20System/%EC%8A%A4%EB%A0%88%EB%93%9C%20%EC%95%88%EC%A0%84)
- [동기화 객체의 종류](https://github.com/23-study/23-CS-Study/tree/main/Operating%20System/%EB%8F%99%EA%B8%B0%ED%99%94%20%EA%B0%9D%EC%B2%B4%EC%9D%98%20%EC%A2%85%EB%A5%98)
- [뮤텍스와 세마포어의 차이](https://github.com/23-study/23-CS-Study/tree/main/Operating%20System/%EB%AE%A4%ED%85%8D%EC%8A%A4%EC%99%80%20%EC%84%B8%EB%A7%88%ED%8F%AC%EC%96%B4%EC%9D%98%20%EC%B0%A8%EC%9D%B4)
- [스케줄링](https://github.com/23-study/23-CS-Study/tree/main/Operating%20System/%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81)

## :floppy_disk: DB
- [데이터베이스 풀](https://github.com/23-study/23-CS-Study/tree/main/Database/Database%20POOL)
- [정규화(1차 2차 3차 BCNF)](https://github.com/23-study/23-CS-Study/tree/main/Database/%EC%A0%95%EA%B7%9C%ED%99%94(1%EC%B0%A8%202%EC%B0%A8%203%EC%B0%A8%20BCNF))
- [트랜잭션](https://github.com/23-study/23-CS-Study/tree/main/Database/%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98)
- [트랜잭션 격리 수준(Transaction Isolation Level)](https://github.com/23-study/23-CS-Study/tree/main/Database/%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98%20%EA%B2%A9%EB%A6%AC%20%EC%88%98%EC%A4%80)
- [Join](https://github.com/23-study/23-CS-Study/tree/main/Database/%EC%A1%B0%EC%9D%B8)
- [SQL injection](https://github.com/23-study/23-CS-Study/tree/main/Database/SQL%20injection)

## :satellite: Network
- [OSI 7계층](https://github.com/23-study/23-CS-Study/tree/main/Network/OSI%207%EA%B3%84%EC%B8%B5)
- [TCP/IP의 개념](https://github.com/23-study/23-CS-Study/tree/main/Network/TCP/IP%EC%9D%98%20%EA%B0%9C%EB%85%90)
- [TCP와 UDP](https://github.com/23-study/23-CS-Study/tree/main/Network/TCP%EC%99%80%20UDP)
- [TCP와 UDP의 헤더 분석](https://github.com/23-study/23-CS-Study/tree/main/Network/TCP%EC%99%80%20UPD%EC%9D%98%20%ED%97%A4%EB%8D%94%20%EB%B6%84%EC%84%9D)
- [TCP의 3-way-handshake와 4-way-handshake](https://github.com/23-study/23-CS-Study/tree/main/Network/TCP%EC%9D%98%203-way-handshake%EC%99%80%204-way-handshake)
- [HTTP와 HTTPS](https://github.com/23-study/23-CS-Study/tree/main/Network/TCP%EC%9D%98%203-way-handshake%EC%99%80%204-way-handshake)
