----
## Ce sunt probabilitatile conditionate?
$$P(a|b) = \frac{P(a \cap b)}{P(b)}$$
## Ce este o inferenta probabilista?
 - calculul probabilitatilor conditionate, date fiind anumite observatii
 ![[Inferenta probabilista.png]]
## Ce este o probabilitate marginala?
 - distribuitia peste o submultime de variabile
 - marginalizare: insumam probabilitatile pentru fiecare valoare posibila a celorlate variabile
 - $$P(Y) = \sum\limits_{z \in Z}P(Y, z) $$
 - ![[Probabilitate_marginala.png]]
## Care este teorema lui Bayes?
 - $P(I|E) = \frac{P(E|I)P(I)}{P(E)}$
## Interogare simpla
 -  $P(x_1,x_2,...,x_n) = \prod\limits_{i = 1}^nP(x_i|parents(X_i))$ (calculezi in functie de parinti)
## Inferenta unei probabilitati marginale
 - $P(A) = \sum\limits_nP(A|B_n)P(B_n)$
 - daca ai de calculat un nod, iei doar nodurile care au legatura cu nodul ales (slide42-43 din curs)
 - ![[Inferenta probabilitatilor marginale 1.png]]
 - ![[Inferenta probabilitatilor 2.png]]
 - ![[Inferenta probabilitatilor 3.png]]
## Inferenta prin enumerare
 - $P(X|e) = \alpha P(X, e) = \alpha \sum\limits_{y} P(X, e, y)$ 
 - X - variabila de care ne intereseaza
 - e - variabilele observabile
 - $\alpha$ - coeficient de normalizare (ex: $\frac{1}{P(e)}$)
 - y - variabilele neobserabile, ce nu sunt in e
## Cum se rezolva reletele bayesiene?
 - rezolvari in ex1.pdf si ex2a.pdf + Curs IA_11_retele_bayes.pdf incepand cu slide-ul 42 si in AI_Lab_11.pdf
 - te folosesti de interogarea simpla + inferenta prin enumerare ca sa calculezi probabilitatile
 - iei cazul pentru X si not X si impreuna trebuie sa dea 1
 - de aici, iei $\alpha$ si aflii probabilitatea 
 - 