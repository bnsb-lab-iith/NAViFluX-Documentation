An algorithm to assess the flow of metabolites occuring in a metabolic network. It answers the question **Given all the reactions in a metabolic network, how much of each metabolite is being produced or consumed at steady state?**


## **Analysis Workflow**

![Flux Analysis](./../images/pathway-visualizer/flux-analysis.png)

1. Select the **"Flux Analysis"** button under the **Analysis Options** dropdown. 

2. Set bounds for model associated reactions

3. Select an objective function. 

    !!! note "Selecting an objective function"
        A reaction that you want the model to maximize or minimize. 
        If you pick the **Biomass reaction** as the objective, the model will find a flux distribution where this reactions as strongly as possible subject to all constraints. 

4. Choosing a **Flux** algorithm

5. Once the analysis is done, the flux values acts as **weights** and are applied to the model that is reflected in the color gradient.

!!! tip "Recomended"
    To learn more about **Flux Weight File**. Check out [Uploading a Flux weight File](./upload-flux-weight-file.md)

---

## **Types of Flux Analysis Algorithms**

### Standard Flux-Balanace Analysis **(FBA)**

Standard FBA predicts the steady-state flux distribution in a metabolic network by optimizing an objective.

Maximize or minimize an objective function \(Z\) (e.g., biomass flux) using **Flux Balance Analysis (FBA)**:

$$
\text{maximize } Z = c^T v
$$

subject to:

$$
S \cdot v = 0 \quad \text{(steady-state mass balance)}
$$

$$
v_\text{min} \le v \le v_\text{max} \quad \text{(flux bounds)}
$$

Where:  

- \(S\) = stoichiometric matrix  
- \(v\) = vector of reaction fluxes  
- \(c\) = vector defining the objective (1 for biomass reaction, 0 for others)

****


### Cycle Free Flux (Loopless solution)

!!! info "Why was Loopless solution developed"
    Loopless solution was developed to solved the problem of standard FBA: **Possibility of predicting thermodynamically infeasible cycles**.  These cycles can produce flux distributions where metabolites appear to be produced without the substrate being consumed. 


Loopless FBA considers additional constraints to prevent such cycles and this algorithm becomes a Mixed Integer Linear Programming (MILP) problem that is computationally expensive.

Adds constraints to remove internal loops:

$$
v_j \cdot (v_j - M y_j) = 0 \quad \forall j \in \text{reversible reactions}
$$

Where:

- $y_j$ = binary variable indicating reaction direction  
- $M$ = a large constant (**Big-M method**)

---

### Single-Reaction Deletion

An approach where each reaction is deleted (knock-out) one at a time and the resulting flux distribution is calculated. 

This methods helps you to identify which reactions are essential for product formation as deletion of one reaction results in a loss of objective value. 

For each reaction $r_i$:

$$
v_i = 0
$$

Then solve **Standard FBA** or **Loopless FBA** to see how the objective $Z$ changes.

---

### Parsimonous Flux Balance Analysis (pFBA)

!!! info "Why was pFBA developed"
    pFBA was developed to solved the problem of standard FBA: **Flux Redundancy**. 

In some cases, multiple flux distributions achieve the same optimal objective value, but biologically not all are equally likely.  pFBA includes a second optimization step where the total flux is minimized, subject to achieving the same maximum objective. This tends to identify the most efficient flux distribution


Two-step Linear Program (LP):

1. Solve standard FBA to get optimal objective $Z^*$  

2. Minimize total flux while keeping $Z = Z^*$:

$$
\begin{aligned}
\text{minimize} \quad & \sum_j |v_j| \\
\text{subject to} \quad & S \cdot v = 0 \\
& v_{\min} \leq v \leq v_{\max} \\
& c^T v = Z^*
\end{aligned}
$$

---

### Flux Variability Analysis (FVA)

Flux Variability Analysis quantifies the **range of possible flux values** for each reaction while still achieving the same optimal objective value. Unlike FBA, which returns a single flux distribution, FVA reveals **alternative pathways** and **network flexibility**.

!!! info "Why was FVA developed"
Standard FBA provides only one optimal solution, even though many equally optimal solutions may exist.
FVA helps identify reactions that are **rigid (fixed flux)** versus **flexible (variable flux)** under the same biological objective.

For each reaction ( v_i ), FVA computes:

* **Minimum possible flux**
* **Maximum possible flux**

while keeping the objective fixed at its optimal value ( Z^* ).

For each reaction ( i ):

$$
\begin{aligned}
\text{minimize / maximize} \quad & v_i \\
\text{subject to} \quad & S \cdot v = 0 \\
& v_{\min} \le v \le v_{\max} \\
& c^T v = Z^*
\end{aligned}
$$

Where:

* ( Z^* ) is the optimal objective value obtained from standard FBA
* Each reaction is optimized **independently**

**Interpretation:**

* Narrow flux range → reaction is essential or tightly regulated
* Wide flux range → reaction is flexible or part of alternative pathways

---

### Single-Gene Deletion

Single-Gene Deletion simulates the **knockout of individual genes** to assess their impact on network functionality and the objective value.

!!! info "Why Single-Gene Deletion is useful"
Genes often control multiple reactions through gene–protein–reaction (GPR) associations.
Deleting a gene allows identification of **essential genes** and **genetic robustness** in the metabolic network.

For a gene ( g ):

* All reactions associated with ( g ) (based on GPR rules) are constrained to zero flux:

$$
v_j = 0 \quad \forall j \in \text{reactions associated with } g
$$

Then solve **Standard FBA** or **Loopless FBA** to compute the new objective value ( Z_g ).

**Interpretation:**

* ( Z_g = 0 ) → gene is **essential**
* ( Z_g < Z^* ) → gene is **important but non-essential**
* ( Z_g = Z^* ) → gene deletion has **no effect**

