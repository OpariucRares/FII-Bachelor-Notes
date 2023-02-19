----
## Ce inseamna abordare bazata pe stari?
  - descriem o problema
  - modelam o problema a.i. sa poate fi modelata de calculator
  - calculatorul rezolva problema, ne ofera o solutie
## Ce este NP?
  - set de probleme ce pot fi rezolvate in timp polinimial de o masina Turing Non-determinista (exista un punct in care nu stim despre algoritm ce decizie va lua)
## Ce este NP-complete?
  - subset din problemele NP care pot fi reduse intr-un timp polinomial
## Ce este NP-hard?
 - probleme din set-ul NP care nu pot fi rezolvabile
 - exemplu de problema NP-hard rezolvabila (SAT)
 - exemplu de problema NP-hard nerezolvabila: Turing Halting
 ![[NP-complete problems.png]]
## Ce este o stare?
 - toate informatiile necesare pentru a continua recuperarea solutiei
 - Proprietati:
	 - Fara Ambiguitati, compact, expresiv, include toate datele necesare
## Ce stari speciale sunt? (aplicam pentru problema turnurile din Hanoi)
 - Stare initiala: de unde incepe algoritmul
 - Ex: Initial state(3, 1, 1, 1, 1, 1) -> primul numar reprezinta numarul de turnuri, iar restul este reprezentat asa: pozitia este marimea piesei si valoarea din pozitie reprezinta pozitia piesei pe turn (in cazul de fata, toate piesele sunt puse pe primul turn)
 -``
```
State Initializare (int n, int m)
{
	return State(n, 1, 1, ..., 1) de m ori
}
```

 - Stare finala: cand se termina algoritmul
 - Ex: toate piesele sa se afle pe ultimul turn, in oridinea corecta
```
boolean FinalState(State state)
{
	if state == (n, n, n, .., n) -> cate piese sunt
		return true;
	return false;
}
```
## Ce este o tranzitie?
 - este o trecere de la o stare la alta; se realizeaza in functie de restrictii
 - Exemplu de aici: toate numerele sunt pozitive, toate valorile sunt cel mult egale cu prima, o piesa mai mare sa nu fie peste o piesa mai mica
```
Boolean Validate(State s, piece, tower)
{
	//introduci toate if-urile necesare si la final return true sau false
}
```
## Strategia de cautare 
```
Void strategy(State s) 
{ 
	While (!isFinal(s)) 
	{ 
		//Choose piece, tower; 
		If (Validate (s, piece, tower)) 
			s = Transition(s, piece, tower); 
	} 
}
```
## Cum alegem strategia de cautare?
 - BFS - parcurgem BFS-ul pana cand ajungem in starea finala.
	- Dezavantaje: memorarea tuturor starilor explorate, nu pot demonstra ca solutia gasita e cea optima, vizitarea unei stari de mai multe ori
 - DFS - nu trec de 2 ori prin aceeasi stare
	 - Dezavantaje: trebuie sa retina fiecare stare generata, paote sa nu ajunga la final, poate vizita aceeasi stare de mai multe ori
 - BKT - NU TREBUIE SA RETINA STARILE VIZITATE  