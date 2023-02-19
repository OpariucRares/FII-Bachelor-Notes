----
## Ce probleme erau in protocoalele TCP/IP?
 - Bellovin (1989) a raportat probleme in protocoale TCP/IP:
	- eavesdropping (sniffing, snooping)
	- data modification
	- sequene number spoofing
	- IP address spoofing
	- Routing attacks
- datele care intra in IP primesc protectie; poate fi folosit de la IPv4 la IPv6

## Ce elemente din securitate sunt?
 - host
 - security
 - gateway
## Ce tipuri de securitate sunt?
1) host-host
2) host - poarta de securitate
3) poarta de securitate - poarta de securitate (security gateway)

## Cum poate opera reteaua?
- transport (end-to-end)
- tunnel (VPN)

## Concepte din retelistica
- Node - dispozitiv capabil sa creeze sau sa transmita mesaje identificate prin adresa IP
- Host - nod ce este un computer
- Security gateway (poarta de securitate) - daca implementeza protocoale IPsec (router/firewall)

## Ce ofera IPsec?
1) Autentificare (AH)
2) Encapsulare (ESP) - pt confidentialitate
3) Asocieri de securitate (SA) - specificatii la ce tip de securitate doresc
4) Mecanism de management al cheilor
5) Algoritm de autentificare si criptare
## Unde se afla IPsec?
![[Curs13_IPSec_Position.png]]

## Ce ofera Autentificarea si encapsularea?
 - control  acces
 - integritate date
 - data origin authentication
 - confidentiality
 - rejection of replayed packages
 - limited traffic flow 
 - confidentiality
		  
## Cum lucreaza IPsec?
![[Curs13_IPSec_how_works.jpg]]

## Cum functioneaza modul transport?
- se utilizeaza intre 2 gazde (client-server)
- Portile de securitate nu sunt obligate sa suporte modul transport
- nu protejeaza campurile mutabile !!!!!
- costuri de procesare mai reduse
- **IMPORTANT**: Datagrama de autentificare fara campuri mutabile, cripteaza corpul datagramei

## Cum arata AH-transport?
- bloc de autentificare (MAC) => AH 
- la Ipv4: intre header si IP payload
- la Ipv6: in extensisa header-ului, intre rout si dest
 - ![[Curs13_Bloc_autentificare_transport.jpg]]
## Cum arata ESP-transport?
- alcatuit din ESP header, ESP trailer (padare), ESP autoritate
- la Ipv4: 
	- Esp header se pune la final la Ip header
	- se cripteaza IP payload-ul + ESP trailer
	- Autentificare cu ce am criptat + ESP header

- la Ipv6:
	- Esp header in extensie header, intre rout si dest
	- se cripteaza dest + IP payload + ESP trailer
	- se autentifica cu ce am criptat + ESP header
- ![[Curs13_IPSec_ESP_transport.jpg]]




## Cum inseamna modul tunnel?
- protejeaza totul
- cost suplimentar
- inlocuim cu un nou header, deaorece cand autentific campurile mutabile, pierd totul
## Cand este folosit modul tunnel?
- **IMPORTANT**: Host-urile trebuie sa suporte modul transport si modul tunel
- se foloseste cand un capat are o poarta de securitate
	1) host-host
	2) host - poarta de securitate
	3) poarta de securitate - poarta de securitate (2 firewall-uri)

## Cum arata AH in modul tunel?
- la ipv4: ai nou Ip header + blocul de autentificare + Ipv4 datagrama
- la ipv6: ai nou main Ip header + new extension header + blocul de autentificare + Ipv6 datagram
 - ![[Curs13_IPSec_AH_tunel.jpg]]

## Ce elemente are Authentication Header?
- are next header + payload length + researved
- security parameter inex (SPI) - un nr care identifica o asociere de securitate
- sequence number - impotriva atacurilor de reply
- adresa de sursa si de destinatie este sub protectia AH si ESP -> previne address spoofing
- authentication data (variabila) - bloc de autoritate
	- Primitive criptografice - HMAC-SHA-1-96, AES_XCBC_96
-  ![[Curs13_Cum_arata_header-ul_AH.jpg]]

## Ce elemente are Encapsulation Security Payload format?
- security index parameter
- sequence number - impotriva reply attacks
- payload data + padding + pad length + next header
- data de autentificare
- ![[Curs13_Encapsulating_header.jpg]]

## Ce este Asociere de securitate (SA)?
- specifica cum vrem sa comunicam
- are o tupla alcatuita din (SPI, IP destionation address, protocolul de securitate)
- SPI - sa faca o diferentie intre mai multe asocieri de securitate (care au acelas ip address si protocol de securitate)
- ip destionation address poate sa fie unicat, broadcast, multicast
- protocol de securitate - AH sau ESP
- este unidirectionala

## Ce este Asociere de securitate de tip bundle?
- combinatii de SA
- pot fi combinate in 2 moduri
	a) transport adiacent - in modul transport aplic ambele protocoale de securitate pe aceeasi datagrama
	b) iterare tunelata - aplicam mai multe layere de securitate

## Modele folosind IPSec
- End-to-end security
	- host1 - internet/intranet - host2 (tunel de conexiune) (ESP sau AH sau ambele)
- Basic support vpn
	- host1-intranet-gw1 - intranet/internet - gw2 - intranet -host2 (tunel de conexiune)
- portile de securitate TREBUIE sa implementeze IPsec, hosturile nu
- End-to-end security cu vpn
	- host1-intranet-gw1 - intranet/internet - gw2 - intranet -host2 (conexiune + tunele)
	- portile de securitate TREBUIE sa implementeze IPsec, hosturile nu
- Remote access
	- host1 - intranet/internet - g2(firewall) - intranet - host2
	- h1 si g2 => tunel mod
	- intre h1 si h2 - tunel sau transport
## Unde se afla politicile de securitate?
- Politicile de securitate se afla in baza de date (SAD, SPD)
- Security Association DAtabase, Security Policy Database
## Ce este Internet key exchange?
- componenta din IPsec
- permite autentificare mutuala de la ambii membrii
- stabileste un IKE SA ce contine secretele partajate
- stabileste AH si ESP SAs si set de algoritmi criptografici ce sunt folosite de ei









	