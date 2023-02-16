---
title : How to archive without selecting a specific directory during tar backup in Solaris 10
date : 2023-02-16 16:00:00 + 0900
categories : [SERVER, UNIX]
tags : [ solaris, archive, tar, exclude ]
render_with_liquid: false
---

# How to archive without selecting a specific directory during tar backup in Solaris 10


## 1. 'exclude_dir.list'파일 생성 
아카이빙하고 싶은 디렉토리 내에서  제외하고 싶은 디렉토리 or 파일을 리스트에 작성하여 준다. 
예를들어 '/backup_source'의 하위 디렉토리내에 A, B, C, D가 있는경우,
A와 B만 아카이빙 하고 싶은 경우 C, D를 아래와 같이 exclude list에 작성하여 준다. 

`# vi /backup_target/exclude_dir.list` 
```bash
/backup_source/C
/backup_source/D
```


## 2. Exclude List를 포함한 Tar Archiving 

형식 : tar cvpfX [Backup이 받아질 위치 및 아카이브 파일 이름] [아카이브 제외 대상 목록] [백업할 디렉토리] 

**Example>**
```
# nohup tar cvpfX /osbackup_target/backup_source_A_B.tar /backup_target/exclude_dir.list /backup_source/* >\
 /backup_target/backup_source_A_B.stdout 2> /backup_target/backup_source_A_B.stderr &
```


## APPENDIX 
### Solaris 10 Tar Options 
+ `-c`: 선택된 파일들에 대해 새로은 Tar 파일을 생성
+ `-r`: 선택된 파일들을 기존의 tar의 끝에 추가
+ `-t`: tar 파일이 저장하고 있는 파일의 리스트를 출력
+ `-u`: 선택된 파일들이 tar 파일에 없거나 또는 변경된 경우 tar파일에 추가/수정
+ `-x`: 선택된 파일들을 tar 파일로 부터 추출
+ `-b`: Tape 디바이스를 이용하여 아카이브할 때 Block Size 지정
+ `-B`: 여러번 읽어 들거나, Pipe 또는 Socket를 이용할때 한번에 읽어 드리는 데이터의 크기를 지정하거난 데이터를 읽는 횟수를 지정
+ `-e`: 예상치 않은 에러 발생시 정상 종료 값을 리턴으로 종료 
+ `-f`: 다음의 매개변수를 tar 파일의 이름으로 지정 
+ `-F`: 하나의 F 문자 지정시 SCCS(Source Code Control System) 모두 배제. 두개의 FF 문자 지정시 확장자가 .o, .errs, .core, a.out 파일들을 모두 배제
+ `-h`: Simbolic link일 경우 실제 파일의 내용을 사용
+ `-i`: Directory checksum 에러 무시 
+ `-m`: tar 파일을 풀 때 각 파일의 수정 시간을 tar 파일을 푸는 현재 시간으로 설정
+ `-p`: umask 값을 무시하고 원래의 파일 접근 권한을 이용한다. Super User의 경우 setuid, sticky bit도 무시
+ `-v`: tar 작업의 상세 내역을 출력
+ `-w`: tar 작업 수행시 각각의 파일에 대해 작업을 수행할지에 대한 여부를 물어본다.(y이외의 문자를 입력하면 해당 파일에 대해 작업을 수행하지 않음)
+ `-X`: 다음의 매개변수를 해당 작업을 수행하지 않을 파일리스트를 가진 파일로 인식 
+ `-l`: 다음의 매개변수를 해당작업을 수행할 파일 리스트를 가진 파일로 인식 ('x' 옵션과 반대) 
+ `-C`: 'c' 또는 'r' 선택사항에서, tar 파일 안에 묶기 전에 해당 디렉토리로 이동을 한다. 결과적으로 tar 파일 안에 묶이는 파일들의 경로명이 단축 됨
