# **Notations**

In MATRIX, the metabolic network is represented as a **bipartite graph** consisting of two distinct node types:

- **Reaction nodes** (representing biochemical reactions)
- **Metabolite nodes** (representing chemical compounds)

Edges (arrows) in the graph denote the **directionality** of reactions based on model constraints.
This section explains the **visual notations** used for nodes and edges in the application.

---

## **Node Notations**

### **🔹 Reaction Nodes**

Reaction nodes are displayed as **rectangles**. Their appearance is determined by two properties:

##### **1. Normalized Weights (Color Encoding)**

- Each reaction node is assigned a **normalized weight** in the range **[0, 1]**.
- Colors transition from **light blue → dark blue** as the weight increases.
- Higher weights correspond to **darker shades**, making it easier to visually identify high-influence reactions.

##### **2. Size**

- Reaction nodes have a **fixed size**, kept constant for readability.

```
![ReactionNode-Image]
```

---

### **🔸 Metabolite Nodes**

Metabolite nodes are represented as **orange circles**.
They maintain:

- **Fixed size**
- **Fixed color**

```
![Metabolite-Image]
```

---

## **Edge Notations**

Edges describe the **directionality** of reactions in the bipartite network.

!!! tip "Priority Rule: Bounds > Flux"
    1. If **lower bound (`lb`)** and **upper bound (`ub`)** are defined, directionality is determined **from the bounds**.
    2. If **bounds are missing**, the **flux value** is used to determine directionality.

---

## **Direction Cases**

| **Case** | **Conditions**            | **Direction Meaning**                | **Arrow Notation** |
| -------- | ------------------------- | ------------------------------------ | ------------------ |
| **1**    | `lb = -1000`, `ub = 1000` | Fully reversible                     | `←→`               |
| **2**    | `lb = -1000`, `ub = 0`    | Irreversible (reverse only)          | `←`                |
| **3**    | `lb = 0`, `ub = 1000`     | Irreversible (forward only)          | `→`                |
| **4**    | `lb = -250`, `ub = -150`  | Only negative flux allowed (reverse) | `←`                |
| **5**    | `lb = 150`, `ub = 450`    | Only positive flux allowed (forward) | `→`                |
| **6**    | `lb = -350`, `ub = 250`   | Reversible (asymmetric range)        | `←→`               |
| **7**    | No bounds, `flux > 0`     | Flux-based forward direction         | `→`                |
| **8**    | No bounds, `flux = 0`     | Inactive / no net flux               | `—`                |
| **9**    | No bounds, `flux < 0`     | Flux-based reverse direction         | `←`                |


