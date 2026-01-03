---
hide:
  toc: true             # hides the right sidebar
---

### Improving essential gene predictions in *E. coli* using intuitive single-gene deletion simulations

Step 1: Model selection

The genome-scale metabolic model [*iJO1366*](http://bigg.ucsd.edu/static/models/iJO1366.mat) of *E. coli* was selected for this study.
The model in .mat format was downloaded from the [BiGG](http://bigg.ucsd.edu/) database and uploaded through Upload Options in NAViFluX.

[Insert image]

Step 2: Mapping gene essentiality to reactions

Genes from the [KEIO library](https://pmc.ncbi.nlm.nih.gov/articles/PMC1681482/) were mapped to their corresponding reactions in the iJO1366 model using gene-reaction associations.
Reactions associated with essential and non-essential genes were separated for comparative analysis.

[Insert image]

Step 3: Setting up the metabolic environment

The iJO1366 model was constrained to simulate growth in MOPS minimal medium.
Environmental constraints were applied using the same procedure described in Case Study 1.


[Insert image]

Step 4: Cycle-free Flux Balance Analysis (cFBA)

Cycle-free flux balance analysis (cFBA) was performed using the Flux Analysis module in NAViFluX.

[Insert image]

Step 5: Flux comparison between essential and non-essential reactions

Flux magnitudes of reactions associated with essential and non-essential genes were compared.
Non-essential reactions exhibited larger flux magnitudes, whereas essential reactions carried lower but indispensable fluxes.

[Insert image]


Step 6: Single-gene deletion simulation and model evaluation

Single-gene knockout simulations were performed in NAViFluX, available in "Flux Analyses" module.
Predicted growth rates were compared against KEIO essentiality annotations.

[Insert image]

Step 7: Investigating incorrect predictions (PRPPS case)
Phosphoribosyl pyrophosphate synthetase (PRPPS) is experimentally essential for biomass synthesis.
However, the default iJO1366 model predicted PRPPS to be non-essential. Exploration in NAViFluX revealed an alternative prpp synthesis route via Ribose-1,5-bisphosphokinase (R15BPK).

[Insert image]


Step 8: Constraint revision to remove alternative routes


The R15BPK reaction was constrained to 0 mmol/(gDW·hr) to eliminate the alternative prpp synthesis route. This forced biomass production to depend on PRPPS.
Similarly, glucose uptake via GLCptspp was partially constrained to maintain activity of HEX1, preserving realistic glucose catabolism.

[Insert image]

After applying minimal internal constraint revisions, gene essentiality predictions were recomputed.
The model performance improved slightly to an auROC of 0.76. 

Step 9: Constructing the prpp synthesis subnetwork.

To mechanistically study prpp synthesis, three subsystems were merged: Glycolysis, Pentose phosphate pathway, Histidine metabolism

[Insert image]

The resulting merged subnetwork represented net glucose catabolism towards prpp synthesis.


Step 12: Wild-type flux distribution

Cycle-free FBA was performed in the wild-type model using NAViFluX "Flux Analyses" module.

[Insert image]

Flux overlay showed that RPI-mediated oxidative PPP was the preferred route for prpp synthesis. This visualization was stored in NAViFluX’s native JSON format.

[Insert image]

Step 13: Single knockout of RPI

The RPI reaction was knocked out by fixing its flux bounds to zero.

[Insert image]

Following the knockout, prpp synthesis was rerouted entirely through the non-oxidative PPP, driven by TKT1 activity.

[Insert image]

Step 14: Double knockout of RPI and TKT1

A double knockout was simulated by constraining both RPI and TKT1 reactions to zero.
This eliminated both oxidative and non-oxidative PPP routes.

[Insert image]

The double knockout confirmed that RPI and TKT1 form a synthetic essential pair for prpp-dependent biomass synthesis.







