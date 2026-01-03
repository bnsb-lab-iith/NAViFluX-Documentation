## Download Edge List

The **Download Edge List** feature allows you to export the reconstructed model as different types of edge lists: **Reaction–Metabolite**, **Metabolite–Metabolite**, or **Reaction–Reaction**.

---

#### Reaction–Metabolite

In this format, edges connect reactions to their associated metabolites.

Example:

```mermaid 
graph LR 
    A --> R1 
    B --> R1 
    R1 --> C 
    R1 --> D 

    %% Define styles
    classDef reaction fill:#4a90e2,stroke:#2c3e50,stroke-width:2px,rx:5px,ry:5px,color:#fff;
    classDef metabolite fill:#27ae60,stroke:#145a32,stroke-width:1.5px,color:#fff,stroke-dasharray:0;

    %% Assign classes
    class R1,R2,R3 reaction;
    class A,B,C,D,E,F,G metabolite;
```

| **Source** | **Target** | **Type**        |
| ---------- | ---------- | --------------- |
| A          | R1         | Substrate → Rxn |
| B          | R1         | Substrate → Rxn |
| R1         | C          | Rxn → Product   |
| R1         | D          | Rxn → Product   |

where

* **A, B**: Substrates
* **R1**: Reaction
* **C, D**: Products

**Note:** Directionality is preserved.

---

#### Metabolite–Metabolite

In this format, edges connect **substrates** to **products** through the reactions that consume/produce them.

Example:

```mermaid 
graph LR 
    A --> R1 
    B --> R1 
    R1 --> C 
    R1 --> D 

    %% Define styles
    classDef reaction fill:#4a90e2,stroke:#2c3e50,stroke-width:2px,rx:5px,ry:5px,color:#fff;
    classDef metabolite fill:#27ae60,stroke:#145a32,stroke-width:1.5px,color:#fff,stroke-dasharray:0;

    %% Assign classes
    class R1,R2,R3 reaction;
    class A,B,C,D,E,F,G metabolite;
```

| **Source** | **Target** | **Type**            |
| ---------- | ---------- | ------------------- |
| A          | C          | Substrate → Product |
| A          | D          | Substrate → Product |
| B          | C          | Substrate → Product |
| B          | D          | Substrate → Product |

where

* **A, B**: Substrates
* **C, D**: Products

**Note:** Directionality is preserved.

---

#### Reaction–Reaction

In this format, edges connect reactions via **shared metabolites**

Example:

```mermaid
graph LR
    %% Reaction 1: A + B → C
    A --> R1
    B --> R1
    R1 --> C

    %% Reaction 2: C → D + E
    C --> R2
    R2 --> D
    R2 --> E

    %% Reaction 3: D + F → G
    D --> R3
    F --> R3
    R3 --> G

    %% Define styles
    classDef reaction fill:#4a90e2,stroke:#2c3e50,stroke-width:2px,rx:5px,ry:5px,color:#fff;
    classDef metabolite fill:#27ae60,stroke:#145a32,stroke-width:1.5px,color:#fff,stroke-dasharray:0;

    %% Assign classes
    class R1,R2,R3 reaction;
    class A,B,C,D,E,F,G metabolite;


```

| **Source** | **Target** | **Shared Metabolite(s)** |
| ---------- | ---------- | ------------------------ |
| R1         | R2         | C                        |
| R2         | R3         | D                        |


where

* **R1** produces **C**
* **R2** consumes **C**
* **R2** produces **D**
* **R3** consumes **D**

