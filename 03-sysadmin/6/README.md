# Домашнее задание к занятию «Компьютерные сети. Лекция 1»

### Цель задания

В результате выполнения задания вы: 

* научитесь работать с HTTP-запросами, чтобы увидеть, как клиенты взаимодействуют с серверами по этому протоколу;
* поработаете с сетевыми утилитами, чтобы разобраться, как их можно использовать для отладки сетевых запросов, соединений.

### Чеклист готовности к домашнему заданию

1. Убедитесь, что у вас установлены необходимые сетевые утилиты — dig, traceroute, mtr, telnet.
2. Используйте `apt install` для установки пакетов.


### Инструкция к заданию

1. Создайте .md-файл для ответов на вопросы задания в своём репозитории, после выполнения прикрепите ссылку на него в личном кабинете.
2. Любые вопросы по выполнению заданий задавайте в чате учебной группы или в разделе «Вопросы по заданию» в личном кабинете.


### Дополнительные материалы для выполнения задания

1. Полезным дополнением к обозначенным выше утилитам будет пакет net-tools. Установить его можно с помощью команды `apt install net-tools`.
2. RFC протокола HTTP/1.0, в частности [страница с кодами ответа](https://www.rfc-editor.org/rfc/rfc1945#page-32).
3. [Ссылки на другие RFC для HTTP](https://blog.cloudflare.com/cloudflare-view-http3-usage/).

------

## Задание

### **Шаг 1.** Работа c HTTP через telnet.

- Подключитесь утилитой telnet к сайту stackoverflow.com:

`telnet stackoverflow.com 80`
 
- Отправьте HTTP-запрос:

```bash
GET /questions HTTP/1.0
HOST: stackoverflow.com
[press enter]
[press enter]
```
*В ответе укажите полученный HTTP-код и поясните, что он означает.*

```bash
Slava@TURBOMac netology % telnet stackoverflow.com 80
Trying 151.101.1.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
HOST: stackoverflow.com

HTTP/1.0 403 Forbidden
Accept-Ranges: bytes
Content-Length: 1921
Content-Type: text/html
Date: Mon, 29 May 2023 15:10:31 GMT
Retry-After: 0
Server: Varnish
Via: 1.1 varnish
X-Cache: MISS
X-Cache-Hits: 0
X-Dns-Prefetch-Control: off
X-Served-By: cache-osl6529-OSL
X-Timer: S1685373031.056059,VS0,VE1

<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>Forbidden - Stack Exchange</title>
    <style type="text/css">
		body
		{
			color: #333;
			font-family: 'Helvetica Neue', Arial, sans-serif;
			font-size: 14px;
			background: #fff url('img/bg-noise.png') repeat left top;
			line-height: 1.4;
		}
		h1
		{
			font-size: 170%;
			line-height: 34px;
			font-weight: normal;
		}
		a { color: #366fb3; }
		a:visited { color: #12457c; }
		.wrapper {
			width:960px;
			margin: 100px auto;
			text-align:left;
		}
		.msg {
			float: left;
			width: 700px;
			padding-top: 18px;
			margin-left: 18px;
		}
    </style>
</head>
<body>
    <div class="wrapper">
		<div style="float: left;">
			<img src="https://cdn.sstatic.net/stackexchange/img/apple-touch-icon.png" alt="Stack Exchange" />
		</div>
		<div class="msg">
			<h1>Access Denied</h1>
                        <p>This IP address (185.253.97.180) has been blocked from access to our services. If you believe this to be in error, please contact us at <a href="mailto:team@stackexchange.com?Subject=Blocked%20185.253.97.180%20(Request%20ID%3A%20315822864-OSL)">team@stackexchange.com</a>.</p>
                        <p>When contacting us, please include the following information in the email:</p>
                        <p>Method: block</p>
                        <p>XID: 315822864-OSL</p>
                        <p>IP: 185.253.97.180</p>
                        <p>X-Forwarded-For: </p>
                        <p>User-Agent: </p>

                        <p>Time: Mon, 29 May 2023 15:10:31 GMT</p>
                        <p>URL: stackoverflow.com/questions</p>
                        <p>Browser Location: <span id="jslocation">(not loaded)</span></p>
		</div>
	</div>
	<script>document.getElementById('jslocation').innerHTML = window.location.href;</script>
</body>
</html>Connection closed by foreign host.
Slava@TURBOMac netology %
```

В моем случае при попытке обращения к ресурсу был получен ответ с ошибкой ```HTTP/1.0 403 Forbidden```.
HTTP 403 Forbidden — стандартный код ответа HTTP, означающий, что доступ к запрошенному ресурсу запрещен. Сервер понял запрос, но не выполнит его.

---

### **Шаг 2.** Повторите задание 1 в браузере, используя консоль разработчика F12:

 - откройте вкладку `Network`;
 - отправьте запрос [http://stackoverflow.com](http://stackoverflow.com);
 - найдите первый ответ HTTP-сервера, откройте вкладку `Headers`;
 - укажите в ответе полученный HTTP-код;
 - проверьте время загрузки страницы и определите, какой запрос обрабатывался дольше всего;
 - приложите скриншот консоли браузера в ответ.

![2_Question](images/2.png)

Получен ответ "HTTP 200 OK" - запрос выполнен успешно.
Время загрузки страницы - 5.99 секунд.
Дольше всего обрабатывался запрос страницы https://stackoverflow.com (на скриншоте выше список отсортирован по времени обработки).

---

### **Шаг 3.** Какой IP-адрес у вас в интернете?

![3_Question](images/3.png)

---

### **Шаг 4.** Какому провайдеру принадлежит ваш IP-адрес? Какой автономной системе AS? Воспользуйтесь утилитой `whois`.

```bash
Slava@TURBOMac netology % whois 178.252.127.224
% IANA WHOIS server
% for more information on IANA, visit http://www.iana.org
% This query returned 1 object

refer:        whois.ripe.net

inetnum:      178.0.0.0 - 178.255.255.255
organisation: RIPE NCC
status:       ALLOCATED

whois:        whois.ripe.net

changed:      2009-01
source:       IANA

# whois.ripe.net

inetnum:        178.252.127.0 - 178.252.127.225
netname:        NWLINK-NET
descr:          NWLINK-NET2
country:        RU
admin-c:        RC6422-RIPE
tech-c:         RC6422-RIPE
status:         ASSIGNED PA
mnt-by:         NWLINK-MNT
created:        2010-12-13T12:00:44Z
last-modified:  2010-12-13T12:00:44Z
source:         RIPE

person:         Rjevkin Constantine
address:        Russia, 196240,Saint-Petersburg, 23B, Egorova
phone:          +7 905 2166789
nic-hdl:        RC6422-RIPE
created:        2007-04-16T07:58:43Z
last-modified:  2020-06-04T07:32:57Z
source:         RIPE
mnt-by:         NWLINK-MNT

% Information related to '178.252.112.0/20AS42893'

route:          178.252.112.0/20
descr:          Home Internet ltd 4
origin:         AS42893
mnt-by:         NWLINK-MNT
created:        2010-06-15T09:54:31Z
last-modified:  2010-06-15T09:54:31Z
source:         RIPE

% This query was served by the RIPE Database Query Service version 1.106.1 (BUSA)


Slava@TURBOMac netology %
```

IP адрес **178.252.127.224** принадлежит провайдеру ```NWLINK-MNT``` и связан с автономной системой AS42893.

---

#### **Шаг 5.** Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой `traceroute`.

```bash
vagrant@vagrant:~$ traceroute -A --icmp 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  _gateway (10.0.2.2) [*]  0.405 ms  0.314 ms  0.253 ms
 2  192.168.1.1 (192.168.1.1) [*]  2.394 ms  2.884 ms  2.806 ms
 3  10.139.84.125 (10.139.84.125) [*]  4.472 ms  4.899 ms  4.797 ms
 4  * * *
 5  * * *
 6  74.125.244.132 (74.125.244.132) [AS15169]  4.377 ms  8.349 ms  8.264 ms
 7  142.251.61.219 (142.251.61.219) [AS15169]  8.180 ms  7.924 ms  7.827 ms
 8  172.253.79.113 (172.253.79.113) [AS15169]  7.190 ms  7.096 ms  7.024 ms
 9  * * *
10  * * *
11  * * *
12  * * *
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  dns.google (8.8.8.8) [AS15169]  15.288 ms  15.144 ms  14.983 ms
vagrant@vagrant:~$
```

Маршрут пакетов:

1. `_gateway` - Локальная сеть
2. `192.168.1.1` - домашний роутер
3. `10.139.84.125` - возможно, какой-то узел интернет-провайдера 
4. `* * *` - неизвестно, возможно, какой-то узел интернет-провайдера или узел, проигнорировавший наш запрос
5. `* * *` - неизвестно, возможно, какой-то узел интернет-провайдера  или узел, проигнорировавший наш запрос
6. `74.125.244.132 (74.125.244.132) [AS15169]  4.377 ms  8.349 ms  8.264 ms` - промежуточный узел в автономной системе AS15169
7. `142.251.61.219 (142.251.61.219) [AS15169]  8.180 ms  7.924 ms  7.827 ms` - промежуточный узел в автономной системе AS15169
8. `172.253.79.113 (172.253.79.113) [AS15169]  7.190 ms  7.096 ms  7.024 ms` - промежуточный узел в автономной системе AS15169
9-17. `* * *` - неизвестно, несколько узлов, проигнорировавших наш запрос
18. `dns.google` (8.8.8.8) - искомый узел, находящийся в автономной системе AS15169

---

#### **Шаг 6.** Повторите задание 5 в утилите `mtr`. На каком участке наибольшая задержка — delay?

![6_Question](images/6.png)

Данные программы MTR показывают, что самые большие задержки возникают на узле 142.251.51.187, связанном с автономной системой AS15169.

---

#### **Шаг 7.** Какие DNS-сервера отвечают за доменное имя dns.google? Какие A-записи? Воспользуйтесь утилитой `dig`.

```bash
vagrant@vagrant:~$ dig +trace dns.google

; <<>> DiG 9.16.1-Ubuntu <<>> +trace dns.google
;; global options: +cmd
.			7145	IN	NS	m.root-servers.net.
.			7145	IN	NS	l.root-servers.net.
.			7145	IN	NS	k.root-servers.net.
.			7145	IN	NS	j.root-servers.net.
.			7145	IN	NS	i.root-servers.net.
.			7145	IN	NS	h.root-servers.net.
.			7145	IN	NS	g.root-servers.net.
.			7145	IN	NS	f.root-servers.net.
.			7145	IN	NS	e.root-servers.net.
.			7145	IN	NS	d.root-servers.net.
.			7145	IN	NS	c.root-servers.net.
.			7145	IN	NS	b.root-servers.net.
.			7145	IN	NS	a.root-servers.net.
;; Received 262 bytes from 127.0.0.53#53(127.0.0.53) in 4 ms

google.			172800	IN	NS	ns-tld5.charlestonroadregistry.com.
google.			172800	IN	NS	ns-tld1.charlestonroadregistry.com.
google.			172800	IN	NS	ns-tld3.charlestonroadregistry.com.
google.			172800	IN	NS	ns-tld2.charlestonroadregistry.com.
google.			172800	IN	NS	ns-tld4.charlestonroadregistry.com.
google.			86400	IN	DS	6125 8 2 80F8B78D23107153578BAD3800E9543500474E5C30C29698B40A3DB2 3ED9DA9F
google.			86400	IN	RRSIG	DS 8 1 86400 20230611050000 20230529040000 60955 . oX5I54Q0Ew5/FPgpwWvhrLBNgnjFHwA82EuWg1FVtDhXeM9TD++ApKo6 bk4GD6sG7MRrpgg3EOmmdBODt0DVyL2mhXurrP0IdVycsRcNko/TAFyO 6LYWXvwdQhiXXjrbtCFP92XtFY3SVBl0XOoL0ZRM8OExLOmsyQ/P/Mw9 0J0hsQgeZRVQ9tLiPXHioDmC+JgWSpxVUVRnieXZ4eRSRw/a6zIKajME jdc+96q9QMGSw6vMvUMLKVvdYSIy/rKNH9gyQ6GWssbrm45DMCuuUeq1 51n3QSiv0szYzo0d87UJ6J3+pV7U3DSSV0ngXtSpzShT6dXlCFNXIPSX jeNxTg==
;; Received 758 bytes from 192.33.4.12#53(c.root-servers.net) in 48 ms

dns.google.		10800	IN	NS	ns4.zdns.google.
dns.google.		10800	IN	NS	ns1.zdns.google.
dns.google.		10800	IN	NS	ns2.zdns.google.
dns.google.		10800	IN	NS	ns3.zdns.google.
dns.google.		3600	IN	DS	56044 8 2 1B0A7E90AA6B1AC65AA5B573EFC44ABF6CB2559444251B997103D2E4 0C351B08
dns.google.		3600	IN	RRSIG	DS 8 2 3600 20230616214813 20230525214813 42193 google. O2POXm+aGH1B1o6Tg5YEo5t/S6sIbByO8EDvvteL5TGhf96ORv4yPlik Iu7QsONGv1MaDMezJbh5qmPulF3oXNihcjifcmVe2agTROo/Z+zv67Ti qTxDmGlvXhIyX0YvT7/yVmSLp4JSDLaBH8mxdMZuCF5eDxyibB3aBixr BcA=
;; Received 506 bytes from 216.239.38.105#53(ns-tld4.charlestonroadregistry.com) in 16 ms

dns.google.		900	IN	A	8.8.4.4
dns.google.		900	IN	A	8.8.8.8
dns.google.		900	IN	RRSIG	A 8 2 900 20230618191939 20230527191939 34681 dns.google. GGEB40je4qkf+SDtxbpjT3UssK7A8xLTQRB1WRW6yZC54bu5+ZjUyuI0 9I9IdP81TIY+j1QQ2OGKXAMfAnzJq6HAGQTgK3n6qcnpl0U+dUtsvqwo yqorRyBC1XcZWRG5I4YcfWRTvV64XgV4gueULxKyAqJNSNXgHY+kbRC/ kzE=
;; Received 241 bytes from 216.239.34.114#53(ns2.zdns.google) in 40 ms

vagrant@vagrant:~$
```

За доменное имя `dns.google` отвечают сервера c IP адресами `8.8.8.8` и `8.8.4.4` (`A` записи).

По трассировке виден маршрут поиска:

1. `.` - получено от 127.0.0.53

1. `google.` - получено от 192.33.4.12 (c.root-servers.net)

1. `dns.google.` - получено от 216.239.38.105 (ns-tld4.charlestonroadregistry.com)

1. А записи получены от 216.239.34.114 (ns2.zdns.google)

---

#### **Шаг 8.** Проверьте PTR записи для IP-адресов из задания 7. Какое доменное имя привязано к IP? Воспользуйтесь утилитой `dig`.

*В качестве ответов на вопросы приложите лог выполнения команд в консоли или скриншот полученных результатов.*

Обратный вызов к `8.8.8.8`:

```bash
vagrant@vagrant:~$ dig -x 8.8.8.8

; <<>> DiG 9.16.1-Ubuntu <<>> -x 8.8.8.8
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39478
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;8.8.8.8.in-addr.arpa.		IN	PTR

;; ANSWER SECTION:
8.8.8.8.in-addr.arpa.	6320	IN	PTR	dns.google.

;; Query time: 4 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Mon May 29 16:21:22 UTC 2023
;; MSG SIZE  rcvd: 73
```

PTR запись `dns.google.`

Обратный вызов к `8.8.4.4`:

```bash
vagrant@vagrant:~$ dig -x 8.8.4.4

; <<>> DiG 9.16.1-Ubuntu <<>> -x 8.8.4.4
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 32034
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;4.4.8.8.in-addr.arpa.		IN	PTR

;; ANSWER SECTION:
4.4.8.8.in-addr.arpa.	3367	IN	PTR	dns.google.

;; Query time: 12 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Mon May 29 16:21:37 UTC 2023
;; MSG SIZE  rcvd: 73
```

PTR запись `dns.google.`

Обратный вызов к `192.33.4.12`:

```bash
vagrant@vagrant:~$ dig -x 192.33.4.12

; <<>> DiG 9.16.1-Ubuntu <<>> -x 192.33.4.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 20067
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;12.4.33.192.in-addr.arpa.	IN	PTR

;; ANSWER SECTION:
12.4.33.192.in-addr.arpa. 7551	IN	PTR	c.root-servers.net.

;; Query time: 40 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Mon May 29 16:26:19 UTC 2023
;; MSG SIZE  rcvd: 85
```

PTR запись `c.root-servers.net.`

---

Использованные в лекции материалы:

- `traceroute -An 8.8.8.8` - Показывать маршрут. `A` - показывает AS (автономные системы), `n` - скрывает доменные имена

- `mtr -zn 8.8.8.8` - Показывать маршрут в реальном времени. `z` - показывает AS (автономные системы), `n` - скрывать доменные имена

- `ping` - Проверяет доступность сетевого адреса

- `whois` - Вывод информации об IP, `-h whois.radh.net <IP>` - запрос в базу. `-- '-i origin AS32331'` - показывает все диапазоны адресов автономной системы

- `bgpq3` - Пакет автоматизации GBP фильтрации для CISCO и JUNIPER роутеров (`man 8 bgpq3`)

- `dig` - Утилита поиска DNS (Требуется установка: `apt install dnsutils`)

- `telnet <адрес> <порт>` - Пользовательский интерфейс к протоколу TELNET

- `curl` - Отправка запросов на сервер

- `httpie` - Отправка запросов по HTTP протоколу (более простой cURL, Требуется установка: `apt install httpie`)

- `jq` - JSON процессор для коммандной строки (Требуется установка: `apt install jq`)


---

### Правила приёма домашнего задания

В личном кабинете отправлена ссылка на .md-файл в вашем репозитории.


### Критерии оценки

Зачёт:

* выполнены все задания;
* ответы даны в развёрнутой форме;
* приложены соответствующие скриншоты и файлы проекта;
* в выполненных заданиях нет противоречий и нарушения логики.

На доработку:

* задание выполнено частично или не выполнено вообще;
* в логике выполнения заданий есть противоречия и существенные недостатки. 
