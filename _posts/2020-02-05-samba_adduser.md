---
title: "samba adduser"
excerpt: "This will be the excerpt."
date: 2020-02-05
categories: 
- post
tags: 
---


# Intro

우분투 samba를 사용해서 자료 공유 중인 서버가 있다.
사용자를 추가해서 특정 폴더에만 그 사용자가 접속하도록 관리 중인데,
그 방법을 기록해 둔다.


# adduser

다음 명령어로 사용자를 추가한다.

```bash
$sudo adduser <user_name>
```

그러면 패스워드를 입력하라고 나오는데 이 때 입력하는 패스워드를 \`<user<sub>passwd</sub>>\`라고 하자.
'~/etc/group'파일 안에 다음과 같은 입력이 추가되어 있음을 확인하자.

<user<sub>name</sub>>:x:<number>:


# group

서버에 폴더별로 사용자 그룹을 지정해 두었다.
따라서 사용자 그룹에 <user<sub>name</sub>>을 추가하는 작업을 한다.

```bash
$sudo groupadd <group_name>
$sudo useradd -G <group_name> <user_name>
```

'~/etc/group'파일 안에 다음과 같은 입력이 추가되어 있음을 확인하자.

<group<sub>name</sub>>:x:<number>:<user<sub>name</sub>>


# sambda 폴더 지정

'/etc/samba/smb.conf' 파일에 다음 내용을 추가한다.

```bash
[project_name]
      path = <folder_path>
      writable = yes
      read only = no
      browseable = yes
      public = yes
      create mask = 644
      directory mask = 755
      guest ok = no
      valid users = @<group_name>
      force user = <admin_user_name>
```


# samba user 추가

다음 명령어로 samba 사용자로 <user<sub>name</sub>>을 추가한다. 
adduser로 추가할 때 적었던 패스워드를 적었는데, 다른 패스워드로 해도 되는지는 잘 모르겠다.
알게되면 추가.

```bash
$smbpasswd -a <user_name>
New SMB password:
Retype new SMB password:
```


# samba 서비스 재시작

다음 명령어로 samba 서비스를 재시작 하면 위 내용이 적용된다. 

```bash
$sudo service smbd restart
```


# Comments

ftp 서비스를 사용하는 것 보다 윈도우 사용자에게 samba 서비스가 더 사용하기 편리한 듯 하다.
윈도우 사용자는 바로가기를 만들어서 '\\\\<ip<sub>address</sub>>\\<forder<sub>name</sub>>'으로 접속하도록 만들면 편리하다.

-   참고링크 : [nil](https://citylock.tistory.com/547)


<!----- Footnotes ----->

