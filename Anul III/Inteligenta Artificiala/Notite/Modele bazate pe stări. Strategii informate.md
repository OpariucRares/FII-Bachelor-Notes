----
## Ce este o euristica?
 - o functie ce se aplica pe orice stare, returneaza valori extreme si opuse pentru toate starile si pentru cel putin o stare finala
 - trebuie sa fie usor de computationat
 - nu poate supraestima distanta, dar o poate subestima
 - incearca sa calculeaza distanta pana la starea finala
## Ce este o euristica admisibila?
 - este o euristica care nu supraestimeaza niciodata
## Ce este Hillclimbing?
 - alegi pe cear care e cel putin la fel de buna
 - se alege doar o stare cu scorul >= scorul starii curente
 - Metoda FIRST
 - **Alta Varianta:** Hillclimbing cu BKT
## Cum se alege cu metoda Greedy?
 - se ia varianta cea mai buna (>, FARA >=)
 - metoda BEST
## Ce este A*?
 - caut starea are scorul cu 1 mai putin, pana ajung la starea initiala
## Metode de a te uita la solutii 
1) Cale intr-un graf (Greedy): mai rapida decat DFS, dar nu ofera mereu solutia optima; Dezavantaj: DFS cu decizii proaste
2) Hillclimbing: cea mai rapida geenrala; Dezavanta: nu gaseste o solutie, se blocheaza (minim local)
3) Simulated annealing: Hillclimbing, mai incet, dar nu mai are optim local
4) A* Algorithm: euristica aleasa + distanta de la starea initiala

**IMPORTANT**: UITA-TE LA Lab3_AStar_Example si rezolvarea corecta si completa la A_start_by_me
 - tu pui nodurile in PQ si le scoti in functie de rezultatul cel mai mic
 - cand l-ai scos din PQ, nu mai ai treaba cu el dupa
 - mereu calculezi distanta de la nodul initial pana la nodul vecin cu nodul scos din PQ ce trece prin nodul scos din PQ (pe desen e mai usor)
 - cand vizitezi un nod nou, verifici la parents daca are parinte sau noua distanta e mai buna decat cea initiala. In ambele cazuri, schimb parintele
 - te opresti cand ai scos nodul final
 - Avantaj la A*: mult mai rapid datorita euristicii
 