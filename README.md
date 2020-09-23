# Targeting with Partial Incentives
<img src="https://evanemolo.com/assets/images/algorithms/graphs/nodes-edges.png" align="right" Hspace="15" Vspace="0" width=300 height=300
Border="0">
Progetto realizzato per il corso di Reti Sociali. <br>
Data una rete sociale rappresentata da grafo G = (V,E), dove V è l'insieme dei nodi
della rete, E è l'insieme degli archi che rappresentano i collegamenti tra i nodi della rete, ed una threshod function t: V → N dove t(v) indica il numero di adiacenti
attivi del nodo v necessari ad attivare v, si vuole trovare un insieme di nodi che sia in grado di influenzare l'intera rete.
Un **assegramento di incentivi parziali** ai vertici del grafo G con V = v<sub>1</sub>, ... , v<sub>n</sub> è un vettore s = (s(v<sub>1</sub>), ... , s(v<sub>n</sub>)) ∈ {0,1,2, ...} rappresenta la quantità di influenza applicata al nodo v ∈ V. <br>
Un **processo di attivazione** in G che inizia con un vettore di incentivi è una sequenza *Active[s,0]* ⊆ *Active[s,1]* ⊆ ...  ⊆ *Active[s,l]* ⊆ ... ⊆ V di sottoinsiemi di vertici con:
* *Active[s,0]* = {v: s(v) > t(v)},
* *Active[s,l]* = *Active[s,l-1]* U {u: |N(u) ∩ *Active[s,l-1]*| ≥ t(u) - s(u)}, ∀l>0.
### Obiettivo
Un **vettore target** s è un'assegnazione di incentivi parziali che innesca un processo di attivazione che influenza l'intera rete, cioè tale che *Active[s,l]* = V per un *l*≥0. L'obiettivo è trovare il vettore s che minimizza il totale degli incentivi per avere *Active[0,∞]* = V , cioè un vettore s che minimizzi *C(s)* = Σ s(v) ∀ v ∈ V.
### Implementazione
L'algoritmo presentato è stato implementato utilizzando Python 3.6 e la libreria SNAP per la manipolazione dei grafi.
Si utilizza un modello di attivazione con threshold; dato un grafo non direzionato G = (V,E), una threshold function *t* : V → N e una distribuzione di probabilità associata agli archi di G, *p* : E → [0,1]:
* Applicare il *principio di decisione differita*: per ogni arco *e* del grafo viene generato un numero pseudocasuale *x* compreso tra 0 e 1. Se *x* < *p(e)* (cioè il nodo infetta con una probabilità inferiore rispetto a quella richiesta), allora l'arco *e* viene rimosso dal grafo.
* Eseguire l'algoritmo sul grafo ottenuto: il grafo è dato in input all'algoritmo che calcola la soluzione. Questa procedura è iterata 10 volte, poi viene calcolata la dimensione media delle soluzione ottenute.
### Risultati
I risultati ottenuti vengono rappresentati mediante i seguenti grafici. Sulle ascisse sono riportati i valori di trheshold utilizzati, mentre sulle ordinate è riportata la size
delle soluzioni trovate dall’algoritmo. In Figura 1 è mostrata l’esecuzione dell’algoritmo, dopo aver applicato il principio di decisione differita al grafo, utilizzando thresholds costanti per tutti i nodi. In particolare, si è partiti assegnando ad ogni nodo una threshold pari a 1, e successivamente si è incrementata la threshold ad ogni esecuzione. Dato il gran numero di nodi e archi, l’incremento avviene con uno step pari a 2, e ci si è fermati al valore 11, che corrisponde al grado medio.
<img src="constant_plot.png" align="center" Hspace="250" Vspace="0" width=500 height=500 Border="0">
