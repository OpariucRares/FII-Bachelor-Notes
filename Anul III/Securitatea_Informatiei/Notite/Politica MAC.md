----
## Ce proprietati are accesul MAC?
 - controleaza accesul o autoritate generala
 - guvernate de reguli clare, stabilite a priori
 - distinctia dintre intre user si subiect (ca sa eviti atac de cal trojan)
 - orientata pe proprietatile de securitate: integritate, confidentialitate, separarea indatoririlor
 - orientata pe proprietate
## Ce sunt modelele flux de informatii (information flow)?
 - information flow (transfer de informatii)
 - subiectii si obiectii se impart in clase organizate ierarhic
 - informatia circula de jos in sus sau invers, dar se stabileste care este sensul
 ```mermaid
 flowchart TB
	 a_nivele_superioara_securitate_superioara --> b & c--> d
	 d --> e & f --> g_jos:_obiecte_publice
```
## Ce este o clasa de securitate si cum este reprezentata?
 - Clasa de securitate: multime de subiecte si obiecte
## Cum este reprezentata o clasa de securitate?
 - IF : (SC, ->, xor) (information flow, security class)
1) SC = multime de clase de securitate
2) relatie binara, relatie de transfer de informatii
3) xor : SC x SC -> SC => ne arata cum se combina informatia din 2 clase de securitate diferite
## Care sunt axiomele Denning?
1) SC finit
2) -> reprezinta o ordine partiala (intr-un singur sens)
3) SC contine un cel mai mic element relativ la relatia de ordine partial (exista o unica clasa de info publice)
4) xor least upper bound operator - combinarea dintre cele doua clase sa obtina cea mai mica clasa posibila
 - **OBS**: Orice IF ce respecta Axiomele Denning este o latice (orice parte finita are un majorant si un minorant)
 - Nu exista drum intre 2 elemente -> clase incomparabile
## Ce modele MAC exista
 - MAC pentru confidentialitate 
 - MAC pentru integritate
## MAC pentru confidentialitate (Modelul Bell-LaPadula)
 - initial pentru scop militar
 - Clasa de securitate este alcatuit din subiecte si obiecte reprezentate prin asociere de etichete
 - Modelul BLP (Bell-LaPadula)
 - model bazat pe confidentialitate
 - Aprroach in 2 pasi
	 - matricea de acces discreption este stabiliti
	 - operatiile sunt autorizare de politicile MAC
	 - initial pt drepturi de R = {r, w}
### Ce functie are modelul BLP?
 - $\lambda$ = functie ce stabileste eticheta de securitate pentru subiecti si obiecte
 - clase superioare pot citi clase inferioare DAR NU INVERS
### Care sunt regulile de scriere si citire?
1) Regula de securitate simpla (ss) (de citire)
	- subiectul s poate citi obiectul o daca $\lambda(s) \geq \lambda(o)$ (in latice)
2) Regula * (de scriere)
	- subiectul s poate scrie in obiectul o daca $\lambda(s) \leq \lambda(o)$ 
	- informatii mai putin confidentiale pot fi transmise catre clase cu un nivel de securitate mai mare
 - **OBS**: Regula \*-strong: subiectul s poate scrie in obiectul o daca lambda(s) = lambda(o)
ex: imaginea Curs9_4.jpg de sus
 - pot fi adaugate proprietati de distrugere sau de creare
## Sinteza modelul BLP
 - este model de confidentialitate
 - asociem $\lambda(s), \lambda(o)$ (asociem subiecti) (etichete de sec. pt. subiecti, obiecte)
 - etichetele de securitate sunt ordonate partial intr-o latice
 - un subiect s poate citi un obiect o daca $\lambda(s) \geq \lambda(o)$
 - un subiect s poate scrie intr-un obiect o daca  $\lambda(s) \leq \lambda(o)$
 - putem combina BLP cu DAC!!
	 - daca control acces in matrice nu este permis, atunci nu are rost sa ne folosim de politicile MAC pentru ca oricum o sa fie rejectat

## MAC pentru integritate
- subiecte si obiectele sunt impartite in clase de securitate numite clase de integritate (pot fi speificate prin etichete de integritate)
 - o = eticheta de integritate (masoara gradul de integritate al obiectului)
 - s = eticheta de gradul de integritate al subiectului in sensul lucrului cu informatii
### Modelul BIBA
 - functia este $\omega$
1) Regula de integraritate simpla (si)
	- subiectul s ii este permis sa citeasca pe obiectul o daca $\omega(s) \leq \omega(o)$ (nu am voie sa citesc in jos)
2) Regula * pentru integritate
	- subiectul s ii este permis sa scrie in obiectul o daca $\omega(s) \geq \omega(o)$
## Sinteza BIBA
 - model de integritate
 - sub., ob. -> etichete de integritate
 - etichetele structurate intr-o latice
- flux de informatii de sus in jos
- s poate citi o numai daca$\omega(s) \leq \omega(o)$
- s poate scrie in o daca $\omega(s) \geq \omega(o)$
- Biba se poate combina cu DAC
## Combinare BLP cu BIBA
1) Etichete care masoara atat integritatea, cat si confidentialitate
	- citirea se poate realiza daca $\lambda(s) \geq \lambda(o)$ si $\omega(s) \leq \omega(o)$
		- rezulta ca este doar din aceeasi clasa
2) Utilizam 2 latici: confidentialitate, integritate
3) Combinam 2 latici, una pentru confidentialitate, una pentru integritate intr-o singura latice
	- citire: $\lambda(s) \geq \lambda(o)$ si $\omega(s) \geq \omega(o)$
	- scriere: $\lambda(s) \leq \lambda(o)$ si $\omega(s) \leq \omega(o)$


## Separation of Duty (separarea indatoririlor)
- ex: o persoana poate face si examinare si rezolvarea contestatiilor dar nu in aceeasi sesiune

## Ce model MAC exista care se foloseste de SoD?
 - Modelul Chinezesc (produs de Brewer si Nash)

## Ce elemente sunt din Modelul Zidul Chinezesc?
 - Obiect = orice informatie importanta pentru respectiva companie
 - Dataset = multimea obiectelor unei companii
 - Clasa de conflict de interese (CIC) = multimea maximala de companii int competitie
 - subiect = orice utilizator care are acces la obiectele unei companii sau un program care ruleaza pentru un anumit user
## Care este scopul acestui model?
 - Un utilizator realizaeaza o operatie de citire datele unei companii -> se creeaza un zid chinezesc in jurul lui
 - operatia de scriere este restrictionata numai in interiorul zidului

## Care sunt regulile de scriere si citire?
1) Regula simpla de securitate
   - un user poate citi datele companiei daca compania se afla in interiorul zidului SAU
compania e intr-o clasa de conflict de interes

2) Regula de scriere (proprietatea *)
	- utilizatorul poate citi daca are drept de citire si utilizatorul nu mai citeste din niciun alt dataset (chiar daca se afla intr-o clasa de conflict de interese (CIC))
	- adica ori nu scrie ori scrie si citeste dintr-un singur dataset

## Cand este folosit acest model?
 - functioneaza daca e o singura companie

## Cum se poate relaxa modelul?
 - introducerea conceptului de principal
 - User-Principal-Subiect (avem incredere in user, dar nu la nivel de subiect)

## Ce implementari MAC exista
1) SELinux (Security-Enhanced Linux)
	- creeaza clase de securitate, prin intermediul carora este dirijat fluxul informational
	- 1998 introdus de AppArmor
	- propus in 2000 de catre RedHat
	- reguli intr-un fisier -> politica de acces pentru aplicatia respectiva
## Ce vulnerabilitati are MAC-ul?
 - Convert channels (canale sub acoperire)
 - canale de transmisie neautorizate intre 2 useri care permite scurgeri de informatii auxiliare
## Ce tipuri de canale sub acoperire exista?
 - storage channels - modifica locul in care se intampla comunicarea
 - timing channels - permite o intarziere a transmisiei pachetelor
 - nu exista metoda de a le detecta
## Sinteza MAC
 - se bazeaza pe crearea de clase de securitate (laticeal)
 - general, nu acordate de proprietarul fisierului (care nu exista)
