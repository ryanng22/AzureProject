# Azure Pharmacy Data Pipeline Project

![workflow](https://github.com/ryanng22/AzureProject/assets/106357350/848a04a5-bf55-4975-8af4-ab01aff0a551)

Utilizing Azure services to extract, transform, and load data into a data warehouse environment.

Data Source:  
Mock pharmacy data with files for transactions, medications, patients, and insurance types

Blob Storage Layer: Azure Data Lake Storage Gen 2  
Interim staging environment to consolidate into one transformation process

Transform Layer: Azure Databricks  
Fill NULLs and drop duplicate records in transactions file.  
Implementation of slowly changing dimensions type 2 to capture most recent insurance per patient.  
Transform all files into parquet to minimize storage and increase performance.  

Analytics Environment: Azure Synapse Analytics Dedicated SQL Pool (FKA Azure Datawarehouse)  
Store parquet files into their respective warehouse tables. Mapping below:  
Transactions -> FactTransactions  
Medications -> DimMedications  
Patients -> DimPatients  
Insurance -> DimInsurance  

Monitoring: Azure Event Hubs  
Capture monitoring logs from data warehouse using Event Hubs service  

Log Analytics: Azure Stream Analytics  
Create job that ingests log data from Event Hubs and outputs logs for data warehouse monitoring  
