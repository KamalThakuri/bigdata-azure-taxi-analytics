# Notebooks

Run these in order:

1. **`01_explore_data.ipynb`** — initial data ingestion verification and quality assessment.
2. **`02_clean_transform.ipynb`** — bronze-to-silver cleaning + feature engineering.
3. **`03_analysis_ml.ipynb`** — analytics queries + gold aggregates + ML model.

## Requirements

- Azure Databricks Serverless compute (Premium workspace, Spark 3.5+)
- Unity Catalog External Locations configured for `bronze`, `silver`, `gold` containers
- Access Connector managed identity granted `Storage Blob Data Contributor` on the
  ADLS Gen2 storage account

## Configuration

Each notebook begins with a setup cell that defines:

```python
storage_account_name = "staxidatakc250253104"  # change this to yours
```

Update the storage account name to match your own deployment.

## Expected Outputs

- **Bronze** (`bronze/yellow_taxi/2023/`): 12 Parquet files (~606 MB total)
- **Silver** (`silver/yellow_taxi_2023/`): Delta table, 35.6M rows, partitioned by month
- **Gold** (`gold/`): 6 Delta tables —
  `monthly_summary`, `hourly_pattern`, `dow_pattern`, `top_pickup_zones`,
  `tip_analysis`, `payment_mix`, plus `ml_predictions_sample`
