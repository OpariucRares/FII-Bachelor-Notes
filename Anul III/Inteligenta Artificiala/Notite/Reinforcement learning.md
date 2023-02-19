----
## Ce cuprinde reinforcement learning?
 - o sarcina: sa mearga fara a se lovi de gheata
 - actiuni posibile: ii revin agentului
 - mediu: furnizeaza stari urmatoare ce realizeaza recompensele
 - Scop agent: maximizarea recompenselor
## Ce este o politica?
 - ce actiune realizeaza agentul in starea curenta
## Ce tipuri de medii sunt?
 - determinist: actiuni de probabilitate egala
 - nedeterminist (stochastic): se ajunge intr-o stare cu o anume probabilitate
## Presupunerea Markov
 - starea curenta depinde de un numar finit de stari anterioare (de ordin intai: depinde doar de starea anterioara)
## Proces de decizie Markov
 - problema de decizie secventiala pentru un mediu stochastic cu un model de tranzitie Markov si recompense aditive
      - Stari $s \in S$ (stare initiala $s_0$), actiuni $a \in A$
      - Modelul de tranzitii P(s'|s, a)
      -   Functia recompensa R(s)
      - s stare; (s, a, s') tranzitie P(s'|s,a), R(s, a, s')
      - muchiile sunt recompensele; tranzitia: ai ajuns la starea s' din starea initiala s, a
	    ```mermaid
	    graph LR;
			s -->|a| s,a
			s,a -->|s,a,s'|s'
## Scopul MDP (Markov Decision Process)
 - politica optima $\pi^*$ (identificarea actiunilor pt tranzitiile intre stari)
## Ce tipuri de recompense sunt?
1) Recompense aditive
$$U_h([s_0,s_1,s_2,..]) = R(s_0) + R(s_1) + R(s_2) + ...$$
2) Recompense actualizate (discounted) 
$$U_h([s_0,s_1,s_2,..]) = R(s_0) + \gamma R(s_1) + \gamma ^ 2 R(s_2) + ...$$
## Ce este factorul de actualizare? (discount factor)
 - recompensele viitoare conteaza mai putin decat cele imediate
 - maximizeaza suma recompenselor
 - prefera recompensele curente, nu cele de mai tarziu
 - valorile recompenselor scad exponential
 - Ex: $\gamma = 0.5 \space si \space U([1, 2, 3]) = 1 * 1 + 0.5 * 2 + 0.25 * 3; U([1, 2, 3]) \lt U(3, 2, 1)$
 | 10  | ?   | ?   | ?   | 1   |
 | --- | --- | --- | --- | --- |
 | a   | b   | c   | d   | e   |
 - in functie de recompensa, vedem cum se modifica politica. Modificarea lui $\gamma$ poate modifica politica
 - De exemplu, sunt pe pozitia c si trebuie sa calculez cele doua castiguri (stanga, dreapta)
 - U(c) = R(c) + $\gamma$ R(b) + $\gamma ^2$R(a) (stanga) 
           = R(c) + $\gamma$R(d) + $\gamma^2$R(e) (dreapta)
 - Rezultatele difera pentru $\gamma = 0.1$ si $\gamma = 1$ 
 - OBS: cand calculezi, iei recompensa de pe pozitia initiala  
## Ecuatia Bellman
$$U(s) = R(s) + \gamma\max_{a \in A(s)}\sum\limits_{s'} P(s'|s, a)U(s')$$
Exemplu: ![[Ecuatia_Bellman_Dem_1.png]]![[Ecuatia_Bellman_Dem_2.png]]
## Ce scop are policy iteration?
 - ai o politica deja stabilita, trebuie sa vezi daca e politica optima sau trebuie sa o schimbi
 - modificam politica pana cand nu se schimba
## Care sunt pasii din policy iteration?
1) Pasul 1: avem politica, aplicam ecuatia Bellman imbunatatita
 - $$\large U_{i + 1} = R(s) + \delta \sum_{s'}P(s'|s, \pi_i(s))U_i(s')$$
2) Pasul 2: Policy Evaluation (imbunatatirea)
 - $$\large a_i^* = max_a\sum_{s'}P(s'|s,a)U(s')$$
 - am obtinut valorile din politica si vedem ce decizie trebuie sa ia de fapt (aia maxima)
## Cum functioneaza policy iteration pe un exemplu?
- https://www.youtube.com/watch?v=ghbGffXAYfk&t=164s
- ![[policy_iteration.jpg]]
## Iterarea valorilor
- aici avem de calculat politica noastra
- se foloseste de formula lui Bellman cu maxim. 
- calculezi toate variantele pentru pozitia initiala si vezi ce decizie va lua
- ![[value_iteration.jpg]]
## Ce este spatiul de actiune?
 - ce posibilitati are agentul
## Algoritmul Temporal Differences learning
 - Ecuatia Bellman pentru calcul utilitatilor si actualizeaza doar starile afectate
 - Ecuatia diferentelor temporale: calculeaza diferanta dintre utilitatea strii urmatoare si utilitatea starii curente
 - $$U^{\pi}(s) = U^{\pi}(A) + \alpha (R(s) + \delta U(s') - U(s))$$
 - este de forma (C, East, C, -2) ce reprezinta (unde suntem, directia, unde ajungem, recompensa)
## Exemplu de Temporal Differences learning
- ![[temporal_difference_learning.png]]

## Algoritmul Q-Learning
 - Formula de updatare
 $$Q(s, a) = Q(s, a) + \alpha(R(s, a) + \gamma\max_{a'}Q(s', a') - Q(s, a))$$
 - s - starea curenta; a - actiunea pe care am luat-o; R(s, a) - reward-ul pe care l-am obtinut; s' - noua stare
 - $\max_{a'}Q(s', a')$ - valoarea maxima Q pentru noua stare
 - $\alpha$ - learning rate; $\gamma$ - factorul discount
 - Exista cazuri cand un agent alege o cale, dar nu este cea mai buna cale. Introducem un nou parametru $\epsilon$ - greedy. Cu o sansa de $\epsilon$, luam o actiune random. Cu o sansa de $1 - \epsilon$, luam o actiune ce maximizeaza Q
 - La inceput, $\epsilon$ incepe de la 1, dar la fiecare episod, acesta scade ($\epsilon = {\epsilon * decay}$, unde decay ia valori intre 0 si 1 (0.9, 0.99, 0.999))
 - exercitiu explicat in ExercitiuQLearning.pdf