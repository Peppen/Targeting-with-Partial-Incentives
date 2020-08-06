# Targeting with Partial Incentives
<img src="https://evanemolo.com/assets/images/algorithms/graphs/nodes-edges.png" align="right" Hspace="15" Vspace="0" width=300 height=300
Border="0">
Data una rete sociale rappresentata da grafo G = (V,E), dove V è l'insieme dei nodi
della rete, E è l'insieme degli archi che rappresentano i collegamenti tra i nodi della rete, ed una threshod function t: V → N dove t(v) indica il numero di adiacenti
attivi del nodo v necessari ad attivare v, si vuole trovare un insieme di nodi che sia in grado di influenzare l'intera rete.
Un **assegramento di incentivi parziali** ai vertici del grafo G con V = v<sub>1</sub>, ... , v<sub>n</sub> è un vettore s = (s(v<sub>1</sub>), ... , s(v<sub>n</sub>)) ∈ {0,1,2, ...} rappresenta la quantità di influenza applicata al nodo v ∈ V. <br>
Un **processo di attivazione** in G che inizia con un vettore di incentivi è una sequenza *Active[s,0]* ⊆ *Active[s,1]* ⊆ ...  ⊆ *Active[s,l]* ⊆ ... ⊆ V di sottoinsiemi di vertici con:
* *Active[s,0]* = {v: s(v) > t(v)},
* *Active[s,l]* = *Active[s,l-1]* U {u: |N(u) ∩ *Active[s,l-1]*| ≥ t(u) - s(u)}, ∀l>0.
### Obiettivo
Un **vettore target** s è un'assegnazione di incentivi parziali che innesca un processo di attivazione che influenza l'intera rete, cioè tale che *Active[s,l]* = V per un *l*≥0. L'obiettivo è trovare il vettore s che minimizza il totale degli incentivi per avere *Active[0,∞]* = V , cioè un vettore s che minimizzi *C(s)* = Σ s(v) ∀ v ∈ V.
