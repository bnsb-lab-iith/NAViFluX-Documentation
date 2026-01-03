The Add New Reaction feature for the model builder module is the same as that is present in the Pathway Visualizer module.

!!! important "Important"
    It is recommended to understand the notations of nodes and edges to proceed further with the documentation. [Check out the Notations](./notations.md)

!!! info "Note"
    When a model is uploaded, the server automatically detects whether the model is from KEGG or BiGG. Based on the database, corresponding reactions will be fetched for the selected metabolite

![Add Reaction Workflow](./../images/pathway-visualizer/add-reaction.png)

### About

The **Add New Reaction** feature allows you to expand your uploaded model dynamically.  
When you select a metabolite from the graph, the system queries the detected database (KEGG or BiGG) and retrieves all reactions in which that metabolite is **consumed** or **produced**.

From the suggested list, you can add one or more reactions to your model. This makes it easy to:

- Explore alternative metabolic routes.
- Extend incomplete pathways.

By iteratively adding reactions, you can refine your network and tailor it to the biological system you are modeling.

### Result Table

!!! info "Note"
    Once results are fetched for potential reactions where the selected metabolite is consumed or produced, you will be redirected to a table below the canvas.

Each row in the table corresponds to a potential reaction that can be added to the model.

| **Column**          | **Description**                                                                                                                                      |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Reaction**        | Identifier for the reaction (e.g., `PPC`, `ICL`)                                                                                                     |
| **Description**     | Full name of the reaction (e.g., _Phosphoenolpyruvate carboxylase_)                                                                                  |
| **Reaction string** | Stoichiometric equation showing substrates and products (e.g., `PEP + CO₂ → OAA`)                                                                    |
| **Lower bound**     | Minimum allowable flux value (e.g., `0` for irreversible reactions). **Default `-1000`**                                                             |
| **Upper bound**     | Maximum allowable flux value (e.g., `1000` for unconstrained forward flux). **Default `1000`**                                                       |
| **Subsystem**       | Pathway the reaction should belong to (chosse from existing subsystems). **Default: Reaction assigned to the subsystem, the metabolite was part of** |

!!! tip "Recommendation"
    It is recommended to understand the definitions of lower bound and upper bound to effectively apply them to the potential new reactions.
