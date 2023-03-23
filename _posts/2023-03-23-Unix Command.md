---

layout: single
title: "[2023-03-21] Unix Command"
categories: Autonomous-Driving-Devcourse-TIL
tags: Linux
toc: true
author_profile: false
sidebar :
    nav : "docs"

---

# Unix Command

2023-03-21



## Linux(Unix) 필수 명령어

- CLI(Command Line Interface) 명령어
- 관리자용 명령어를 제외한 필수 명령어는 수십여개 정도
  - 하지만 각 명령어마다 Option의 조합으로 인해 수백개 이상의 조합이 형성됨
  - 자주 쓰는 명령어는 자연스럽게 외워짐
  - 그 외의 모르는 것들은 `man` 페이지를 참고



## Command Completion

![image](https://user-images.githubusercontent.com/116723552/227124929-7d8b8799-01a4-4cc8-a268-f2b37c8dd9f9.png)

- Auto-Completion
- `Tab` 키를 사용해서 자동완성



## i18n

- **i**<u>nternationalizatio</u>**n**의 축약형

- UTF-8이 기본문자세트로 사용

- 현재 리눅스/유닉스 Command는 i18n에 맞춰서 만들어졌음

  - 따라서 LANG 환경변수 설정의 영향을 받음

    

## Linux Basic Commands

매뉴얼 

- **man**

파일 관련(path) 

- **pwd**, **cd**, pushd/popd 

파일 관련(file data / meta-data) 

- 조회 : **ls**, **file**, **stat**, tree, which, **find**, locate
- 데이터 변경 : **cp**, **mv**, **rm**, **mkdir**, **rmdir**, **ln**, readlink
- 메타 변경 : **chmod**, **chown**, chrgp, chattr/lsattr

파일 묶음(archive)

- **tar**, cpio

압축(compress)

- **gzip**, bzip2, xz, lz4, zstd

Text 관련

- Editor : **vim(vi)**, nano, emacs
- Filter : **cat(tac)**, **head**, **tail**, **less**, more, **sort**, unique
- Regex : **grep**, **sed**, **awk**

Job Control 

- **jobs**, **fg**, **bg**, disown

Process Control

- **kill**, **pkill**, **pgrep**, killall
- tracing : **strace**, pmap

Networking

- nc, curl, wget
- w

Disk

- df(disk free), du(disk usage)

  

## Linux Admin Commands

System

- uptime, **free**, smem
- process summary : **top**, htop, atop, sar, saidar
- process status : **ps**, pstree
- stat : **vmstat**, iostat, mpstat, **pidstat**, statgrab, dstat
- hardware : **lshw**, lspci, lsusb

Package

- RedHat : rpm, **yum**, dnf
- Debian : dpkg, apt-get/apt-cache/apt-file, **apt**

Network 

- status : **ss**
- config : **nmcli**, nmtui, ip, ipconfig/route, iw/iwconfig
- arp, dig
- ssh, sftp, scp, ssh-copy-id
- packet : tcpdump, wireshark, tshark

Files 

- open files : lsof, fuser

Kernel

- Kernel Parameter : sysctl
- Kernel Module : lsmod, modprobe, rmmod

Firewall

- iptables,ip6tables
- firewall-cmd,ufw

Disks

- **fdisk**, cfdisk, sfdisk, fixparts, flock
- **parted**, gdisk, cgdisk, sgdisk
- **mkfs**, **fsck**
- **mount**, **lsblk**, **blkid**
- **grubby**, grub2-install, grub2-mkconfig, grub2-editenv
- lvs, vgs, pvs
- **udisksctl**

Security

- **ulimit**
- visudo
- sestatus, getsebool / setsebool, getenforce / setenforce
- abrt

User 

- **useradd**, **groupadd**, **usermod**, groupdel, chgrp, newgrp
- **passwd**, **chpasswd**, gpasswd

Service 

- init, service, chkconfig, ntsysv, update-rc
- **systemctl**

Performance

- tuned-adm
- perf
- pcp

Locale 

- locale, localectl

Alternatives

- update-alternatives

  

## Linux Dev. Commands

Compiler

- gcc, g++, clang

Debugging, Tracing

- gdb, strace, coredumpctl

Tools

- make, maven, graddle
- **git**

Python

- python2, pip

- python3, pip3

  

## Linux Obsolete(구식) Commands 

![image](https://user-images.githubusercontent.com/116723552/227124756-80619e49-b0c4-48d2-90fb-cd1db0bbea7e.png)

![image](https://user-images.githubusercontent.com/116723552/227124476-c3b66307-c195-478a-9d89-651405af00e8.png)



위의 명령어들을 다 외울 필요는 없고, Bold로 표시한 명령어들을 위주로 확인하고, **pwd, cd, ls, cp, mv, rm, mkdir, ln, find, chmod, ssh, vim** 명령어만 잘 익혀두자.

