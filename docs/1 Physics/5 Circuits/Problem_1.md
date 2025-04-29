# Problem 1

**Equivalent Resistance Using Graph Theory**

## 1. Graph-Based Modeling

An electrical circuit can be modeled as an **undirected weighted graph**:

- **Nodes** ($V$): represent junctions.
- **Edges** ($E$): represent resistors, with weights corresponding to resistance values in ohms ($\Omega$).

Thus, a graph is defined as:

$$
G = (V, E)
$$

Each edge $e \in E$ has an associated weight function:

$$
w: E \rightarrow \mathbb{R}^{+}
$$

where $w(e)$ is the resistance value.

> **Note**: Use a `Graph` if each resistor connects different pairs of nodes. Use a `MultiGraph` if multiple resistors exist between the same two nodes.

---

## 2. Mathematical Rules for Simplification

### 2.1 Series Connection

When two resistors are connected end-to-end (node degree $=2$), their resistances add directly:

$$
R_{\text{eq}} = R_1 + R_2 + \cdots + R_n
$$

Simplification steps:
- Identify a node with exactly two neighbors.
- Replace the two connecting resistors with one of equivalent resistance.

---

### 2.2 Parallel Connection

When multiple resistors connect the same pair of nodes, the equivalent resistance satisfies:

$$
\frac{1}{R_{\text{eq}}} = \frac{1}{R_1} + \frac{1}{R_2} + \cdots + \frac{1}{R_n}
$$

Or equivalently:

$$
R_{\text{eq}} = \left( \sum_{i=1}^n \frac{1}{R_i} \right)^{-1}
$$

Simplification steps:
- Identify multiple edges between two nodes.
- Collapse them into a single edge using the above formula.

---

## 3. Algorithm Description

Given a graph $G = (V, E)$ and two distinguished nodes $A$ and $B$:

### Input
- Graph $G$ where each edge has weight $w(e)$.
- Source node $A$, target node $B$.

### Output
- Equivalent resistance $R_{\text{eq}}$ between $A$ and $B$.

### Steps

1. **While changes are possible**:
   - **Series Reduction**:
     - Find nodes (except $A$ and $B$) with degree 2.
     - Combine adjacent resistors by summing resistances.
   - **Parallel Reduction**:
     - Find multiple edges between the same two nodes.
     - Combine using parallel formula.

2. **After each operation**:
   - Check if $A$ and $B$ remain connected.
   - If disconnected: $R_{\text{eq}} = \infty$.

3. **Stopping condition**:
   - If only one edge exists between $A$ and $B$, return its weight.

---

## 4. Pseudocode

```python
def detect_and_simplify_series(G, source, target):
    for node in list(G.nodes()):
        if node in (source, target):
            continue
        if G.degree(node) == 2:
            neighbors = list(G.neighbors(node))
            u, w = neighbors
            R1 = G[node][u]['weight']
            R2 = G[node][w]['weight']
            G.remove_node(node)
            G.add_edge(u, w, weight=R1 + R2)
            return True
    return False

def detect_and_simplify_parallel(G):
    edge_dict = {}
    for u, v, data in G.edges(data=True):
        key = tuple(sorted((u, v)))
        edge_dict.setdefault(key, []).append(data['weight'])

    for (u, v), resistances in edge_dict.items():
        if len(resistances) > 1:
            R_eq = 1 / sum(1/r for r in resistances)
            G.remove_edges_from([(u, v)] * len(resistances))
            G.add_edge(u, v, weight=R_eq)
            return True
    return False

def simplify_graph(G, source, target):
    while True:
        changed = detect_and_simplify_series(G, source, target)
        changed |= detect_and_simplify_parallel(G)
        if not changed:
            break
        if not nx.has_path(G, source, target):
            return float('inf')
    return G[source][target]['weight']
```

---

## 5. Important Observations

- **Series and parallel reductions are associative**:
  
  For series:
  $$
  (R_1 + R_2) + R_3 = R_1 + (R_2 + R_3)
  $$

  For parallel:
  $$
  \left( \frac{1}{R_1} + \frac{1}{R_2} \right)^{-1} \parallel R_3 = \left( \frac{1}{\left( \frac{1}{R_1} + \frac{1}{R_2} \right) + \frac{1}{R_3}} \right)
  $$

- **Algorithm always terminates** because each operation reduces the number of nodes or edges.

- **Edge Cases**:
  - Mesh networks (complex loops) require advanced methods (Kirchhoff’s laws, Star-Delta transformations).
  - Disconnection means $R_{\text{eq}} = \infty$.

---

## 6. Example

### Series Example
Three resistors in series:

```python
G = nx.Graph()
G.add_edge('A', 'B', weight=5)
G.add_edge('B', 'C', weight=10)
```

After simplifying:

$$
R_{\text{AC}} = 5 + 10 = 15\ \Omega
$$

### Parallel Example
Two resistors in parallel:

```python
G = nx.MultiGraph()
G.add_edge('A', 'B', weight=8)
G.add_edge('A', 'B', weight=12)
```

After simplifying:

$$
R_{\text{eq}} = \left( \frac{1}{8} + \frac{1}{12} \right)^{-1} = 4.8\ \Omega
$$

---

## **7. Visualizations**

In this section, we provide graphical visualizations of circuits before and after applying series and parallel simplifications.

Each plot clearly shows how the graph structure evolves during reductions.

---

### 7.1 Series Simplification

#### (a) Original Series Circuit

```python
import networkx as nx
import matplotlib.pyplot as plt

G = nx.Graph()
G.add_edge('A', 'B', weight=5)
G.add_edge('B', 'C', weight=10)

pos = nx.spring_layout(G, seed=42)
edge_labels = nx.get_edge_attributes(G, 'weight')

plt.figure(figsize=(6, 4))
nx.draw(G, pos, with_labels=True, node_color='lightblue', node_size=700)
nx.draw_networkx_edge_labels(G, pos, edge_labels={k: f"{v}Ω" for k, v in edge_labels.items()})
plt.title("Original Series Circuit: A → B → C")
plt.show()
```
![Original Series](../../_pics/Physics/5%20Circuits/Problem_1/original_series.png)

---

#### (b) After Series Simplification

```python
import networkx as nx
import matplotlib.pyplot as plt
G_simplified = nx.Graph()
G_simplified.add_edge('A', 'C', weight=15)  # 5Ω + 10Ω

pos = nx.spring_layout(G_simplified, seed=42)
edge_labels = nx.get_edge_attributes(G_simplified, 'weight')

plt.figure(figsize=(6, 4))
nx.draw(G_simplified, pos, with_labels=True, node_color='lightgreen', node_size=700)
nx.draw_networkx_edge_labels(G_simplified, pos, edge_labels={k: f"{v}Ω" for k, v in edge_labels.items()})
plt.title("After Series Simplification: A → C (15Ω)")
plt.show()
```
![Simplification Series](../../_pics/Physics/5%20Circuits/Problem_1/simplification_series.png)

---

### 7.2 Parallel Simplification

#### (a) Original Parallel Circuit

```python
import networkx as nx
import matplotlib.pyplot as plt
G_parallel = nx.MultiGraph()
G_parallel.add_edge('A', 'B', weight=8)
G_parallel.add_edge('A', 'B', weight=12)

pos = nx.spring_layout(G_parallel, seed=42)
edge_labels = {(u, v, k): d['weight'] for u, v, k, d in G_parallel.edges(keys=True, data=True)}

plt.figure(figsize=(6, 4))
nx.draw(G_parallel, pos, with_labels=True, node_color='lightcoral', node_size=700)
nx.draw_networkx_edge_labels(
    G_parallel, pos,
    edge_labels={(u, v): f"{w}Ω" for (u, v, k), w in edge_labels.items()}
)
plt.title("Original Parallel Circuit: Two Resistors A ↔ B")
plt.show()
```
![Original Parallel](../../_pics/Physics/5%20Circuits/Problem_1/original_parallel.png)

---

#### (b) After Parallel Simplification

```python
import networkx as nx
import matplotlib.pyplot as plt
G_parallel_simple = nx.Graph()
G_parallel_simple.add_edge('A', 'B', weight=4.8)  # Simplified 8Ω || 12Ω

pos = nx.spring_layout(G_parallel_simple, seed=42)
edge_labels = nx.get_edge_attributes(G_parallel_simple, 'weight')

plt.figure(figsize=(6, 4))
nx.draw(G_parallel_simple, pos, with_labels=True, node_color='lightyellow', node_size=700)
nx.draw_networkx_edge_labels(G_parallel_simple, pos, edge_labels={k: f"{v:.1f}Ω" for k, v in edge_labels.items()})
plt.title("After Parallel Simplification: A ↔ B (4.8Ω)")
plt.show()
```
![Simplification Parallel](../../_pics/Physics/5%20Circuits/Problem_1/simplification_parallel.png)

### Colab: Circuits Problem 1
[Souce Code](https://colab.research.google.com/drive/1BwGVhREaPlcOuarPoGW_Ov7ZTVtykMyb?usp=sharing)