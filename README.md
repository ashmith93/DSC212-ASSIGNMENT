
# Recursive Spectral Partitioning: The Karate Club Analysis
**DSC212: Graph Theory | Research Assignment**

**NAME : ASHMITH S S**

**ROLL NUMBER : IMS24047**

![Language](https://img.shields.io/badge/Python-3.8%2B-3776AB?style=flat&logo=python&logoColor=white)
![Library](https://img.shields.io/badge/NetworkX-Graph%20Mining-darkgreen?style=flat)
![Method](https://img.shields.io/badge/Algorithm-Spectral%20Bisection-purple)
![Status](https://img.shields.io/badge/Submission-Ready-success)

---

## Abstract
This project implements a **Recursive Spectral Modularity Optimization** algorithm to detect community structures within the famous **Zachary's Karate Club** network. 

By computing the leading eigenvectors of the **Modularity Matrix ($B$)**, we mathematically identify the social "fault lines" that led to the historic split between the club's instructor ("Mr. Hi") and the administrator. Furthermore, this study tracks the dynamic evolution of node centrality metrics as the network fractures into smaller sub-communities.

---

## Project Objectives & Tasks

This repository fulfills the following assignment requirements:

- [x] **Task 1: Recursive Partitioning** Implement the spectral bipartition algorithm to recursively split the graph until the leading eigenvalue $\lambda_1 \le 0$.
  
- [x] **Task 2: Dynamic Visualization** Visualize the graph state after each split, maintaining a fixed layout to clearly highlight community evolution.

- [x] **Task 3: Metric Computation** Calculate four key metrics after every iteration:
  * *Degree Centrality*
  * *Betweenness Centrality*
  * *Closeness Centrality*
  * *Clustering Coefficient*

- [x] **Task 4: Evolution Analysis** Plot and analyze how these metrics change for key nodes (e.g., Node 0 and Node 33) as the community structure is refined.

---

## Mathematical Methodology

The core of the analysis relies on the **Modularity Matrix $B$**, defined as the difference between the actual adjacency matrix $A$ and a null model based on degree distribution:

$$B_{ij} = A_{ij} - \\frac{k_i k_j}{2m}$$

### The Recursive Algorithm:
1.  **Construct $B^{(C)}$:** Form the modularity matrix for the current community $C$.
2.  **Eigen-Decomposition:** Solve for the leading eigenpair $(\lambda_1, u_1)$.
3.  **Check Modularity Gain:**
    * If $\lambda_1 > 0$: Split community $C$ into two groups based on the signs of elements in $u_1$.
    * If $\lambda_1 \le 0$: Stop; the community is indivisible.
4.  **Recurse:** Apply steps 1-3 to all resulting subgroups.

---

## Key Findings & Metric Evolution

The algorithm successfully recovers the ground-truth split between the **Mr. Hi** faction and the **Officer** faction. The metric analysis revealed:

| Metric | Observation |
| :--- | :--- |
| **Degree Centrality** | **Static/Decreasing.** Since this is a local measure dependent on subgraph size, it naturally decreases as communities shrink. It acts as a baseline for node connectivity. |
| **Betweenness** | **Dynamic Shifts.** Global leaders (Nodes 0 & 33) start with peak betweenness. As the graph splits, their scores drop, and new "local bridges" emerge within the sub-communities. |
| **Closeness** | **Increases.** Counter-intuitively, closeness scores often rise because the "average distance" to other nodes drops significantly within small, tight-knit communities. |
| **Clustering** | **Increases.** The algorithm effectively isolates dense cliques, resulting in higher clustering coefficients for nodes deeply embedded in their factions. |

---

## Repository Structure

```text
├── DSC212_Modularity_Ashmith_IMS24047.ipynb  # Primary Analysis Notebook
├── README.md                            # Project Documentation
