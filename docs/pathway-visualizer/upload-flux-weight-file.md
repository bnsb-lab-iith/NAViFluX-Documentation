The **Upload Flux Weight File** feature allows you to assign flux values to reactions in the pathway. These weights are then reflected in the **visualization** as **color gradient of reaction nodes**

### Input
Upload a two-column CSV file formatted as:

| Reaction        | Flux   |
| --------------- | ------ |
| `EX_glc__D_e` | `12.5` |
| `PYK`         | `4.2`  |

* **Reaction** — the reaction ID exactly as it appears in the model.
* **Flux** — a numeric value representing the computed or estimated flux through that reaction (e.g., FBA, pFBA, Flux Variability results).


!!! tip "Recommended"
    Check out the [Upload Reaction Weight File](./upload-reaction-weight-file.md) for more details.



