- UNIVERSIDADE FEDERAL DO RIO GRANDE DO NORTE
- DISCIPLINA: ALGORITMOS E ESTRUTURAS DE DADOS II
- Grupo:
- Rychardson Ribeiro de Souza
- Thiago Jordão Melo da Costa

- Link do vídeo no Loom: https://www.loom.com/share/cb75e4d4888e4af69c4143da9d1abc39

- PARA O REPOSITÓRIO EM GERAL: 
- !pip install nxviz=='0.6.3'
- import networkx as nx
- import matplotlib.pyplot as plt
- import nxviz as nv
- import numpy as np
- import seaborn as sns
- import pandas as pd


- REQUERIMENTO 1: 
- In graphs, assortativity (or assortativity coefficient) is a measure that describes the tendency of similar nodes to connect to each other. It measures the preference of nodes to link to nodes of similar characteristics, such as attribute similarity or node degree.
The assortativity coefficient can vary from -1 to 1. A value close to 1 indicates a highly assortative network, where nodes with similar characteristics are more likely to connect. A value close to -1 indicates a distortive network, where nodes with different characteristics are more likely to connect. A value close to 0 indicates a neutral network, where the connection between nodes is not affected by its characteristics.

- Filtrando dados pelo país
nodesBrasil = []
for node in G.nodes():
  if G.nodes[node]['country'] == "BRASIL":
    nodesBrasil.append(node)

nodesG = G.subgraph(nodesBrasil)

Número de nós após a filtragem:  495
Número de links após a filtragem:  4402

- REQUERIMENTO 2: 
- Bivariate graph analysis refers to the study and exploration of relationships between pairs of nodes in a complex network. Rather than analyzing the properties of a single node in isolation, bivariate analysis considers the interaction between two nodes and examines how these interactions can affect the structure and functioning of the network.
In bivariate analysis, researchers investigate various characteristics and properties of pairs of nodes, such as attribute similarity, connection patterns, dynamic interactions, or statistical correlations

- First represented for Brazil, then for each of the regions

- REQUERIMENTO 3: 
- Determine how many connected components exist in the Brazilian air network. Characterize each component: quantity, percentage by region.

- REQUERIMENTO 4:
- Create a simulated scenario where a trip with the following route is desired:

- City 1 (North) to City 2 (South)

- City 2 (South) to City 3 (Northeast)

- City 3 (Northeast) to City 4 (Central-West)

- City 4 (Central-West) to City 5 (Southeast)

- REQUERIMENTO 5: 
- 
- The clustering coefficient is a measure used in graphs to quantify the degree of local clustering of a node or the network as a whole. It measures the tendency of a node's neighbors to be interconnected, forming groups or clusters.
The clustering coefficient of a node is calculated as the ratio between the number of existing edges between the neighbors of this node and the maximum number of possible edges between these neighbors. This measure is normalized to a value between 0 and 1.





