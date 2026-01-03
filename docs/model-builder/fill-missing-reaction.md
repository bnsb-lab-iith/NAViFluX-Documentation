### **About**

The **Filling Missing Reactions** feature helps fill gaps in metabolic pathways. By selecting two metabolites in the graph, the system queries the detected database (KEGG or BiGG) to fetch all possible reactions that connect them.  

!!! warning "Note"
    The order of selection is important — the first metabolite is treated as the **substrate**, and the second as the **product**. 


This feature is especially useful for:

- Identifying missing links in incomplete or draft models  
- Reconstructing pathways when certain reactions are absent in the uploaded network  


!!! important "Important"
    It is recommended to understand the notations of nodes and edges to proceed further with the documentation. [Check out the Notations](./../pathway-visualizer/notations.md)

!!! info "Note"
    When a model is uploaded, the server automatically detects whether the model is from KEGG or BiGG. Based on the database, corresponding reactions will be fetched for the selected metabolite

![Fill Missing Reaction](./../images/pathway-visualizer/fill-missing-reaction.png)





### **Result table**

Each row in the table corresponds to a potential reaction that can be added to the model. 

| **Column**       | **Description**                                                                 |
|------------------|---------------------------------------------------------------------------------|
| **Reaction**     | Identifier for the reaction (e.g., `PPC`, `ICL`) |
| **Description**  | Full name of the reaction (e.g., *Phosphoenolpyruvate carboxylase*)             |
| **Reaction string** | Stoichiometric equation showing substrates and products (e.g., `PEP + CO₂ → OAA`) |
| **Lower bound**  | Minimum allowable flux value (e.g., `0` for irreversible reactions). **Default `-1000`**             |
| **Upper bound**  | Maximum allowable flux value (e.g., `1000` for unconstrained forward flux). **Default `1000`**     |

### **Assigning subsystem**

The **Fill missing reaction** follows a different approach to assign subsystem to the selected reaction. 

##### CASE 1
When the selected metabolites are of the same subsystem 

| **Metabolite ID** | **Full Name** | **Subsystem**     |
| ----------------- | ------------- | ----------------- |
| `icit_c`          | Isocitrate    | Citric Acid Cycle |
| `acon_c`          | Aconitase     | Citric Acid Cycle |

In this situtation, the new selected reaction is added to **Citric Acid Cycle** by default.

---

##### CASE 2
When the selected metabolites are **not** of the same subsystem

| **Metabolite ID** | **Full Name** | **Subsystem**     |
| ----------------- | ------------- | ----------------- |
| `icit_c`          | Isocitrate    | Citric Acid Cycle |
| `q8_c`          | Ubiquinone-8     | Oxidative Phosphorylation |

In this situation, you will be prompted a dropdown to select any of the above two subsystems
