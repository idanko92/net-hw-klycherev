# Домашнее задание к занятию "`Уязвимости и атаки на информационные системы`" - `Ключерев Даниил`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя **nmap**.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

- Какие сетевые службы в ней разрешены?
- Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)
  
*Приведите ответ в свободной форме.*  

### Ответ

Список сетевых служб:

1. 21 порт - ftp (vsftpd 2.3.4)
2. 22 порт - ssh (OpenSSH 4.7p1 Debian 8ubuntu1)
3. 23 порт - telnet
4. 25 порт — smtp (Postfix smtpd)
5. 53 порт — domain (ISC BIND 9.4.2)
6. 80 порт — http (Apache 2.2.8)
7. 111 порт — rpcbind
8. 139/445 порты — netbios-ssn (Samba smbd 3.X – 4.X)
9. 512 порт — exec (netkit-rsh rexecd)
10. 514 порт — shell (Netkit rshd)
11. 1099 порт — java-rmi (GNU Classpath grmiregistry)
12. 1524 порт — bindshell (root shell)
13. 2049 порт — nfs
14. 2121 порт — ftp (ProFTPD 1.3.1)
15. 3306 порт — mysql (MySQL 5.0.51a-3ubuntu5)
16. 5432 порт — postgresql (8.3.0-8.3.7)
17. 5900 порт — vnc
18. 6667 порт — irc (UnrealIRCd)
19. 8009 порт — ajp13 (Apache Jserv)
20. 8180 порт — http (Apache Tomcat/Coyote JSP 1.1) 

Список обнаруженных уязвимостей:

1. netbios-ssn - [Samba 3.5.0 - Remote Code Execution](https://www.exploit-db.com/exploits/42060)
2. mysql - [MySQL 5.0.x - Single Row SubSelect Remote Denial of Service](https://www.exploit-db.com/exploits/29724)
3. http - [phptax 0.8 - Remote Code Execution](https://www.exploit-db.com/exploits/21665)

Вывод nmap:

```
danko2@danko2ubuntu:~$ sudo nmap -sS -sV -O 10.0.123.101
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-14 10:07 MSK
Nmap scan report for 10.0.123.101
Host is up (0.00043s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
53/tcp   open  domain      ISC BIND 9.4.2
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
111/tcp  open  rpcbind     2 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
512/tcp  open  exec        netkit-rsh rexecd
513/tcp  open  login?
514/tcp  open  shell       Netkit rshd
1099/tcp open  java-rmi    GNU Classpath grmiregistry
1524/tcp open  bindshell   Metasploitable root shell
2049/tcp open  nfs         2-4 (RPC #100003)
2121/tcp open  ftp         ProFTPD 1.3.1
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
5900/tcp open  vnc         VNC (protocol 3.3)
6000/tcp open  X11         (access denied)
6667/tcp open  irc         UnrealIRCd
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
MAC Address: 08:00:27:2F:F5:F7 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 2.6.X
OS CPE: cpe:/o:linux:linux_kernel:2.6
OS details: Linux 2.6.9 - 2.6.33
Network Distance: 1 hop
Service Info: Hosts:  metasploitable.localdomain, irc.Metasploitable.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 54.03 seconds

```

---

### Задание 2

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

- Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
- Как отвечает сервер?

*Приведите ответ в свободной форме.*

### Ответ

Отличия режимов c точки зрения трафика и ответы сервера:

- SYN scan - nmap отправляет только SYN-пакет без завершения соединения (полуоткрытое соединение), если сервер отвечает SYN-ACK, порт открыт; если RST - порт закрыт. В трафике видны только одиночные SYN и ответы SYN-ACK или RST.
- FIN scan - nmap отправляет пакеты с флагом FIN без установления соединения. Большинство ОС, если порт закрыт, отправляют RST в ответ; если открыт — игнорируют пакет, и ответа нет. В трафике - только FIN-запросы и, при закрытом порте, RST-ответы.
- Xmas scan - nmap отправляет TCP-пакет с флагами FIN, URG, PSH. Ответ аналогичен FIN: RST при закрытом порте, отсутствие ответа - порт открыт. В трафике Xmas-запросы, ответы - RST или ничего.
- UDP scan - nmap отправляет UDP-пакет. Если порт закрыт, сервер отвечает ICMP-пакетом "порт недоступен". Если порт открыт - чаще всего ответ отсутствует (или, для некоторых сервисов, генерируется UDP-ответ). В трафике поток UDP-запросов, ответы - ICMP unreachable либо UDP-пакеты от сервисов.

Файл со сканированием - [scan.pcapng](/scan.pcapng)