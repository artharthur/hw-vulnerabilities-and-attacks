# Домашнее задание: «Уязвимости и атаки на ИС»

---

## Сканирование nmap

```bash
nmap -sV 192.168.1.55

Результаты (характерные для Metasploitable 2):

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

Найденные сервисы
	•	FTP (vsftpd 2.3.4)
	•	SSH (OpenSSH 4.7p1)
	•	Telnet
	•	Apache 2.2.8 (HTTP)
	•	Samba (SMB 3.x)
	•	MySQL 5.0.51a
	•	PostgreSQL 8.3.x
	•	Apache Tomcat 1.1 (8180/tcp)

⸻

Уязвимости (Exploit-DB)
	1.	vsftpd 2.3.4 — Backdoor Command Execution — EDB-ID 17491
	2.	Samba 3.x — Remote Code Execution (Username map script) — EDB-ID 16320
	3.	Apache Tomcat (8180/tcp) — Manager App Default Credentials — EDB-ID 16189

⸻
