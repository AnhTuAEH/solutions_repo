# Problem 1

---

## 1. Problem Overview

### 1.1 Introduction

Compute the **equivalent resistance** $R\_{\text{eq}}$ between two nodes in a resistor network, modeled as a weighted undirected graph $G = (V, E)$ where edges represent resistors. Use Ohm’s Law: $R\_{\text{eq}} = \frac{V}{I}$.

### 1.2 Equivalent Resistance Basics

* **Ohm’s Law**: $V = I \cdot R$
* **Series**: $R\_{\text{eq}} = R\_1 + R\_2 + \cdots + R\_n$
* **Parallel**: $\frac{1}{R\_{\text{eq}}} = \sum \frac{1}{R\_i}$

### 1.3 Formal Statement

Given graph $G$, START node $A$, and END node $B$, find $R\_{\text{eq}}(A, B)$.

### 1.4 Applications

Useful in power systems, electronics, and network analysis; demonstrates links between circuit theory and graph theory.

---

## 2. Graph Representation

Model circuit as an undirected, weighted graph with:

* Nodes = junctions
* Edges = resistors, with weights $R\_{uv}$

Support formats include adjacency and resistance matrices. Graphs help in detecting simplifications like series and parallel connections.

---

## 3. Input Structure

Input defines:

* Nodes list
* Edge list as tuples: $(u, v, R\_{uv})$
* Start and end nodes

Edge representations and formats enable algorithmic simplification.

---

## 4. Series and Parallel Detection

Key for simplification:

* **Series**: Two edges in line through a node with degree 2 (not start/end)
* **Parallel**: Multiple edges between same nodes

Apply recursively until no more simplifications.

---

## 5. Resistance Computation

Use Ohm’s Law: $R = \frac{V}{I}$.

* **Node Voltage Method**: Solve linear system using KCL.
* **Laplacian Method**: Use matrix pseudoinverse to find resistance.

---

## 6. Complex Network Reduction

For complex circuits:

* Apply **recursive reduction**, **node elimination**, or **Y-Δ transforms**
* Use **matrix methods** for numerical and symbolic solutions

---

## 7. Resistance Computation (Final Step)

Once simplified, compute $R\_{\text{eq}}$:

* **Simple case**: Apply direct formulas
* **General case**: Use node voltage or Laplacian methods

---

## 8. Plot and Visualization

### Circuit simplification

#### Case 1

```python
import networkx as nx
import matplotlib.pyplot as plt
import os
from PIL import Image
from IPython.display import HTML
import base64

# Step directory
folder_name = "case_1"
os.makedirs(folder_name, exist_ok=True)

# Base position layout (same throughout)
base_pos = {
    "B+": (0, 1),
    "R2": (1, 1.5),
    "R3": (2, 1.5),
    "R4": (3, 1),
    "R5": (4, 1),
    "B-": (5, 1),
    "R1": (1.5, 0.3)
}

# Function to draw and save a step
def draw_step(G, pos, title, highlight=[], merged_labels={}, filename="step.png"):
    plt.figure(figsize=(7, 3))
    
    # Colors for nodes
    colors = []
    for node in G.nodes():
        if node in highlight:
            colors.append("red" if "1" in node or "2" in node or "3" in node or "23" in node else
                          "green" if "4" in node or "5" in node or "45" in node else
                          "cyan" if "123" in node else
                          "magenta")
        else:
            colors.append("lightgray")
    
    # Labels
    labels = {n: merged_labels.get(n, n) for n in G.nodes()}
    
    nx.draw_networkx_nodes(G, pos, node_color=colors, node_size=1200, node_shape='s', edgecolors='black')
    nx.draw_networkx_labels(G, pos, labels=labels, font_size=10, font_weight="bold")
    nx.draw_networkx_edges(G, pos, edge_color="gray", arrows=True, arrowsize=15, width=2)
    
    plt.title(title, fontsize=14, loc='left')
    plt.axis("off")
    plt.tight_layout()
    plt.savefig(f"{folder_name}/{filename}", dpi=100)
    plt.close()

# Step 0
# Step 1: Initial circuit
G1 = nx.DiGraph()
G1.add_edges_from([
    ("B+", "R2"), ("R2", "R3"), ("R3", "R4"),
    ("R4", "R5"), ("R5", "B-"),
    ("B+", "R1"), ("R1", "R4")
])
draw_step(G1, base_pos, "Initial circuit", highlight=[], filename="step_0.png")


# Step 1: Initial circuit
G1 = nx.DiGraph()
G1.add_edges_from([
    ("B+", "R2"), ("R2", "R3"), ("R3", "R4"),
    ("R4", "R5"), ("R5", "B-"),
    ("B+", "R1"), ("R1", "R4")
])
draw_step(G1, base_pos, "First step", highlight=["R2", "R3"], filename="step_1.1.png")

# Step 1: After combining R2 and R3 → R23
G2 = nx.DiGraph()
G2.add_edges_from([
    ("B+", "R23"), ("R23", "R4"),
    ("R4", "R5"), ("R5", "B-"),
    ("B+", "R1"), ("R1", "R4")
])
pos2 = base_pos.copy()
pos2["R23"] = ((base_pos["R2"][0] + base_pos["R3"][0]) / 2, base_pos["R2"][1])
draw_step(G2, pos2, "First step", highlight=["R23"], merged_labels={"R23": "R23"}, filename="step_1.2.png")

# Step 2: Highlight R4 and R5
draw_step(G2, pos2, "Second step", highlight=["R4", "R5"], filename="step_2.1.png")

# Step 2: Combine R4 + R5 → R45
G3 = nx.DiGraph()
G3.add_edges_from([
    ("B+", "R23"), ("R23", "R45"),
    ("R45", "B-"),
    ("B+", "R1"), ("R1", "R45")
])
pos3 = pos2.copy()
pos3["R45"] = ((base_pos["R4"][0] + base_pos["R5"][0]) / 2, base_pos["R4"][1])
draw_step(G3, pos3, "Second step", highlight=["R45"], merged_labels={"R45": "R45"}, filename="step_2.2.png")

# Step 3: Highlight R1 and R23
draw_step(G3, pos3, "Third step", highlight=["R1", "R23"], filename="step_3.1.png")

# Step 3: Combine R1 ‖ R23 → R123
G4 = nx.DiGraph()
G4.add_edges_from([
    ("B+", "R123"), ("R123", "R45"), ("R45", "B-")
])
pos4 = pos3.copy()
pos4["R123"] = ((base_pos["R1"][0] + pos2["R23"][0]) / 2, 1.1)
draw_step(G4, pos4, "Third step", highlight=["R123"], merged_labels={"R123": "R123"}, filename="step_3.2.png")

# Step 4: Highlight R123 and R45
draw_step(G4, pos4, "Fourth step", highlight=["R123", "R45"], filename="step_4.1.png")

# Step 4: Combine R123 + R45 → R12345
G5 = nx.DiGraph()
G5.add_edges_from([
    ("B+", "R12345"), ("R12345", "B-")
])
pos5 = {"B+": (0, 1), "R12345": (2.5, 1), "B-": (5, 1)}
draw_step(G5, pos5, "Fourth step", highlight=["R12345"], merged_labels={"R12345": "R12345"}, filename="step_4.2.png")

# === Generate GIF from step images ===

image_files = sorted([f for f in os.listdir("case_1") if f.endswith(".png")])
print(image_files)
frames = [Image.open(os.path.join(folder_name, fname)) for fname in image_files]
gif_path = "case1_visual_simplification.gif"
frames[0].save(gif_path, save_all=True, append_images=frames[1:], duration=1200, loop=0)

# Display GIF in Colab using HTML
with open(gif_path, 'rb') as f:
    gif_data = f.read()
b64_gif = base64.b64encode(gif_data).decode('utf-8')
html = f'<img src="data:image/gif;base64,{b64_gif}">'
HTML(html)
```

![Circuit Simplification](../../_pics/Physics/5%20Circuits/Problem_1/circuit_simplification/circuit_simplification.gif)

#### Case 2

```python
import networkx as nx
import matplotlib.pyplot as plt

# -----------------------------
# Function to draw nodes with different shapes
# -----------------------------
def custom_draw(G, pos, title):
    plt.figure(figsize=(12, 4))

    circle_nodes = [n for n in G.nodes if n.startswith("O")]
    rounded_square_nodes = ["B+", "B-"]
    square_nodes = [n for n in G.nodes if n.startswith("R")]

    # Vẽ các cạnh với mũi tên
    nx.draw_networkx_edges(
        G, pos,
        arrows=True,
        arrowstyle='->',
        arrowsize=20,
        connectionstyle='arc3,rad=0.0',
        min_target_margin=15,
        width=2
    )

    # Vẽ các node hình tròn (O)
    nx.draw_networkx_nodes(G, pos,
                           nodelist=circle_nodes,
                           node_shape='o',
                           node_color='lightgrey',
                           node_size=1000)

    # Node B+ B- giả lập bo góc bằng màu trắng + viền đậm
    nx.draw_networkx_nodes(G, pos,
                           nodelist=rounded_square_nodes,
                           node_shape='s',
                           node_color='white',
                           edgecolors='black',
                           linewidths=2,
                           node_size=1000)

    # Node điện trở vuông
    nx.draw_networkx_nodes(G, pos,
                           nodelist=square_nodes,
                           node_shape='s',
                           node_color='lightgrey',
                           edgecolors='black',
                           linewidths=1,
                           node_size=1000)

    # Vẽ nhãn
    nx.draw_networkx_labels(G, pos)

    plt.title(title)
    plt.axis('off')
    plt.show()

# -----------------------------
# Picture 1: Resistors as Nodes (Initial)
# -----------------------------
G1 = nx.DiGraph()
G1.add_edges_from([
    ("B+", "R1"),
    ("R1", "R2"),
    ("R1", "R3"),
    ("R2", "O1"),
    ("R3", "O1"),
    ("O1", "R4"),
    ("O1", "R5"),
    ("R4", "B-"),
    ("R5", "B-"),
])

pos1 = {
    "B+": (-2, 0),
    "R1": (-1, 0),
    "R2": (0, 1),
    "R3": (0, -1),
    "O1": (1, 0),
    "R4": (2, 1),
    "R5": (2, -1),
    "B-": (3, 0),
}
custom_draw(G1, pos1, "Resistors as Nodes (Initial)")

# -----------------------------
# Picture 2: Consistent Node Representation
# -----------------------------
G2 = nx.DiGraph()
G2.add_edges_from([
    ("B+", "O0"),
    ("O0", "R1"),
    ("R1", "O1"),
    ("O1", "R2"),
    ("O1", "R3"),
    ("R2", "O2"),
    ("R3", "O2"),
    ("O2", "R4"),
    ("O2", "R5"),
    ("R4", "O3"),
    ("R5", "O3"),
    ("O3", "B-"),
])

pos2 = {
    "B+": (-3, 0),
    "O0": (-2, 0),
    "R1": (-1, 0),
    "O1": (0, 0),
    "R2": (1, 1),
    "R3": (1, -1),
    "O2": (2, 0),
    "R4": (3, 1),
    "R5": (3, -1),
    "O3": (4, 0),
    "B-": (5, 0),
}
custom_draw(G2, pos2, "With Junction Nodes")

# -----------------------------
# Picture 3: Edge-Based Resistor Graph
# -----------------------------
G3 = nx.DiGraph()
G3.add_edges_from([
    ("B+", "O0", {"label": ""}),
    ("O0", "O1", {"label": "R1"}),
    ("O0", "O1", {"label": "R2"}),
    ("O1", "O2", {"label": "R3"}),
    ("O1", "O2", {"label": "R4"}),
    ("O2", "O3", {"label": "R5"}),
    ("O3", "B-", {"label": ""}),
])

# Vị trí node
pos3 = {
    "B+": (-3, 0),
    "O0": (-2, 0),
    "O1": (-1, 0),
    "O2": (0, 0),
    "O3": (1, 0),
    "B-": (2, 0),
}

plt.figure(figsize=(12, 4))

# Vẽ B+ → O0
nx.draw_networkx_edges(G3, pos3,
    edgelist=[("B+", "O0")],
    connectionstyle='arc3,rad=0.0',
    arrowstyle='->', arrowsize=20, width=2
)

# Vẽ R1
nx.draw_networkx_edges(G3, pos3,
    edgelist=[("O0", "O1")],
    connectionstyle='arc3,rad=0.0',
    arrowstyle='->', arrowsize=20, width=2
)

# Vẽ R2: cong lên
nx.draw_networkx_edges(G3, pos3,
    edgelist=[("O1", "O2")],
    connectionstyle='arc3,rad=0.3',
    arrowstyle='->', arrowsize=20, width=2
)

# Vẽ R3: cong xuống
nx.draw_networkx_edges(G3, pos3,
    edgelist=[("O1", "O2")],
    connectionstyle='arc3,rad=-0.3',
    arrowstyle='->', arrowsize=20, width=2
)

# Vẽ R4 và R5: hơi cong lên & xuống
nx.draw_networkx_edges(G3, pos3,
    edgelist=[("O2", "O3")],
    connectionstyle='arc3,rad=0.3',
    arrowstyle='->', arrowsize=20, width=2
)
nx.draw_networkx_edges(G3, pos3,
    edgelist=[("O2", "O3")],
    connectionstyle='arc3,rad=-0.3',
    arrowstyle='->', arrowsize=20, width=2
)

# Vẽ O3 → B-
nx.draw_networkx_edges(G3, pos3,
    edgelist=[("O3", "B-")],
    connectionstyle='arc3,rad=0.0',
    arrowstyle='->', arrowsize=20, width=2
)

# Vẽ node
circle_nodes = [n for n in G3.nodes if n.startswith("O")]
rounded_square_nodes = ["B+", "B-"]

nx.draw_networkx_nodes(G3, pos3, nodelist=circle_nodes,
    node_shape='o', node_color='lightgrey', node_size=1000)

nx.draw_networkx_nodes(G3, pos3, nodelist=rounded_square_nodes,
    node_shape='s', node_color='white', edgecolors='black',
    linewidths=2, node_size=1000)

# Nhãn node
nx.draw_networkx_labels(G3, pos3)

# Nhãn cạnh
edge_labels = {
    ("O0", "O1"): "R1",
    ("O1", "O2"): "R2 / R3",
    ("O2", "O3"): "R4 / R5",
}
nx.draw_networkx_edge_labels(G3, pos3, edge_labels=edge_labels)

plt.title("Resistors as Edges")
plt.axis('off')
plt.show()
```

**Initial**
![Initial](../../_pics/Physics/5%20Circuits/Problem_1/circuit_simplification/initial.png)

**Consistent Node Representation**
![Consistent Node Representation](../../_pics/Physics/5%20Circuits/Problem_1/circuit_simplification/consistent-node-representation.png)

**Edge-Based Resistor Graph**
![Edge-Based Resistor Graph](../../_pics/Physics/5%20Circuits/Problem_1/circuit_simplification/edge-based-resistor-graph.png)

### Building blocks

#### Series configuration
```python
import networkx as nx
import matplotlib.pyplot as plt

def draw_circuit(G, pos, title):
    plt.figure(figsize=(10, 5))

    # Classify nodes
    circle_nodes = [n for n in G.nodes if n.startswith('o')]
    square_nodes = [n for n in G.nodes if n.startswith('I') or n.startswith('D') or n.startswith('R')]

    # Draw edges
    nx.draw_networkx_edges(G, pos, arrows=True)

    # Draw nodes with different shapes
    nx.draw_networkx_nodes(
        G, pos, nodelist=circle_nodes,
        node_color=[G.nodes[n].get('color', 'lightgrey') for n in circle_nodes],
        node_size=2000, node_shape='o'
    )
    nx.draw_networkx_nodes(
        G, pos, nodelist=square_nodes,
        node_color=[G.nodes[n].get('color', 'lightgrey') for n in square_nodes],
        node_size=2000, node_shape='s'
    )

    # Draw labels
    nx.draw_networkx_labels(G, pos, font_size=10)

    plt.title(title)
    plt.axis('off')
    plt.show()


# First graph: Original circuit
G1 = nx.DiGraph()
inputs = [f"I{i}" for i in range(1, 4)]
outputs = [f"D{i}" for i in range(1, 5)]

# Add nodes and edges
G1.add_node("o1", color='lightgreen')
G1.add_node("o2", color='red')
G1.add_node("o3", color='lightgreen')
G1.add_node("R1")
G1.add_node("R2")

for i in inputs:
    G1.add_edge(i, "o1")

G1.add_edge("o1", "R1")
G1.add_edge("R1", "o2")
G1.add_edge("o2", "R2")
G1.add_edge("R2", "o3")

for d in outputs:
    G1.add_edge("o3", d)

# Positioning manually
pos1 = {
    "I1": (-2, 1), "I2": (-2, 0), "I3": (-2, -1),
    "o1": (-1, 0), "R1": (0, 0), "o2": (1, 0), "R2": (2, 0), "o3": (3, 0),
    "D1": (4, 1), "D2": (4, 0.5), "D3": (4, -0.5), "D4": (4, -1)
}

draw_circuit(G1, pos1, "Original Circuit")

# Second graph: Simplified circuit
G2 = nx.DiGraph()
G2.add_node("o1", color='lightgreen')
G2.add_node("o3", color='lightgreen')
G2.add_node("R12")

for i in inputs:
    G2.add_edge(i, "o1")

G2.add_edge("o1", "R12")
G2.add_edge("R12", "o3")

for i in range(1, 6):  # Assume m=5 for illustration
    G2.add_edge("o3", f"D{i}")

# Positioning manually
pos2 = {
    "I1": (-2, 1), "I2": (-2, 0), "I3": (-2, -1),
    "o1": (-1, 0), "R12": (0, 0), "o3": (1, 0),
    "D1": (2, 1), "D2": (2, 0.5), "D3": (2, 0), "D4": (2, -0.5), "D5": (2, -1)
}

draw_circuit(G2, pos2, "Simplified Circuit")
```

![Series Original](../../_pics/Physics/5%20Circuits/Problem_1/building_blocks/series_original.png)

Can be replaced by
![Series Simplified](../../_pics/Physics/5%20Circuits/Problem_1/building_blocks/series_simplified.png)

---

#### Parallel configuration

![Parallel Original](../../_pics/Physics/5%20Circuits/Problem_1/building_blocks/parallel_original.png)

Can be replaced by
![Parallel Simplified](../../_pics/Physics/5%20Circuits/Problem_1/building_blocks/parallel_simplified.png)

### Colab: Circuit Problem 1
[Souce Code](https://colab.research.google.com/drive/1ZesDtPsi-T2gTUKiNK-pqcJ_RN1R3pau?usp=sharing)
