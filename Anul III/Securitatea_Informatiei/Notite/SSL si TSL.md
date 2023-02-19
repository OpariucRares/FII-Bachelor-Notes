----
## Ce este Secure Socket Layer (SSL)?
- propusa de Netscap Communication
- Trebuie sa asigure: 
	- confidentialitate
	- autentifiare celor 2 parti (client-server), la IPSEC era host-host
	- integritate
- ![[Curs14_unde_e_pus_SSL.jpg]]
## Ce variante de SSL au fost scoase?
- SSL 1.0 - spart in 10 minute, nu a fost sigur (1994)
- SSL 2.0 - s-au gasit slabiciuni
- SSL 3.0 - se mai gaseste, dar nu e sigur. bazele

## Cum arata SSL?
- SSL nu asigaura nerepliere
- SSL orientat pe sockets: e deja securizat la transmitere
- application independent
- trece mai intai prin SSL si dupa ajunge la TCP
- are pe layer-ul 2 4 protocoale
- are pe primul layer 1 protocol (SSL record)
- ![[Curs14_SSL_in_protocol_TCP.jpg]]
## Ce este Transport Layer Security (TLS)?
- are o structura similara, dar s-au realizat schimbari semnificative:
	- a imbunatatit latenta (handshake in 1-RRT)
	- a imbunatati securitatea si privacy (forward security)
	- a imbunatatit arhitectura cripto ale protocoalelor: HMAC, AEAD
	
## Care este cea mai noua versiune de TLS?
- TLS 1.3 - incepand din 2014 si terminat in 2018
- folosit in Firefox, Chrome, Google, Facebook
- vibrant research topic: HMAC, SIGma, Tamarin

TLS in TCP/IP stack
- contine TLS handshake si TLS record

## Ce este o sesiune?
- avem mai multe conexiuni
- creat de protocolul handshake
- deschiderea unei sesiuni de lucru intre client-server in care se stabilesc parametri criptografici majori

## Ce este o conexiune?
- calculeaza cheile de la parametrii initiali ai sesiunii
- tip de serviciu

## Ce este TLS handshake protocol (cel mai complex protocol de la TLS)?
- clientul si serverul poate sa nu aiba nimic in comun
- negociaza parametrii criptografici intre cele 2 parti
- autentificare cu fiecare
- se stabileste matterialul de cheie pt comunicarea datelor

## Ce moduri de schimbare a cheii exista?
1) (EC)DHE mod - handshake standard ce nu foloseste chei impartasite anterior
2) Pre-shared key (PSK) based mode -> 2 variante
	2.1. PSK-only, fara forward security
	2.2. PSK with (EC)DHE ce are forward security


## HMAC-based key derivation
- functie de derivare a cheii (HMAC-based key derivation function)
	1) mai intai extrage o cheie din IKM. K <- HKDF.Ext(salt,IKM)
	2) in functie de optiuni, il extinde intr-un OKM (output key manager). OKM <- HKDF.Exp(K,info, L)

## Ce proprietati are handshake-ul?
1) A stabili aceleasi chei de sesiune
2) Securitatea cheilor de sesiune
3) Autentificarea partilor
4) Unicitatea cheilor de sesiune
5) Protectie la downgrade - aceeasi paramatri criptografici
6) Forward security - parametrii nu compromit cheile
7) Impersonificarea cheii - daca unul dintre parti a fost compromisa, celelalte parti nu pot fi impersonate
8) Protejarea capetelor de comunicatie

## Ce este protocol record?
- ai un fragment, concatenezi inainte de fragment cu noi parametrii
- ele sunt puse intr-un MAC care este padat la final si inaintea lui concatenat cu aceiasi parametri de dinainte
- cripteaza noua informatie si pune un header
- AHEAD (criptare autentificata cu date suplimentare)

## Ce este Mesaje alert?
- ofera closure information si erori
- criptat
- tipuri de alerte
	- closure alert 
		- close_notify (nu ii mai este permis sa transmita niciun mesaj pe conexiune)
		- user_canceled (user-ul cancel la handshake)
- error alerts - erori legate de inchiderea brusca a conexiunii
## Ce aplicatii sunt cu TLS si SSL>
- HTTPS (HTTP + SSL/TLS + TCP)
- FTPS (FTP + TLS), TLS CU VPN