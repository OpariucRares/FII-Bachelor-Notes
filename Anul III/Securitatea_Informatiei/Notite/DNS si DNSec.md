----
## Ce reprezinta protocoalele de securitate?
- Internet Domain (domeniu de internet) = colectie de date ce formeaza o unitate administrativa si tehnica in internet
 - Nume de domeniu: string de identificare a unui Internet domain
 - DNS - sistem ierarhic de gestiune a domeniilor de internet, organizat ierarhic si descentralizat administrat de entitati locale conectate intre ele
		
## Care sunt componentele principale dintr-un DNSEC?
1) spatiu de nume de domenii (info care se ataseaza de fiecare domeniu) si RR (resource records) - inregistrari de resurse
2) Serverele de nume (NS) - retine tree-ul domeniului si informatiile
3) Resolver - programe care extrag informatii din baza DNS (NS?)

## Ce reprezinta spatiul de nume (name space)?
 - Spatiu de nume (name space): organizare arborescenta a DNS
 - radacina se refera la intreg spatiul de nume
 - subdomenii: subspatii
 - fiecare informatii din DNS este insotita de o baza de date cu diverse informatii
 - pentru a face gestiunea de nume -> arborele se imparte in zone contigue numite zone de autoritate
 - servere de nume primare, + servere de cache (rol improtant pentru resolver in eficientizarea serviciilor oferite de resolver)
## Unde sunt folosite resursele de inregistrare (RR)?
 - fiecare nod are asociat un RR (resource records)
## Ce format are RR-ul?
 - TTL - timpul in care ramane in cache (mai ales daca este folosita de resolver)
## Ce tipuri de RR exista?
 - SOA - Start of Authority: inregistrare de inceput de zona de autoritate (UNA SINGURA)
	- contine TTL, nume de server principal si email-ul persoanei care se ocupa de administrare
 - NS = Name Server - furnizeaza informatii despre un server de nume ce este autorizat pentru zona
 - A = Address - adresa IP pe 32 de bit (adresa IP a nodului, stocat pentru procesul de rezolutie)
 - MX = Mail eXchanger - specifica locatia (numele device-ului) ce este responsabil pentru mail-urile trimise catre domain, locatia trebuie sa aiba un valid A RR

## Cum se extrage informatia din BD? (Rezolutia)
- standard
- numelui de domeniu
- inversa
- adresa de email	

## Ce tehnici de rezolutie pentru nume de DNS exista?
 - iterativ
 - recursiv

## Cum se realizeaza aceasta rezolutie?
 - solicitarea se face intai pentru serverul principal de nume
 - daca faci un request la un nod, iti intoarce NS cu calea nodul urmator + ce este inaintea lui
 - daca nu are NS, intoarce IP cu acelas naming convention (de jos in sus)
 - (slide 12 din IS-DNSEC)

## Ce tipuri de resolver sunt?
 - full - aplicatie independenta care rezolva rezolve solicitarea de la client
 - stub - doar pe partea de client

## Ce vulnerabilitati are DNS-ul?
 - DNS snooping
 - DNS ID hacking
 - DNS cache poisoning
## Ce solutie exista pentru a combate aceste vulnerabilitati?
 - DNSec - extensie de securitate pt DNS 
 - standardizarea acestei solutii se face in 2005
## Ce avantaje aduce DNSec?
 - contine Autentificare si integritate
 - data origin authentication: permite resolver-ului sa verifice criptografic daca datele de udne au venit provin de unde se presupune
 - data integrity protection - permite resolver-ului sa verifice daca datele au fost
## Ce tipuri de semnaturi digitale exista?
 - RRSIG (RR SIGnature) - intreg ce retine semnatura digitala
- DNSKEY (DNS public KEY) - stocheaza o cheie de verificare publica
- NSEC/NSEC 3 (Next SECure) - arata ca ceva nu exista cu adevarat
- DS (Delegation Signer) 
   - verifica integritatea unei PK de verificare a semnaturii
   - altfel ar putea fi inlocuita de adversar
   - RSA SHA512 -> prea mare
   - SHA-256 folosit
- EC (eliptic curves)

## Care este ordinea canonica a DNS-ului?
- Uppercase US-ASCII letter are treated as lowercase
- sortare cu label-ul cel mai din dreapta
- daca la fel, continua pana la un label diferit
- RData pentru DNSKEY - contine tipul algoritmului
## Cum inregistrezi o zona? 
 - Inregistra o zona ai nevoide Zone Signing keys (ZSK) si pentru a valida ZSK, ai nevoie de Key signing keys (KSK)
 - flag 7 este 1 -> ZSK
 - flag 15 este 1 -> KSK
 - semnarea unei zone include DNSKEY RRs, RRSIG RRs, NSEC RRs si optional DS RRs.
## Ce se intampla daca nu vrei sa inregistrezi o zona
 - Atacul de enumerare a zonelor - spam la email
 - Delegare sigura poate fi scumpa (zone de delegare largi, zone unde delegatiile nesigure sunt updatate rapid)
## Care este solutia?
 - NSEC3 - rezolva cele 2 probleme
	  - raspunsul de data aceasta este hashuit (hash-ul domeniului urmator)
	  - pct de delegare securizat/nesecurizat catre domeniul urmator
## Poti sa ai zone nesemnate. De ce?
 - dimensiunea zonei si fluctuatia informatiei in ea
 - semnarea: costisitoare algo cripto cu PK -> O(log n ^ 3)
## Unde se gaseste DNSec?
 - DNSec se gaseste la nivel de server si NU de client
