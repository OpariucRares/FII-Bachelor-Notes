----
Tags: [Securitatea_Informatiei]
## **Definitie**
- Control Accesul este un set de reguli in care utilizatorii pot accesa o resursa intr-un sistem
- Drepturi noi in sistem -> brese de securitate
- Ce aduce Control Acces?
  - Autentificare, Autorizare 


## Entitati (elemente):
- utilizator: cel care acceseaza resursele
- subiect: proces care actioneaza pentru user (activ)
- obiect: resursa in sistem care urmeaza sa fie accesat (pasiv)
- operatie: subiect asupra obiectului
- permisiuni: forma sub care un subiect acceseaza un obiect

**OBS**: Exemplu de entitati
  - baza de date -> obiectele sunt relatii
  - subiect poate fi privit ca un obiect -> proces ce cheama alt proces


## **Principiul privilegiului minim** 
 - orice program sau user sa aiba nevoie de minimul necesar de privilegii


## Ce elemente sunt intr-o politica?
 - **Politica** - reguli de control acces intr-un limbaj de nimvel inalt
 - **Modele (pseudocod)** - reprezentare grafica a politicii si cum funcitioneaza control accesul
 - **Mecanism** - pune in practica modelul (hardware)


## **Exemple de politici**
 - politici discretionare (DAC) [[Politica DAC]] , mandatate (MAC), bazate pe roluri (RBAC), bazat pe atribute (ABAC) (ultimul mai putin)
Exemple de modele
  - graf, matrici, logica
Exemple de mecanisme
 - monitorizare - se intampla un proces, trebuie sa stim cine a invocat procesul si unde l-a folosit
 - izolare - aparare la atacuri externe
 - verificabilitate - functionare corecta la monitorizarea CA 
 - flexibilitate - sa paote oferi oricui drepturi
 - scalabilitate, manageability

**Auditarea** - etapa intermediara intre solicitarea facuta de utilizator si accesul la resurse


