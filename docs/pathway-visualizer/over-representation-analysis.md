Over Representation Analysis evaluates whether user-selected reactions are statistically over-represented within GEM subsystems by applying hypergeometric enrichment using GSEApy, enabling pathway-level interpretation of reaction-based perturbations.

### Input 
A one column CSV File containing reaction names in each row

### Workflow 

![Over Representation Analysis](./../images/pathway-visualizer/ora.png)

### ORA Result Column Descriptions

| Column Name        | Intepretations                                                                                                           |
|--------------------|--------------------------------------------------------------------------------------------------------------------|
| **Adjusted P-value** | Multiple testing corrected p-value (FDR). Indicates statistical significance after adjusting for false positives. |
| **Combined Score**  | A weighted score combining p-value and enrichment magnitude (from Enrichr/GSEApy formula). Higher = stronger enrichment. |
| **Gene_set**        | Identifier for the gene set or pathway group being tested (e.g., subsystem index).                               |
| **Genes**           | List of input reactions/genes that overlap with the pathway being tested.                                         |
| **Odds Ratio**      | Measure of enrichment strength; ratio of observed vs expected overlap. >1 suggests over-representation.           |
| **Overlap**         | Count of overlapping reactions vs total available in the pathway (e.g., `6/6` = 6 out of 6).                      |
| **P-value**         | Significance score from hypergeometric test before multiple testing correction.                                   |
| **Term**            | Name of the pathway or subsystem being enriched (e.g., Glycolysis, TCA Cycle).                                     |
