----
Tags: [Securitatea_Informatiei]

### Ce inseamna DAC? 
 - model discretionar (de tip matriceal)

### Proprietati
1) CA (Control acces) pe baza identitatii utilizatorilor
2) "Discreptionar" -> este la discretia proprietarului de a oferi drepturi la resursa respectiva
3) Include "proprietar al resursei" ca drept in sistem 
4) Model de tip stare-tranzitie
	- stare: drepturile unui user la o resursa la un timp dat
	- tranzitie: cum se schimba starea atunci cand se aplica o regula din politica de CA

### Model bazat pe matrici
 - Model bazat pe matrici (ACM - access control matrix)

### Proprietati
1) IMPORTANT: SUBIECTII SUNT SI OBIECTE
2) Un proces poate avea drept de executie asupra altui proces
3) Cum este definita matricea? 
	- liniile sunt subiectii 
	- coloanele sunt obiecte
	- o celula - ce drept are subiectul pe acel obiect
4) Cum este definit ca un graf?
	- punctele negre sunt subiectele, punctele albe obiecte
	
ex: slide 5/45 din 5. IS-Access_Control_DAC [[5. IS-Access_Control_DAC.pdf]]

**IMPORTANT**:  SUBIECTII SUNT SI EI OBIECTE

|       | file1 | file2 | device | user | mount | root |
| ----- | ----- | ----- | ------ | ---- | ----- | ---- |
| user  |       | r, w  |        |      | x     |      |
| mount |       |       |        |      |       | t     |
| root  | r, w  |       | r, w   |      |       |      |

### Cum se scrie?

- avem tripleta (S, O, A)
	- S - subiectii; 
	- O - obiectele; 
	- A - este matricea de acces; 
	- R - rights
	
- Comanda - alcatuita dintr-o garda (cerinte ce trebuie indeplinite) si operatii primitive
- Operatii primitive sunt: adaugarea sau stergerea unui drept, crearea/distrugerea unui obiect/subiect
- **IMPORTANT**: Comenzile verifica doar existenta drepturilor, nu si lipsa lor

### Crearea unui subiect
- trebuie sa fie nou subiectul, inexistent in sistem
|                               | op substitutie |              |
| ----------------------------- | -------------- | ------------ |
| (S, O, A) : starea sistemului | ============>  | (S', O', A') |                              |                |              |

|                             | op  |               | op  |               |
| --------------------------- | --- | ------------- | --- | ------------- |
| (S, O, A) = (S_o, O_o, A_o) | ==> | (S_1,O_1,A_1) | ==> | (S_n,O_n,A_n) | 

### Ce este sistemul de protectie?
 - multime de comenzi ce se pot aplica pentru a controla accesul la resurse
 - **IMPORTANT**: Scurgerea de drepturi este nedecidabila

### Cum reprezentam tabela?
1) Tabele de autorizare, similar BD
2) Liste de control al acceslui (ACL) - coloane ale ACM
3) Lista de capabilitati/capacitati - liniile ACM

 - Gupam sub/obiectele: dreapturile sa fie acordate pe grupuri
 - Tabel de autorizare - 3 coloane (subiect, acces, obiect) -> DB
### Avantaje si dezavantaje ACL
 - simplu de facut
 - buna pt environmentul in care user-ul is face singur management asupra propriilor resurse
 - nepotrivit cand populatia se schimba constant
 - program invocat de un user ce afecteaza un alt user pe o perioada de timp
 - greu de verificat securitatea la runtime (SO stie ce program functioneaza decat sa vezi care fisier a fost autorizat)
 - tedious sa vezi toate fisierele ce un user are acces 
### Drepturi speciale in UNIX
 - Drepturi de acces => read, write, execute
 - Permisiuni - owner (user), group (g), other (o) - fiecare un bit
 - Primul bit reprezinta  ce tip de fisier este: fisier, director
 1) Set user id (SUID) 
	- numai pentru fisierele
	- in zona owner se scrie
	- specificia s sau S:
		*  s: obiectul, indiferent unde se afla, in orice folder, poate fi executat de dr. proprietarului
		* S: nu exista drepturi de executie al fisierului (nici pt owner, nici pt destinatarului fisierului)
		
 2) SGID
	- se refera la foldere
	- se specifica in zona 3 de la other
	- specif. t: interdictia de a sterge fisiere din director (doar proprietarul sau root-ul)

- ex: passwd -> schimbarea parolei, poz 3 in zona utilizatorului:s: userul o poate schimba cu drept de root
### Lista de capacitati
- Notatie: C_s: (o1, r1^1),..,(o1, r1^k1),..,(o_m,r_m^(k_m))
- ticket (o, r)
- implementare ticket (o,r) -> s
- evitare falsificare tickete -> s :(autorizare) -> verificare integritate ACL_o
- propagarea controlului: transferul de tickete de la un subiect la alt subiect

### Lista de control al accesului vs Lista de capacitati

| dasd                                              | Lista de control al accesului (ACL)            | Lista de capacitati                  |
| ------------------------------------------------- | ---------------------------------------------- | ------------------------------------ |
| Autorizare                                        | autorizarea proprietarului si integritatea ACL | integritatea si controlul propagarii |
| Access review                                     | obiecte                                        | subiect                              |
| Revocation                                        | subiecti                                       | obiecte                              |
| Modelarea principiului de nr. minim de privilegii | implementare anevoioasa                        |                                      |

**IMPORTANT**: FOLOSITI MAI MULT ACL DECAT CAPACITATI

### Alte modele DAC
1) Model propus de Lipton si Snyder
	- sistem bazat pe stare-tranzitie
	- subiectii nu sunt obiecte
	- modelul este ca un graf orientat unde nodurile sunt subiectii si obiectele iar arcele sunt un set de reguli
	- regulile sunt:
		- take (t): s ii poate lua toate drepturile lui s'
		- grant (g): s ii poate lua toate drepturile lui s'

	- Dezavantaj - mai putin expresiva
	- "scurgerea de drepturi" se verifica in O(n^2) unde n sunt numarul de noduri
	- folosit pt detectarea de anumite vulnerabilitati in retea

2) Model schematic - mai mult teoretic decat practic
	- SLABICIUNE MAJORA al DAC-ului este ATACUL DE TIP TROJAN (nu exista antidot general)
	- def: software rogue ce face actiuni ilegale, nestiute de user, exploitand privilegiile de acces
	- control acces nu ia in calcul modul in care ar trebui sa circule informatia in sistem (intre ce entitati)
## Conclusion
- separea subiecte de obiecte tin controlul flow-ului de informatii
