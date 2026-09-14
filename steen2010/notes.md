# Graph Theory and Complex Networks: An Introduction


**TABLE OF CONTENTS**:

1. [Introduction](#chapter-1-introduction)
    - 1.1 [Communication networks](#11-communication-networks)
    - 1.2 [Social networks](#12-social-networks)
2. [Foundations](#chapter-2-foundations)
    - 2.1 [Formalities](#21-formalities)
    - 2.2 [Graph representations](#22-graph-representations)

---

## Chapter 1: Introduction

**Complex Network** (informal definition): "large collection of interconnected nodes".
- "Generally so huge that it is impossible to understand or predict their overall behavior by looking into the behavior of individual nodes or links".

### 1.1 Communication networks

**Trees** (informal definition): networks in which, between any two nodes, messages could travel only through a unique path.

**Packet switching** *vs* **circuit switching**:
- <u>Packet switching</u>: When a switch (or node) receives a packet, it only decides to which next switch to forward the packet.
- <u>Circuit switching</u>: Firstly, two endpoints establish a path and then let all communication pass through such path.

### 1.2 Social Networks

**Small world** (informal definition): "two people can reach each other through a chainof just a handful of messages".

**Sociograms**:
- Introduced by Jacob Moreno in the 1930s.
- Graphical representation of a network: people are represented by dots or vertices, their relationships by lines connecting the dots (edges).

<br><img src="./img/sociogram.png"><br>

## Chapter 2: Foundations

### 2.1 Formalities

<u>**Definition 2.1**</u>: A <u>graph</u> $G$ consists of a collection $V$ of <u>vertices</u> and a collection $E$ of <u>edges</u>, which we write $G = (V,E)$. Each edge $e \in E$ is said to join two vertices, which are called its <u>end points</u>. If $e$ joins $u,v \in V$, we write $e = \langle u,v \rangle$. Vertices $u$ and $v$ are said to be <u>adjacent</u>. Edge $e$ is said to be <u>incident</u> with vertices $u$ and $v$, respectively.

**Special cases**:
- **Simple graphs**: do not have loops (an edge linking a node to itself) or multiple edges between two nodes.
- **Empty graph**: trivial graph, with no nodes and consequently no edges.
-  **Complete graph** (denoted $K_n$): a simple graph with $n$ nodes, with each node being connected to all other nodes.
- **Complement of a graph** $G$ (denoted $\overline G$): obtained from $G$ by removing all its edges and joining the vertices that were *not* adjacent.

<u>**Definition 2.2**</u>: For any graph $G$ and vertex $v \in V(G)$, the <u>neighbor set</u> $N(v)$ is the set of vertices (other than $v$) adjacent to $v$, that is:

$$
N(v) \stackrel{\text{def}}{=} \{ w \in V(G)\ |\ v \neq w, \exists\ e \in E(G) : e = \langle u,v \rangle \}.
$$

<br><img src="./img/example-graph.png"><br>

**Degree of a vertex**: number of edges that are incident with it.

<u>**Definition 2.3**</u>: The number of edges incident with a vertex $v$ is called the *degree* of $v$, denoted as $\delta (v)$. Loops are counted twice.

<u>**Theorem 2.1**</u>: For all graphs $G$, the sum of vertex degrees is twice the number of edges, that is:

$$
\displaystyle\sum_{v \in V(G)} \delta(v) = 2 \cdot |E(G)|.
$$

<u>**Proof**</u>: When we count the edges of a graph G by enumerating for each vertex v of G the edges incident with that vertex v, we are counting each edge exactly twice.

<u>**Corollary 2.1**</u>: For any graph, the number of vertices with odd degree is even.
- Let us split all vertices into two sets ($V_\text{odd}$ and $V_\text{even}$), based on whether the vertices have odd or even degree.
- We know that
    - $\sum_{v \in V} \delta(v)$ is even (Theorem 2.1);
    - $\sum_{v \in V} \delta(v) = \sum_{v \in V_\text{odd}} \delta(v) + \sum_{v \in V_\text{even}} \delta(v)$;
    - $\sum_{v \in V_\text{even}} \delta(v)$ is even;
- Thus, $\sum_{v \in V_\text{odd}} \delta(v)$ must add up to an even number, which means that the number of nodes with odd degree is even.

**Degree sequence**: list of degrees of all vertices in a graph.
- If every vertex in a graph has the same degree, the graph is called *regular*.
- A $k$-regular graph is one in which all vertices have degree $k$. Cubic graphs are a special case in which $k=3$.

<u>**Theorem 2.2**</u> ([Havel-Hakimi](https://en.wikipedia.org/wiki/Havel%E2%80%93Hakimi_algorithm)): Consider a list $\mathbf{s} = [d_1, d_2, ..., d_n]$ of $n$ numbers in descending order. This list is graphic if and only if $\mathbf{s}^{\ast} = [d^\ast_1, d^\ast_2, ..., d^\ast_{n-1}]$ of $n-1$ numbers is graphic as well, where:

$$
d^\ast_{i} = \begin{cases}
    d_{i+1} - 1, & \text{for } i=1,2, ..., d_1 \\
    d_{i+1}, & \text{otherwise}
\end{cases}
$$

<u>**Definition 2.4**</u>: A graph $H$ is a *subgraph* of $G$ if $V(H) \subseteq V(G)$ and $E(H) \subseteq E(G)$ such that for all $e \in E(H)$ with $e = \langle u,v \rangle$, we have that $u,v \in V(H)$. When $H$ is a subgraph of $G$, we write $H \subseteq G$.

<u>**Definition 2.5**</u>: Consider a graph $G$ and a subset $V^\ast \subseteq V(G)$. The *subgraph induced by* $V^\ast$ has vertex set $V^\ast$ and edge set $E^\ast$ defined by:

$$
E^\ast \stackrel{\text{def}}{=} \{ e \in E(G) \mid e = \langle u, v \rangle \text{ with } u,v \in V^\ast \}
$$

Likewise, if $E^\ast \subseteq E(G)$, the subgraph induced by $E^\ast$ has edge set $E^\ast$ and vertex set $V^\ast$ defined by: 

$$
V^\ast \stackrel{\text{def}}{=} \{ u,v \in V(G)\ |\ \exists\ e \in E^\ast : e = \langle u,v \rangle \}
$$

The subgraph induced by $V^\ast$ or $E^\ast$ is written as $G[V^\ast]$ or $G[E^\ast]$, respectively.

- Every graph $G = (V, E)$ having $n$ vertices can be seen as a subgraph of the complete graph $K_n$.
- Considering the complement $\overline G = (V, \overline E)$, then the *union* $G \cup \overline G$ (the graph with vertex set $V$ and edge set $E \cup \overline E$) corresponds to $K_n$.

<u>**Definition 2.6**</u>: Consider a simple graph $G=(V,E)$. The *line graph* of $G$, denoted as $L(G)$ is constructed from $G$ by representing each edge $e = \langle u,v \rangle$ from $E$ by a vertex $v_{e}$ in $L(G)$, and joining two vertices $v_{e}$ and $v_{e^\ast}$ if and only if edges $e$ and $e^\ast$ are incident with the same vertex in $G$.

<br><img src="./img/line-graph.png"><br>

**Special induced graphs**
- $G - v$ or $G[V(G) \backslash \{v\}]$: induced subgraph generated by removing vertex $v$.
- $G - e$ or $G[E(G) \backslash \{e\}]$: induced subgraph generated by removing edge $e$.

### 2.2 Graph representations

<br><img src="./img/adjacency-matrix.png"><br>

**Adjacency matrix**
- Consider a graph $G$ with $n$ vertices and $m$ edges.
- Its adjacency matrix $A$ is a table with $n$ rows and $n$ columns (square matrix), so that each entry $\mathbf{A}[i,j]$ denotes the number of edges joining vertices $v_i$ to $v_j$.
- Properties:
    - An adjacency matrix is *symmetric*, that is, for all $i,j$, $\mathbf{A}[i,j] = \mathbf{A}[j,i]$. (This is a consequence of representing edges as unordered pairs of vertices: $e = \langle v_i, v_j \rangle = \langle v_j, v_i \rangle$.)
    - A graph $G$ is simple if and only if for all $i,j$ $\mathbf{A}[i,j] \leq 1, i\neq j$ and $\mathbf{A}[i,i] = 0$ (there is at most one edge joining $v_i$ and $v_j$ and no loops).
    - $\delta(v_i) = \sum^{n}_{j=1} = \mathbf{A}[i,j]$, that is, the sum of row $i$ is equal to the degree of vertex $v_i$.

<br><img src="./img/incidence-matrix.png"><br>

**Incidence matrix**
- The incidence matrix of a graph $G$ has $n$ rows and $m$ columns (non-square), so that $\mathbf{M}[i,j]$ contains the number of times ($0$, $1$ or $2$) that edge $e_j$ is incident with vertex $v_i$.
- Properties:
    - $G$ has no loops if and only if for all $i,j$ $\mathbf{M}[i,j] \leq 1$.
    - $\forall i: \delta(v_i) = \sum^{m}_{j=1} = \mathbf{M}[i,j]$, that is, the sum of row $i$ is equal to the degree of vertex $v_i$.
    - Since every edge connects two (not necessarily distinct) endpoints, then $\forall j: \sum^{n}_{i=1} \mathbf{M}[i,j] = 2$.

> PAGE 33 (edge list)