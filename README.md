# Домашнее задание: «Уязвимости и атаки на информационные системы»

## Сканирование nmap

```markdown
nmap -sV 192.168.1.55

Результаты:

PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
111/tcp  open  rpcbind     2 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd 3.X
445/tcp  open  microsoft-ds Samba smbd 3.X
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1


⸻

Ответы на вопросы

Какие сетевые службы в ней разрешены?
На Metasploitable доступны следующие сервисы: FTP, SSH, Telnet, SMTP, HTTP (Apache), RPC, Samba (SMB), MySQL, PostgreSQL и Apache Tomcat.

Какие уязвимости были обнаружены?
	•	Уязвимость в FTP-сервере vsftpd 2.3.4 (backdoor) — EDB-ID 17491
	•	Уязвимость в Samba 3.x (удалённое выполнение кода) — EDB-ID 16320
	•	Уязвимость Apache Tomcat (дефолтные учётные данные в Manager App) — EDB-ID 16189

Metasploitable — это специально уязвимая ОС, в которой преднамеренно оставлены старые версии сервисов. Сканирование nmap показало множество открытых портов (FTP, SSH, Telnet, Samba, базы данных, Apache и Tomcat).
При анализе удалось выявить, что FTP-сервер содержит известный бэкдор, Samba уязвима к удалённому выполнению кода, а Tomcat можно скомпрометировать через стандартные логин/пароль.

⸻

# Задание 2

Сканирование в разных режимах

SYN-скан (полуоткрытый):
nmap -sS 192.168.1.55

FIN-скан:
nmap -sF 192.168.1.55

Xmas-скан:
nmap -sX 192.168.1.55

UDP-скан:
nmap -sU 192.168.1.55


Ответы на вопросы:

Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
- SYN-скан: посылается только SYN. Если порт открыт → SYN/ACK, закрыт → RST.
- FIN-скан: посылается FIN. Закрытые порты отвечают RST, открытые молчат.
- Xmas-скан: отправляется пакет с флагами FIN/PSH/URG. Закрытые → RST, открытые молчат.
- UDP-скан: закрытые отвечают ICMP, открытые — обычно молчат.

Как отвечает сервер?
- Открытые TCP-порты при SYN возвращают SYN/ACK, при FIN/Xmas молчат.
- Закрытые TCP-порты при SYN возвращают RST, при FIN/Xmas тоже RST.
- UDP-порты: закрытые отвечают ICMP, открытые — обычно молчат.

В Wireshark видно, что TCP-сканы отличаются по флагам пакетов: SYN — «полуоткрытый», FIN и Xmas используют необычные комбинации, а UDP-скан работает без установки соединения.
