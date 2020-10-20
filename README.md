## Labo1: Computernetwerken
### Opdrachten met telnet: aan de slag
1. We maken bestand aan:  
 **ssh** oclemens@home.test.atlantis.ugent.be  
 Password: studentennummer  
 **Cat > mijninfo.txt**

2.	We proberen dezelfde server te openen op **poort 13**:  
 We geven het wachtwoord op en krijgen een error. Bash: 13: command not found

3.	We kunnen dit testen door de server te openen op **poort 21**, hierbij krijgen we een output:  
 Connected to home.test.atlantis.ugent.be.  
 Escape character is '^]'.  
 220 ProFTPD 1.3.5b Server (Debian) _[157.193.215.170]_ 

4.	We proberen eerst de mailserver te openen op **poort 25**:  
 Dit lukt niet. We proberen eerst via de home server te verbinden en langs deze weg een verbinding te leggen met de mailserver.     Dit werkt, we zijn verbonden met de server.
  We proberen de server ook te openen op poort 220, hierbij krijgen we een telnet error:  
  telnet: Unable to connect to remote       host: Connection refused  
 >**HELO** mycomputer.homenet.be  
 250 mail.test.atlantis.ugent.be  
 **MAIL FROM**: oclemens@test.atlantis.ugent.be  
 250 2.1.0 Ok  
 **RCPT TO**: oclemens@test.atlantis.ugent.be  
 250 2.1.5 Ok  
 **DATA**  
 354 End data with <CR><LF>.<CR><LF>  
 Dit is een mailtje   
 (Vraag 4)  
 .  
 250 2.0.0 Ok: queued as C8D9AC0054  
 **QUIT**  
 221 2.0.0 Bye  
 Connection closed by foreign host.  

5.	We openen nu dezelfde mailserver op **poort 110**

 >telnet mail.test.atlantis.ugent.be 110  
 Trying 157.193.215.172...  
 Connected to mail.test.atlantis.UGent.be.  
 Escape character is '^]'.  
 +OK Hello there.  
 **USER** oclemens  
 +OK Password required.  
 **PASS** 01808655  
 +OK logged in.  
 **STAT**  
 +OK 1 410  
 **RETR 1**  
 +OK 410 octets follow.  
 Return-Path: <oclemens@test.atlantis.ugent.be>  
 X-Original-To: oclemens@test.atlantis.ugent.be  
 Delivered-To: oclemens@test.atlantis.ugent.be  
 Received: from mycomputer.homenet.be (home.test.atlantis.ugent.be [157.193.215.170])  
	 by mail.test.atlantis.ugent.be (Postfix) with SMTP id C8D9AC0054  
	 for <oclemens@test.atlantis.ugent.be>; Tue, 20 Oct 2020 12:22:04 +0200 (CEST)  
 Dit is een mailtje   
 (Vraag 4)  
 .  
 **QUIT**  
 +OK Bye-bye.  
 Connection closed by foreign host.  

6.	We sturen nu een mail naar het gevraagde mailadres  

>**HELO** mycomputer.homenet.be  
250 mail.test.atlantis.ugent.be  
**MAIL FROM**: oclemens@test.atlantis.ugent.be  
250 2.1.0 Ok  
**RCPT TO**: comnet1@test.atlantis.ugent.be  
250 2.1.5 Ok  
**DATA**  
354 End data with <CR><LF>.<CR><LF>  
_Subject_: Labo 1 -mail  
Dit is het mailtje van het labo.  
.  
250 2.0.0 Ok: queued as 7D255C0054  
**QUIT**  
221 2.0.0 Bye  
Connection closed by foreign host.  

7.	 **NOOP**: De server doet niks, het geeft enkel een _+OK_ terug.

8.	We openen _Wireshark_. We surfen vervolgens naar de gevraagde website:  
 **Firefox www.test.atlantis.ugent.be**  
 We kunnen uit Wireshark alle verbindingen halen met hun IP, die nodig zijn om op de uiteindelijke webpagina te komen.

9.	 We openen de webserver met telnet op **poort 80**.  
 >telnet www.test.atlantis.ugent.be 80  
 Trying 157.193.215.171...  
 Connected to www.test.atlantis.ugent.be.  
 Escape character is '^]'.  
 **GET / HTTP/1.0**  
 HTTP/1.1 200 OK  
 Date: Tue, 20 Oct 2020 11:07:06 GMT  
 Server: Apache/2.4.25 (Debian)  
 Last-Modified: Tue, 13 Oct 2020 16:02:23 GMT  
 ETag: "2bc-5b18f8a5f28e1"  
 Accept-Ranges: bytes  
 Content-Length: 700  
 Vary: Accept-Encoding  
 Connection: close  
 Content-Type: text/html  

10.	We surfen opnieuw naar de gegeven site. We merken op dat het aantal verbindingen veel minder is dan de verbinding met telnet of firefox.




### Opdrachten met DNS: aan de slag

1.	We zoeken het IP adres van www.ugent.be met commando: **nslookup**  
 We vinden hier dat het IP-adres= _157.193.43.50_  
 Voor het zoeken welke servers verantwoordelijk zijn gebruiken we het commando: **dig**  
 Hieruit krijgen we 4 servers:  
 •	ns.belnet.be  
 •	ugdns1.ugent.be  
 •	ugdns2.ugent.be  
 •	ugdns3.ugent.be  

2.	We vinden het IP-adres : _217.19.230.167_.  
 We gebruiken het commando: **host [IP-adres]** en vinden dat de server van www.belnet.be een andere naam heeft: _combell.com_

3.	We zien dat alle resolves op de student server hetzelfde IP-adres geven. We zien wel dat de verschillende nameservers van     plaats veranderen bij elke resolve. Dit zorgt ervoor dat niet iedereen op dezelfde server komt bij het opzoeken van de website. Hierdoor worden de servers minder belast.  
Wanneer we ons inloggen via de home server en de URL resolven, zien we dat het IP-adres is gewijzigd. De naamservers zijn wel dezelfde gebleven.

4.	Wanneer we een lookup doen naar www.tinder.be zien we op Wireshark dat er 2 requests werden gestuurd en 2 antwoorden terug gestuurd werden.



