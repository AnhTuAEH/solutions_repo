# Problem 1

---

## 1. Problem Overview

### 1.1 Introduction

The objective is to compute the **equivalent resistance** $R_{\text{eq}}$ between two designated points in an electrical network: a **START node** and an **END node**. This is a foundational problem in circuit theory, as it enables the prediction of current flow, voltage drops, and power dissipation.

We model the resistor network as a **weighted undirected graph** $G = (V, E)$, where:
- $V$ is the set of nodes (electrical junctions),
- $E$ is the set of edges (resistors),
- Each edge $e = (u, v) \in E$ has an associated resistance $R_{uv} > 0$.

The central task is to determine $R_{\text{eq}}(A, B)$, the effective resistance between a **START node** $A \in V$ and an **END node** $B \in V$. If a voltage source $V$ were connected across $A$ and $B$, the current $I$ flowing through the network would satisfy Ohm’s Law:

$$
R_{\text{eq}} = \frac{V}{I}
$$

---

### 1.2 Equivalent Resistance: Conceptual Basis

#### 1.2.1 Ohm’s Law

For any two-terminal resistive element:

$$
V = I \cdot R
$$

where:
- $V$ is the potential difference (volts),
- $I$ is the current (amperes),
- $R$ is the resistance (ohms, $\Omega$).

---

#### 1.2.2 Series Configuration

For resistors in series:

$$
R_{\text{eq}} = R_1 + R_2 + \cdots + R_n
$$

This applies when the same current flows through each resistor without branching paths.

---

#### 1.2.3 Parallel Configuration

For resistors in parallel:

$$
\frac{1}{R_{\text{eq}}} = \frac{1}{R_1} + \frac{1}{R_2} + \cdots + \frac{1}{R_n}
$$

This configuration implies the voltage across each resistor is the same, while the current divides among the paths.

---

### 1.3 Formal Problem Statement

**Given:**
- A graph $G = (V, E)$ with $R_e > 0$ for all $e \in E$,
- A specified START node $A \in V$,
- A specified END node $B \in V$,

**Find:** the equivalent resistance $R_{\text{eq}}(A, B)$ between nodes $A$ and $B$, as if the network were replaced by a single equivalent resistor.

---

### 1.4 Applications and Implications

Accurate computation of $R_{\text{eq}}$ has applications in:
- Power grid analysis,
- Signal integrity assessment in microelectronics,
- Fault tolerance in communication networks,
- Optimization of low-power and efficient designs.

Additionally, this problem demonstrates the synergy between **electrical engineering** and **graph theory**, showcasing the power of algorithmic thinking in physical systems.

---

## 2. Graph Representation

### 2.1 Motivation

To analyze electrical circuits algorithmically, we need a mathematical abstraction that captures the topology and resistance values of the network. Graph theory provides a natural framework for modeling circuits, where **nodes** correspond to electrical junctions and **edges** represent resistive elements.

This abstraction enables the application of graph algorithms to simplify and solve complex networks, particularly when identifying series and parallel connections, or computing resistance between arbitrary nodes.

---

### 2.2 Graph Model

We model a resistor network as an **undirected, weighted graph**:

$$
G = (V, E, R)
$$

where:
- $V$ is a set of **nodes** (or **vertices**) representing circuit junctions,
- $E \subseteq \{ \{u, v\} \mid u, v \in V, u \neq v \}$ is a set of **edges** representing resistors,
- $R: E \rightarrow \mathbb{R}^+$ is a function assigning a **resistance** value $R_{uv}$ to each edge $e = \{u, v\}$.

Each resistor is treated as a symmetric component: the resistance between $u$ and $v$ is the same regardless of current direction.

---

### 2.3 Edge Representation

Each edge (resistor) can be described as a tuple:

$$
(u, v, R_{uv})
$$

where:
- $u, v \in V$ are the connected nodes,
- $R_{uv} \in \mathbb{R}^+$ is the resistance in ohms $(\Omega)$.

For example, a resistor of $5\,\Omega$ between node 1 and node 3 is represented as:

$$
(1, 3, 5)
$$

Multiple resistors between the same pair of nodes are treated as **parallel resistors** and must be aggregated accordingly:

$$
\frac{1}{R_{\text{eq}}} = \sum_{i=1}^{n} \frac{1}{R_i}
$$

---

### 2.4 Adjacency and Resistance Matrix Representations

The graph can be represented in matrix form to facilitate algorithmic manipulation:

- **Adjacency Matrix** $A$: A symmetric $|V| \times |V|$ matrix with entries:

  $$
  A_{uv} =
  \begin{cases}
    1 & \text{if } \{u, v\} \in E \\
    0 & \text{otherwise}
  \end{cases}
  $$

- **Resistance Matrix** $R$: A weighted matrix storing resistance values:

  $$
  R_{uv} =
  \begin{cases}
    R_{uv} & \text{if } \{u, v\} \in E \\
    \infty & \text{otherwise}
  \end{cases}
  $$

These representations are useful for implementing resistance-reduction algorithms and simulations.

---

### 2.5 Visualization Example

Consider a simple triangular network with nodes $A$, $B$, and $C$, and resistors between each pair:

- $(A, B, 2\,\Omega)$
- $(B, C, 3\,\Omega)$
- $(A, C, 4\,\Omega)$

This network can be visualized as a triangle graph, and the total resistance between any two nodes can be computed using the parallel and series reduction rules based on the graph structure.

---

### 2.6 Benefits of Graph-Based Representation

- Enables recursive simplification.
- Facilitates cycle detection and transformation (e.g., Δ-Y transforms).
- Prepares the circuit for numerical or symbolic computation.
- Unifies the treatment of arbitrary and complex topologies.

---

## 3. Input Structure

### 3.1 Purpose

To perform automated or algorithmic analysis of circuits, we must establish a precise and unambiguous format for inputting the resistor network. This input captures both the **topology** of the network (i.e., how nodes are connected) and the **numerical values** of resistances.

---

### 3.2 Input Components

The input consists of three essential components:

1. **Node Set**: A list of all nodes in the circuit.
2. **Edge List**: Each edge is a resistor defined by a pair of nodes and a resistance value.
3. **Start and End Nodes**: Two nodes $A$ and $B$ between which the equivalent resistance is to be computed.

---

### 3.3 Edge Format

Each resistor is represented as a tuple:

$$
(u, v, R_{uv}) \in V \times V \times \mathbb{R}^+
$$

where:
- $u$ and $v$ are node identifiers,
- $R_{uv}$ is the resistance in ohms $(\Omega)$ between $u$ and $v$.

For example, the following list of edges defines a small network:

```text
(1, 2, 10)
(2, 3, 5)
(1, 3, 20)
```

This specifies resistors of $10\Omega$, $5\Omega$, and $20\Omega$ respectively between the indicated node pairs.

---

### 3.4 Input as Data Structure

In programming terms, the input could be stored as a list of dictionaries or tuples. Example in Python-like pseudocode:

```python
edges = [
    (1, 2, 10),
    (2, 3, 5),
    (1, 3, 20)
]
start_node = 1
end_node = 3
```

---

### 3.5 Graph Construction

From the edge list, we construct a graph $G = (V, E)$:

* The set of vertices $V$ is the union of all nodes that appear in any edge.
* The set of edges $E$ is directly derived from the input tuples.
* A mapping function $R: E \rightarrow \mathbb{R}^+$ is defined such that:

$$
R(\{u, v\}) = R_{uv}
$$

If multiple resistors exist between the same node pair (i.e., parallel resistors), their combined resistance is computed before storing:

$$
\frac{1}{R_{\text{eq}}(u, v)} = \sum_{i=1}^{n} \frac{1}{R_i}
$$

---

### 3.6 Special Cases

* **Duplicate edges**: Combine them using the parallel resistance formula.
* **Self-loops**: Resistors connecting a node to itself are typically ignored unless explicitly meaningful.
* **Isolated nodes**: Nodes not connected to either the start or end can be pruned.

---

### 3.7 Summary

The input format should:

* Be compact and readable.
* Allow for easy graph construction.
* Support preprocessing for simplification (e.g., merging parallels).
* Clearly specify the two terminal nodes of interest: START ($A$) and END ($B$).

---

## 4. Series and Parallel Detection

### 4.1 Motivation

To simplify a resistor network, we must identify **series** and **parallel** substructures within the graph. These structures allow the replacement of multiple resistors with a single equivalent resistor, thereby reducing circuit complexity and enabling easier computation of $R_{\text{eq}}$ between the START and END nodes.

Automated detection of these configurations is crucial for algorithmic analysis, particularly when dealing with arbitrary and nested resistor arrangements.

---

### 4.2 Series Configuration

Two resistors are in **series** if:
- They are connected **end-to-end**, i.e., one resistor's endpoint is the other's start point.
- The shared node does **not** connect to any other component (i.e., has degree 2).
- The **same current** flows through both.

#### 4.2.1 Detection Rule

Given three nodes $u$, $v$, and $w$, if the following conditions hold:
- $(u, v) \in E$ and $(v, w) \in E$,
- $\deg(v) = 2$,
- $v \neq \text{START}$ and $v \neq \text{END}$,

then the resistors $R_{uv}$ and $R_{vw}$ can be combined in series:

$$
R_{\text{eq}}(u, w) = R_{uv} + R_{vw}
$$

The graph is updated by:
- Removing node $v$,
- Adding edge $(u, w)$ with weight $R_{\text{eq}}(u, w)$.

---

### 4.3 Parallel Configuration

Two or more resistors are in **parallel** if:
- They connect the **same two nodes**,
- Each provides an independent path for current between those nodes.

#### 4.3.1 Detection Rule

If multiple edges exist between the same node pair $(u, v)$:
- $\exists \{R_1, R_2, \dots, R_n\}$ connecting $u$ and $v$,
- Replace them with a single equivalent resistor:

$$
\frac{1}{R_{\text{eq}}(u, v)} = \sum_{i=1}^{n} \frac{1}{R_i}
$$

The graph is updated by:
- Removing all parallel edges,
- Adding one edge $(u, v)$ with the combined resistance $R_{\text{eq}}$.

---

### 4.4 General Algorithm Strategy

**Repeat the following until no further simplification is possible:**
1. Scan all nodes for degree-2 series candidates.
2. Collapse series connections using the rule in Section 4.2.
3. Detect and merge all parallel resistors using the rule in Section 4.3.
4. Update the graph structure accordingly.

This recursive simplification reduces the graph step-by-step while preserving the electrical behavior between the START and END nodes.

---

### 4.5 Handling Nested Structures

Series and parallel simplifications can be **nested** or **interleaved**, such as:

- A parallel branch that itself contains series resistors.
- A series connection where one element is a group of parallel resistors.

The algorithm must support recursive detection:
- Flatten inner structures before processing outer ones.
- Traverse the graph hierarchically or use pattern recognition for subgraphs.

---

### 4.6 Example

Given the network:

- $(1, 2, 3\,\Omega)$
- $(2, 3, 5\,\Omega)$
- $(1, 3, 10\,\Omega)$

- Resistors $(1, 2)$ and $(2, 3)$ are in **series**:

  $$
  R_{\text{series}} = 3 + 5 = 8\,\Omega
  $$

- Then, the 8 Ω resistor and the existing 10 Ω between $(1, 3)$ are in **parallel**:

  $$
  \frac{1}{R_{\text{eq}}} = \frac{1}{8} + \frac{1}{10} = \frac{9}{40} \quad \Rightarrow \quad R_{\text{eq}} = \frac{40}{9} \approx 4.44\,\Omega
  $$

---

### 4.7 Summary

Series and parallel detection forms the backbone of circuit simplification:

- **Series:** Collapse resistors along unbranched paths.
- **Parallel:** Merge resistors connecting identical node pairs.
- Ensure recursive handling of nested structures.

This is a key pre-processing step before applying more general techniques like graph traversal, matrix methods, or Y-Δ transforms.

---

## 5. Resistance Computation

### 5.1 Objective

After reducing a resistor network via series and parallel simplification, or in cases where such reductions are insufficient due to complex interconnections (e.g., multiple loops or bridges), we must compute the equivalent resistance between two specific nodes: the **START node** $A$ and the **END node** $B$.

This section presents rigorous methods for computing the effective resistance $R_{\text{eq}}(A, B)$ in arbitrary networks, using physical laws and graph-theoretic principles.

---

### 5.2 Physical Basis

Let a voltage $V$ be applied between nodes $A$ and $B$, resulting in a total current $I$. The equivalent resistance is given by Ohm's law:

$$
R_{\text{eq}}(A, B) = \frac{V}{I}
$$

The challenge is to determine $I$ for a given $V$ using laws of circuit analysis.

---

### 5.3 Kirchoff’s Laws

Two foundational principles are used:

- **Kirchhoff's Current Law (KCL):** The total current entering a node equals the total current leaving it.

  $$
  \sum I_{\text{in}} = \sum I_{\text{out}}
  $$

- **Kirchhoff's Voltage Law (KVL):** The total voltage change around any closed loop is zero.

  $$
  \sum_{\text{loop}} V = 0
  $$

Using these laws, we derive a system of equations representing the flow of current and distribution of voltage in the graph.

---

### 5.4 Method 1: Node Voltage Method

1. **Assign a voltage variable** $V_i$ to each node $i \in V$, with the reference voltage (e.g., $V_B = 0$).
2. **Use KCL** to write equations at each node, expressing the net current as zero:

   For node $i$:

   $$
   \sum_{j \in \mathcal{N}(i)} \frac{V_i - V_j}{R_{ij}} = 0
   $$

   where $\mathcal{N}(i)$ denotes the neighbors of node $i$.

3. Solve the resulting **linear system of equations**.
4. Compute the current from $A$ to $B$:

   $$
   I = \sum_{j \in \mathcal{N}(A)} \frac{V_A - V_j}{R_{Aj}}
   $$

5. Use $R_{\text{eq}} = \frac{V}{I}$ (e.g., set $V = 1$ for convenience).

---

### 5.5 Method 2: Effective Resistance via Laplacian Matrix

The **Laplacian matrix** $L$ of a graph encodes both connectivity and resistance:

- Let $R_{uv}$ be the resistance of edge $(u, v)$.
- Define the **conductance** as $C_{uv} = \frac{1}{R_{uv}}$.

Construct the **Laplacian**:

- $L_{ii} = \sum_{j \in \mathcal{N}(i)} C_{ij}$
- $L_{ij} = -C_{ij}$ for $i \ne j$

Let $L^{\dagger}$ be the **Moore-Penrose pseudoinverse** of $L$. Then the effective resistance between nodes $A$ and $B$ is:

$$
R_{\text{eq}}(A, B) = (e_A - e_B)^T L^{\dagger} (e_A - e_B)
$$

where $e_A$ and $e_B$ are indicator vectors with 1 at index $A$ or $B$ and 0 elsewhere.

This method is powerful for theoretical analysis and for computing resistances in **highly connected** or **cyclic** graphs.

---

### 5.6 Algorithmic Considerations

- Use **sparse matrix solvers** for large networks.
- Exploit **symmetry** and **planarity** if present.
- For small or moderately-sized graphs, the **node voltage method** is often sufficient and interpretable.

---

### 5.7 Example

Consider the triangle network with nodes $1$, $2$, and $3$, and edges:

- $(1, 2, 3\,\Omega)$
- $(2, 3, 5\,\Omega)$
- $(1, 3, 10\,\Omega)$

To find $R_{\text{eq}}(1, 3)$:
1. Combine $(1, 2)$ and $(2, 3)$ in series: $R = 3 + 5 = 8\,\Omega$
2. Then, combine with $(1, 3)$ in parallel:

   $$
   \frac{1}{R_{\text{eq}}} = \frac{1}{8} + \frac{1}{10} = \frac{9}{40}
   \quad \Rightarrow \quad
   R_{\text{eq}} = \frac{40}{9} \approx 4.44\,\Omega
   $$

---

### 5.8 Summary

To compute equivalent resistance:
- Use **simplification** when possible (series/parallel).
- Apply **Kirchhoff’s laws** to derive current-voltage relations.
- For general graphs, use **Laplacian matrix methods** and pseudoinverses.
- Always calculate $R_{\text{eq}} = \frac{V}{I}$ after solving for current or voltage.

These techniques ensure correctness across all circuit topologies—from simple chains to complex meshes.

---

## 6. Complex Network Reduction

### 6.1 Motivation

While many resistor networks can be simplified using basic **series** and **parallel** rules, complex topologies often contain **loops**, **bridges**, or **interlaced structures** that resist straightforward reduction. For such networks, we require more sophisticated methods grounded in graph theory and linear algebra.

Two general strategies are applied:
- **Recursive simplification**: Extend series/parallel logic using traversal and pattern detection.
- **Graph-based algorithms**: Use tools like **node elimination**, **matrix methods**, and **Y-Δ (star-delta) transforms** to reduce the network.

---

### 6.2 Recursive Simplification

Recursive simplification automates the identification of reducible structures through iterative scanning of subgraphs.

#### 6.2.1 Recursive Algorithm Steps
1. **Search for series or parallel structures**.
2. **Reduce** the identified substructure.
3. **Update** the graph.
4. **Repeat** until no more reductions can be made.

This process may be implemented via depth-first or breadth-first search to locate collapsible subgraphs. It also forms the basis for symbolic circuit solvers.

---

### 6.3 Node Elimination

A powerful technique derived from linear algebra is **node elimination**, where non-terminal nodes are removed and their connections replaced by equivalent resistive links.

#### 6.3.1 Example

Suppose node $v$ connects nodes $u$ and $w$ via $R_{uv}$ and $R_{vw}$. Eliminating $v$ results in:

$$
R_{uw}^{\text{new}} = R_{uv} + R_{vw}
$$

if no other edges are present. This can be extended to more general structures by manipulating the **Laplacian matrix** or applying graph contraction.

---

### 6.4 Y-Δ (Star-Delta) Transforms

Some resistor networks contain **triangular** or **Y-shaped** subgraphs that cannot be reduced by series/parallel rules. The **Y-Δ transform** converts between these two equivalent forms to enable further simplification.

#### 6.4.1 Δ to Y Conversion

Given a triangle with resistors $R_{ab}$, $R_{bc}$, and $R_{ca}$, the equivalent star resistors are:

$$
R_a = \frac{R_{ab} R_{ca}}{R_{ab} + R_{bc} + R_{ca}}, \quad
R_b = \frac{R_{ab} R_{bc}}{R_{ab} + R_{bc} + R_{ca}}, \quad
R_c = \frac{R_{bc} R_{ca}}{R_{ab} + R_{bc} + R_{ca}}
$$

#### 6.4.2 Y to Δ Conversion

Given a Y-network with resistors $R_a$, $R_b$, $R_c$ connected to a central node:

$$
R_{ab} = \frac{R_a + R_b + R_a R_b / R_c}, \quad \text{and cyclic permutations}
$$

Applying such transforms can unlock simplifications otherwise blocked by network geometry.

---

### 6.5 Matrix-Based Reduction

Another general method is to solve the **system of linear equations** describing the network:

- Define the **Laplacian matrix** $L$ of the graph using conductances $C_{uv} = 1 / R_{uv}$.
- Solve the equation $L \mathbf{v} = \mathbf{i}$ with boundary conditions (fixed voltages at START and END nodes).
- Derive total current $I$ and compute:

$$
R_{\text{eq}} = \frac{V}{I}
$$

This method generalizes to **arbitrary networks** and supports **symbolic** and **numeric** computation.

---

### 6.6 Summary

To reduce complex resistor networks:
- **Use recursive simplification** for detectably nested structures.
- **Apply node elimination** to remove intermediate nodes.
- **Perform Y-Δ transformations** for triangular or star subgraphs.
- **Use Laplacian methods** for fully arbitrary topologies.

These tools allow rigorous analysis of circuits far beyond what manual reduction permits and are essential for building scalable solvers.

---

## 7. Resistance Computation

### 7.1 Objective

Once the resistor network has been simplified—either through recursive reduction or more advanced graph-based transformations—the final step is to **compute the total equivalent resistance** between two specified nodes: the **START node** $A$ and the **END node** $B$.

This scalar value, denoted as $R_{\text{eq}}(A, B)$, characterizes the electrical behavior of the entire network as seen from terminals $A$ and $B$.

---

### 7.2 Assumption: Simplified Graph

We assume the circuit graph $G = (V, E)$ has already been reduced as much as possible using:

- Series/parallel simplification,
- Y-Δ transformations (if applicable),
- Node elimination (optional),
- Or left in its original form if handled algorithmically.

All remaining resistors are considered **essential**—i.e., no further simplification is evident from the graph's structure alone.

---

### 7.3 Fundamental Approach

The total equivalent resistance is computed using:

$$
R_{\text{eq}} = \frac{V}{I}
$$

where:
- $V$ is the potential difference applied between nodes $A$ and $B$,
- $I$ is the total current flowing between these nodes.

The methods to compute $I$ depend on whether the graph is simple (e.g., a chain or tree) or arbitrary (containing cycles, bridges, etc.).

---

### 7.4 Direct Computation in Simple Cases

In very simple cases—e.g., when only a single path or two resistors in parallel remain—the equivalent resistance can be directly computed using the known rules:

#### 7.4.1 Series:
$$
R_{\text{eq}} = R_1 + R_2 + \cdots + R_n
$$

#### 7.4.2 Parallel:
$$
\frac{1}{R_{\text{eq}}} = \frac{1}{R_1} + \frac{1}{R_2} + \cdots + \frac{1}{R_n}
$$

These cases require no further analysis and can be returned immediately.

---

### 7.5 General Case: Node Voltage Method

When the graph contains cycles or complex interconnections, we apply **Kirchhoff’s Laws** and linear algebra.

#### 7.5.1 Steps:
1. Fix node $B$ as reference: $V_B = 0$
2. Apply KCL at all non-terminal nodes:

   $$
   \sum_{j \in \mathcal{N}(i)} \frac{V_i - V_j}{R_{ij}} = 0
   $$

3. Solve the resulting linear system for all unknown node voltages $V_i$.
4. Compute current leaving $A$:

   $$
   I = \sum_{j \in \mathcal{N}(A)} \frac{V_A - V_j}{R_{Aj}}
   $$

5. Finally, compute:

   $$
   R_{\text{eq}}(A, B) = \frac{V_A - V_B}{I}
   $$

In practice, it is convenient to choose $V_A = 1$ and $V_B = 0$.

---

### 7.6 Laplacian Matrix Method (Optional)

In symbolic or large-scale computation, we use the **graph Laplacian** $L$ and its pseudoinverse $L^\dagger$:

$$
R_{\text{eq}}(A, B) = (e_A - e_B)^T L^\dagger (e_A - e_B)
$$

where $e_A$ and $e_B$ are unit vectors corresponding to nodes $A$ and $B$.

This method guarantees correctness and generality, even on arbitrary networks with thousands of components.

---

### 7.7 Visualization

It is helpful to visualize the **final simplified graph** before computing $R_{\text{eq}}$, to ensure no redundant paths remain and to trace current paths conceptually.

Plotting tools like NetworkX + Matplotlib in Python allow us to inspect the reduced graph before final computation.

---

### 7.8 Summary

- If the simplified graph contains only a few components, apply direct formulas.
- For general networks, use the **node voltage method**.
- For symbolic or matrix-based workflows, use the **Laplacian pseudoinverse method**.
- Always finalize by computing:

  $$
  R_{\text{eq}} = \frac{V}{I}
  $$

This value encapsulates the total resistance between START and END nodes and is the ultimate goal of the entire reduction process.

---

## Plot and Visualization

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