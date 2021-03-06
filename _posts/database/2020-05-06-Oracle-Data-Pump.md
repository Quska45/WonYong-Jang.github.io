---
layout: post
title: "[DB] 오라클 데이터 펌프"
subtitle: "Datapump 사용법 및 Export 와 Datapump 비교"
comments: true
categories : Database
date: 2020-02-18
background: '/img/posts/02.jpg'
---


<h2 class="section-heading">Datapump</h2>

<p>Oracle 10g 이상부터 가능한 export/import 도구로 oracle DB를 백업하거나 
복구 혹은 다른 서버로의 이전에 사용된다.</p>

<img width="525" alt="스크린샷 2020-05-06 오후 9 14 41" src="https://user-images.githubusercontent.com/26623547/81176494-2f771100-8fe0-11ea-9449-87c41cdde0c5.png">
<br/><br/>
<h3>Datapump 장점</h3>

<p><u>1. 작업을 일시 중단 시켰다가 다시 시작하는, JOB의 제어가 가능하다.</u></p>

<p><u>2. 필요한 디스크 공간 예측 가능</u></p>
exp/imp 작업도중 디스크 공간 부족으로 작업하던 것을 취소하고 용량 확보 후 다시 수행 해야 하지만, 
datapump는 ESTIMATE 파라미터를 사용해 해당 작업시 필요한 디스크 공간을 미리 알수 있다.

<p><u>3. remapping 기능 지원</u></p>
<p>스키마 변경이나 테이블 스페이스, 데이터파일 변경까지 가능하다.</p>

<h3>Datapump 단점</h3>
<p>exp로 백업한 자료는 imp로, expdb로 백업한 자료는 impdb로 해야한다. 즉, exp로 한것 impdb로 불가능하다.</p>

<h3>Data Pump 사용법</h3>

<b>Datapump 기능을 사용하기 위해서는 Directory가 생성되어 있어야 하며 datapump를 
수행하는 사용자는 그 디렉토리에 접근 권한이 있어야 한다. <br/>
아래와 같이 Directory 조회 가능하다.</b>

<p>1. Directory 생성</p>
```
 SQL> create directory  디렉토리 이름 as '/실제 물리적 경로';
 SQL> grant read, write on directory 디렉토리 이름 to 유저이름;
 // 모든 유저에게 권한 주고 싶으면 to public;
 SQL> SELECT * FROM DBA_DIRECTORIES;
```

<p>2. Datapump job 모니터링</p>
```
 select * from USER_DATAPUMP_JOBS;
 select * from DBA_DATAPUMP_SESSIONS;
```

<p>Reference</p>

<a href="https://hayleyfish.tistory.com/99">https://hayleyfish.tistory.com/99</a>
