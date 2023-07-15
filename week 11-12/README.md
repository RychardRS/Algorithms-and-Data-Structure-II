UNIVERSIDADE FEDERAL DO RIO GRANDE DO NORTE (UFRN)

DISCIPLINA: ALGORITMOS E ESTRUTURAS DE DADOS II

Grupo: 
- Rychardson Ribeiro de Souza
- Thiago Jordão Melo da Costa

- Link do vídeo no Loom da semana 11-12: https://www.loom.com/share/e2310a7e8cb343c7b98af6185cbd6bc8

## Inicialmente começamos instalando importando as bibliotecas ##


!pip install nxviz==0.6.3
!pip install networkx==2.6.2
!pip install wikipedia
!pip install matplotlib==3.1.3
import networkx as nx
import matplotlib.pyplot as plt
import matplotlib.patches as mpatches
import numpy as np
import seaborn as sns
import pandas as pd
from operator import itemgetter
import networkx as nx
import wikipedia
import matplotlib.pyplot as plt

## Início da Coleta de Dados ##

SEED = "Extremoz".title()
STOPS = ("Isni (Identifier)",
         "International Standard Name Identifier",
         "Viaf (Identifier)",
         "Isbn (Identifier)",
         )
     

todo_lst = [(0, SEED)] # The SEED is in the layer 0
todo_set = set(SEED) # The SEED itself
done_set = set() # Nothing is done yet
     

g = nx.DiGraph()
layer, page = todo_lst[0]

## Limitando o nível de profundidade da rede ##
- Removendo duplicatas
  
%%time
while layer < 2:
  del todo_lst[0]
  done_set.add(page)

  # Show progress
  print(layer, page)

  # Attempt to download the selected page.
  try:
    wiki = wikipedia.page(page)
  except:
    print("Could not load", page)
    layer, page = todo_lst[0]
    continue

  for link in wiki.links:
    link = link.title()
    if link not in STOPS and not link.startswith("List Of"):
      if link not in todo_set and link not in done_set:
        todo_lst.append((layer + 1, link))
        todo_set.add(link)
      g.add_edge(page, link)
  layer, page = todo_lst[0]


  ## Início da etapa de tratamento dos dados ##

  # remove self loops
g.remove_edges_from(nx.selfloop_edges(g))

# identify duplicates like that: 'network' and 'networks'
duplicates = [(node, node + "s")
              for node in g if node + "s" in g
             ]

for dup in duplicates:
  # *dup is a technique named 'unpacking'
  g = nx.contracted_nodes(g, *dup, self_loops=False)

print(duplicates)

duplicates = [(x, y) for x, y in
              [(node, node.replace("-", " ")) for node in g]
                if x != y and y in g]
print(duplicates)

for dup in duplicates:
  g = nx.contracted_nodes(g, *dup, self_loops=False)

# nx.contracted creates a new node/edge attribute called contraction
# the value of the attribute is a dictionary, but GraphML
# does not support dictionary attributes
nx.set_node_attributes(g, 0,"contraction")
nx.set_edge_attributes(g, 0,"contraction")

## Filtrando nós ##
# filtragem nós para grau >=6
core = [node for node, deg in dict(g.degree()).items() if deg >= 6]

# select a subgraph with 'core' nodes
gsub = nx.subgraph(g, core)

print("{} nodes, {} edges".format(len(gsub), nx.number_of_edges(gsub)))

nx.write_graphml(gsub, "cna.graphml")

## Definindo quantidade de conexões de cada nó ##

for i, j in gsub.nodes(data=True):
  gsub.nodes[i]["class"] = gsub.degree(i)
     

#quantidade de conexões de cada nó por cor
import nxviz
from nxviz.plots import CircosPlot
c = CircosPlot(
    gsub,
    node_grouping="class",
    node_color="class",
    node_order="class",
    node_labels=True,
    group_label_position="middle",
    group_label_color=True,
    group_label_offset=1,
)
c.draw()
plt.show()



     


