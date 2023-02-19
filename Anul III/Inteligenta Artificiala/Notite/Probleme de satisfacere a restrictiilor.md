----
## Ce este o solutie?
 - asignare completa pentru toate variabilele astfel incat toate restrictiile sunt satisfacute
## Ce este dimensiunea domeniului?
 - este numarul posibil de valori ramase => Consider variabilele cu cele mai putine valori, pentru ca vreau sa identific cat mai repede esecul
## Conflict-Directed Backjumping
 - pui o valoare la nodul respectiv si marchezi nodurile adiacente ce sunt in conflict cu nodul precedent
 - ce inseamna conflict? daca am un nod cu multimea de valori {1, 2} si nod adiacent cu multimea de valori {2, 3, 4} si iau valoarea 2, se afla in conflict. Daca iau valoarea 3, nu mai sunt in conflict
 - slide 41 din cursul IA_4_CSP.pdf ![[Conflict-Direced Backjumping.png]]
## Ce sunt variabilele discrete?
 - domenii finite (boolean) sau infinite (intregi)
## Ce sunt variabile continue?
 - timpi de inceput/sfarsit
## Ce este Minimum-remaining-values? (MRV)
 - alege variabila cu cele mai putine valori permise (variabila constransa)
## Ce este Least-constraining-value?
 - alege valoarea cea mai putin constransa (cea care exclude cele mai putine valori) -> cele mai multe variante
## Ce este Forward checking?
 - actualizeaza domeniul varabilelor neasignate
 - cand selectam o valoare pentru o variabila, elimina valoarea din domeniul variabilelor neasignate, conectate cu acesta
## Algoritm Arc consistency
 - [https://youtu.be/4cCS8rrYT14](https://youtu.be/4cCS8rrYT14?fbclid=IwAR3VyxVTixT8sI8n1_GsI8yZ2Nw4ZjE92wOkD5DTE_s7n7vPOMGAusI6tc0)
## Care sunt pasii algoritului AC?
 1) Transformi orice constrangere intr-un arc (ex: $A \neq B$ devine $A \neq B$ si $B \neq A$)
 2) Adaugi toate arcele in agenda
 3) Repetam pana cand agenda e goala
	 - iei arc din agenda si verifici $(X_i, X_j)$
	 - trebuie sa exista **CEL PUTIN O VALOARE** $X_j$ pentru $X_i$
	 - elimini valorile inconsistente de la $X_i$
	 - daca $X_i$ s-a schimbat, adauga toate arcele $(X_k, X_i)$ la agenda
## Exemplu de exercitiu cu Arc-consistency
 - ![[Arc_consistency.jpg]]
## Backjumping mai repede decat Backtracking
## Ce este incremental search?
 - este o cautare DFS
 - colorezi toate nodurile in prima culoare, dupa decolorezi pana cand este respectata constrangerea
**IMPORTANT**: de vazut exemplu_FRW_MRV
