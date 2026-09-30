# Online Retail Market Basket Analysis with Apriori

A Python market basket analysis project that uses the **Apriori algorithm** to identify products frequently purchased together in the UCI Online Retail dataset.

## Project overview

The notebook analyses approximately 540,000 retail transaction records from a UK-based online retailer between December 2010 and December 2011. It cleans transaction data, explores purchasing behaviour, converts invoices into basket-level data, and mines association rules for product recommendations.

The analysis uses country-level segmentation because global rules were too sparse at the selected support threshold. France is used as the detailed example, where stronger co-purchase patterns emerged.

## Dataset

- **Source:** UCI Machine Learning Repository — Online Retail dataset
- **Records:** 541,909 transaction lines
- **Period:** December 2010 to December 2011
- **Fields:** `InvoiceNo`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `UnitPrice`, `CustomerID`, and `Country`

The notebook downloads the dataset from a Google Drive link at runtime; the raw CSV is not committed to this repository.

## Workflow

1. Clean the data by removing missing descriptions, non-product/event descriptions, and cancelled invoices.
2. Convert `InvoiceDate` to datetime and set `Country` as a categorical field.
3. Perform exploratory analysis of top products, country distribution, and basket sizes.
4. Create a one-hot encoded invoice-product matrix.
5. Mine frequent itemsets with `mlxtend.frequent_patterns.apriori`.
6. Generate and filter association rules using support, confidence, and lift.
7. Group strong country-level rules into a recommendation lookup table.

## Tools

- Python
- pandas
- mlxtend
- matplotlib
- seaborn
- gdown

Install the requirements:

```bash
pip install pandas mlxtend matplotlib seaborn gdown
```

## Example output

At a global `min_support=0.05`, the analysis found only frequent single products, showing that purchasing patterns vary substantially across countries.

For France, country-level analysis produced 360 association rules. Meaningful examples included party-supply bundles:

| Antecedent | Consequent | Support | Confidence | Lift |
|---|---:|---:|---:|---:|
| SET/20 RED RETROSPOT PAPER NAPKINS + SET/6 RED SPOTTY PAPER CUPS | SET/6 RED SPOTTY PAPER PLATES | 9.95% | 97.5% | 7.64 |
| SET/6 RED SPOTTY PAPER PLATES + SET/20 RED RETROSPOT PAPER NAPKINS | SET/6 RED SPOTTY PAPER CUPS | 9.95% | 97.5% | 7.08 |

A lift above 1 indicates a positive association. These results suggest that the red retrospot/spotty party products are strong candidates for bundled promotions and cross-sell recommendations.

> Note: Rules with `POSTAGE` as the consequent are statistically valid but are excluded from practical product-recommendation interpretation because postage appears in about 76.5% of French invoices.

## Repository structure

```text
.
├── Market_Basket_Analysis_using_Apriori.ipynb
└── README.md
```

## How to run

1. Clone the repository.
2. Install the packages above.
3. Open `Market_Basket_Analysis_using_Apriori.ipynb` in Jupyter Notebook, JupyterLab, VS Code, or Google Colab.
4. Run the cells in order. The notebook downloads the source data automatically.

## Key takeaways

- Broad global retail data may hide meaningful product relationships.
- Segmenting transactions by country revealed more useful local patterns.
- Party-supply and themed product variants showed strong co-purchase behaviour in France.
- Association rules should be assessed with lift and business relevance, not confidence alone.

## License

This repository is intended for portfolio and educational use. The dataset remains subject to the terms of its original source.