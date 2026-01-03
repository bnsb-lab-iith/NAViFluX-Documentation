# Download Tool File

The **Download Tool File** feature allows you to export your current network as a `.json` file.  
This file can later be re-imported into the application using the **NAViFluX JSON Upload** option under the **Upload File** feature with all positions retained. 

!!! important "Important"
    This option only exports the **nodes and edges currently visible in the viewport**.  It does not export the full model.

!!! tip "Recommendation"
    To export the **entire model**, we recommend selecting all pathways in the dropdown, applying any changes, and then downloading the tool file.



##### Sample `.json` Structure

```json
{
  "nodes": [
    {
      "id": "PPC",
      "temp_id": "Anaplerotic reactions__PPC",
      "type": "custom",
      "position": {
        "x": 0,
        "y": 30
      },
      "data": {
        "abbreviation": "PPC",
        "info": "Phosphoenolpyruvate carboxylase",
        "flux": "Not Calculated",
        "subsystem": "Anaplerotic reactions",
        "lower_bound": 0,
        "upper_bound": 1000,
        "color": "#e0e0e0",
        "fontSize": 8,
        "size": null,
        "gene": [
          "b3956"
        ],
        "type": "reaction",
        "BIGG_crossref": [
          "PPC"
        ],
        "KEGG_crossref": [
          "R00345"
        ],
        "EC_crossref": [
          "4.1.1.31"
        ],
        "stoichiometry": {
          "co2_c": -1,
          "h2o_c": -1,
          "h_c": 1,
          "oaa_c": 1,
          "pep_c": -1,
          "pi_c": 1
        }
      },
      "width": 80,
      "height": 40
    },
    {
      "id": "pep_c",
      "temp_id": "Anaplerotic reactions__pep_c",
      "type": "custom",
      "position": {
        "x": 600,
        "y": 30
      },
      "data": {
        "abbreviation": "pep_c",
        "info": "Phosphoenolpyruvate",
        "formula": "C3H2O6P",
        "compartment": "Cytoplasm",
        "crossref": [
          "CHEBI:18021",
          "CHEBI:44894",
          "CHEBI:26054",
          "CHEBI:14812",
          "CHEBI:26055",
          "CHEBI:8147",
          "CHEBI:58702",
          "CHEBI:44897"
        ],
        "weight": "No weight",
        "color": "#FFA500",
        "fontSize": 8,
        "type": "metabolite"
      },
      "width": 30,
      "height": 30
    },
  ],
  "edges": [
    {
      "id": "edge_1764233361864_9j13",
      "source_id": "Anaplerotic reactions__pep_c",
      "target_id": "Anaplerotic reactions__PPC",
      "source": "pep_c",
      "target": "PPC",
      "sourceHandle": "right",
      "targetHandle": "left",
      "type": "default",
      "markerEnd": {
        "type": "arrowclosed",
        "color": "#222"
      },
      "style": {
        "strokeWidth": 2,
        "stroke": "#222"
      }
    },
  ]
}
```
