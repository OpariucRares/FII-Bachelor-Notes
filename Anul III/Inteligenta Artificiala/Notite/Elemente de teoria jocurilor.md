----
## Ce este un joc?
 - problema interactiva de decizii
 - problema de cautare adversariala
## Care este scopul unui joc?
 - atingerea unei stari finale favorabile noua
## Strategia MINIMAX
 - ideea care este: ai doi agenti, MIN si MAX. Si trebuie sa iei nodul in functie de agentul respectiv
 - se alterneaza intre cei 2 agenti
 ![[Algoritmul MINIMAX.png]]
## Optimizare Alpha-Beta
 - este o optimizare al algoritmului MINIMAX
 - se pastreaza doua valori $\alpha = limita \space superioara$ si $\beta = limita \space inf erioara$ 
 - aceste limite se calculeaza in functie de agenti
 - https://www.youtube.com/watch?v=_i-lZcbWkps
 - ![[Algoritmul MINIMAX cu optimizare alpha-beta.png]]
## Ce este o strategie Paretto optimal?
 - indiferent de ce alegi, un player va avea un castig mai mare, dar va pierde castigul celuilalt player
## Ce este o strategie pura?
 - se alege mereu una (aceeasi) din optiuni
 - O strategie e mai buna daca are payoff-ul mai bun fata de ce face adversarul
## Ce este un Nash Equilibrium?
 - se urmareste maximizarea castigului propriu
 - ex: MINIMAX este echilibru Nash pt sah
**Obs**: uita-te la laborator, cursul e ambiguu
## Ce este o strategie dominanta?
 - este o strategie care mereu are u payoff mai bun fata de alte strategii
 - Obs: o strategie e strict dominanta, daca o linie/coloana e mai buna fata de restu
## Cum gasesti un Nash Equilibrium?
 - mergi pe linie pentru valorile din stanga si pe coloane pt valori de sus
1) Gasesti o strategie dominanta pentru ambii playeri si intersectia lor e solutia
2) Gasesti o strategie dominanta fata de cealalta, o elimini pe aia mai mica si continui asa pana la final. Te uiti ori pe linie, ori pe coloana, respectand conditiile de mai sus
3) Te uiti la varianta cea mai buna, atat pt valorile din stanga, cat si cele de sus. Pentru valorile din stanga, iei toate liniile si coloana 1, 2, etc si iei maximul pe coloana. Invers pentru valorile de sus. Iei pe coloana si dupa linia 1, 2, etc. In patratele in care ai ambele subliniate, ala e un Nash Equilibrium.
## Daca nu gasim un Nash Equilibrium, ce facem?
  - facem cu probabilitati: pt valorile de sus, avem pl si 1-pl si valorile din stanga pu si 1-pu.
  - Facem calcule pe coloana/linie pentru valorile de sus/stanga: consantele luate de pe coloana se inmultesc cu variabile laute de pe linie si invers
  - ex: -3 * pu + 1 * (1 - pu) = 2 * pu + 0 * (1 - pu)
  - faci calcule si obtii pu. La fel si pt pl. Uita-te la laborator pt explicatii mai bune.
  - ACEST LUCRU FUNCTIONEAZA PENTRU MATRICI 2x2. Idee: daca ai o matrice care nu e patratica si nu are Nash Equilibrium, te folosesti de eliminari prin strategia dominanta si cand ajungi la o matrice 2x2, aplici probabilitatile