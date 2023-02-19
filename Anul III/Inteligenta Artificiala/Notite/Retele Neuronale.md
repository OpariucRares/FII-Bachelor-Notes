----
## Ce este o retea neuronala artificiala?
 - Un ansamblu de unitati functionale (neuroni) interconectate
## Diferenta dintre clasificare si regresie?
 - tipul iesirii (discret vs. continuu)
## Ce este un perceptron?
 - un neuron artificial care utilizeaza functia de activare treapta
## Functii de activare perceptron
1) Functia de activare treapta
2) Functia de acticare semn
![[Functii de activare perceptron.png]]
## Reguli de antrenare a perceptronului
 - $w_i \leftarrow w_i + \Delta w_i$
 - unde $\Delta w_i = \eta(t - 0)x_i$
 - ![[Antrenare perceptron.png]]
## Ce este o retea neuronala multi-strat?
 - O retea neuronala cu propagare inainte (feed-forward) cu
   - un strat de intrare
   - unul sau mai multe straturi ascunse
   - un strat de iesire
   - semnalele de intrare sunt propagate inainte prin straturile retelei
   - calculele se realizeaza in neuronii din straturile ascunse si din stratul de iesire

## Ce functii de activare neliniara sunt?
 - fiecare layer (exceptand cel de input) are o functie de activare 
1) Functia sigmoida (logistica)
	$\LARGE f(x) = {1 \over 1 + e^{-x}}, f'(x) = {f(x)(1 - f(x)) }$
1) Functia sigmoida bipolara (tangenta hiperbolica)
    $\LARGE f(x) = {1 - e^{-2x} \over 1 + e^{-2x}}, f'(x) = {1 - f(x)^2}$
3) Functia ReLU (Rectified Linear Unit)
   $$f(x)=\begin{cases}0&daca \space x\lt 0\\x&daca \space x\geqq 0\end{cases}, \space \space f'(x)=\begin{cases}0&daca \space x\lt 0\\1&daca \space x\geqq 0\end{cases}$$
   ![[Functii de activare.png]]
## Algortimul Forward Propagation
 - Noi avem deja weight-urile calculate si bias-urile, doar inputul din noduri nu este calculat
 - daca avem de calculat un nod nou, luam (valoarea din nodul din layer-ul anterior) * weight-ul dintre nodul curent si nodul anterior; faci asa cu toate nodurile adiacentele din layer-ul anterior + bayes-ul calculat pentru nodul respectiv
 - rezultatul final trece prin functia de activare (in cazul nostru functia sigmoida) si acela va fi rezultatul
 - Slide-urile 25 - 51 din AI - Lab 6.pdf
 - Implementarea se face cu matrici

## Ce este squarred error?
 - calculezi eroarea dintre nodurile obtinute in layer-ul final si ce ne dorim de fapt
 - valoarea mai buna este asignat pentru valorea 1
 $$y = \begin{pmatrix}0.65\\0.2 \end{pmatrix} \space si \space rezultatul \space t = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$$  $||y - t||^2 = {(0.65 - 1)^2 + (0.2 - 1)^2} = {0.7625}$
## Ce este mean squarred error?
 - Pentru fiecare entry din dataset, generezi targe vectorul si calculezi output-urile .
- $\LARGE C(w, b) = {1 \over 2n }{\sum\limits_{x} ||y - t||^2}$
- n - numarul de intrari din setul de date de antrenare (sau de test)
- x - o intrare
- y - vectorul de output pentru entry x
- t - target vector pentru entry x
- ||v|| - lungimea vectorului

## Ce este o epoca?
 - o epoca reprezinta un forward propagation si un backward propagation
## Notatii
 - L - ultimul layer
 - $y_{i}^l$ - neuronul de activare i de la layer-ul l
 - $b_{i}^l$ - bias-ul neuronului i de la layer-ul l
 - $w_{i, j}^l$ - weight-ul de la neuronul i de la layer-ul l-1 la neuronul j din layer-ul l
## Dupa forward propagate, faci backward propagate. Cum?
1) Calculezi eroarea din layer-ul final (nod_curent = nod_curent(1 - nod_curent)(nod_curent - target_vector_pe_poz_respectiva))$$\delta_{i}^L = y_i^L (1 - y_i^L) (y_i^L - t_i) $$ 
2) Calculeaza eroarea din layer-ul precedent (nod_curent * (1 - nod_curent) * (suma care este formata din (nodul din urmatorul layer) * (weight-ul format din nodul curent si nodul adiacent din urmatorul layer)) -> INVERS
$$\delta_{i}^l = y_i^l (1 - y_i^l) \sum\limits_k \delta_k^{l + 1} \cdot w_{i, k}^{l + 1} $$
3) Calculeaza gradientul pentru weight-urile din layer-ul curent (derivata) (nodul curent * nodul din layer-ul precedent pe aceeasi linie)
$$\frac{\mathrm{\delta \space C}}{\delta \space w_{i, j}^l} = \delta_j^l y_i^{l - 1}$$
4) Calculeaza gradientele pentru baias-urile din layer-ul curent (valoarea nodului)
$$\frac{\mathrm{\delta \space C}}{\delta \space b_i^l} = \delta_i^l$$
5) Dupace ai facut o medie la gradient (pt fiecare weight si bias individual), updatezi weght-urile si bias-urile (alpha e learning reate-ul, iar n numarul de instante; te folosesti de formula de la pasul 3 pentru weight-uri si pentru bais-uri de folosesti de formula de la pasul 4)
$$weights: w_{i, j}^l = w_{i, j}^l - \frac{\alpha}{n}\sum\limits_a \delta_j^l y_i^{l - 1} \space si \space biasuri: \space b_{i}^l = b_i^l - \frac{\alpha}{n}\sum\limits_a \delta_i^l$$
Mai usor in folder-ul din Forward+Backpropagation.pdf
https://www.youtube.com/watch?v=tUoUdOdTkRw