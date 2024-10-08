# End-to-End-data-engineering-project
End to end Dataengineering project from On-premise SQL table to powerBI analysis

This project demonstrates an end-to-end Azure data engineering solution, starting from a local SQL database and culminating in Power BI reporting, all automated.

Thanks to [Mr. K Talks Tech](https://www.youtube.com/@mr.ktalkstech) for the project inspiration.

## Business Objective

This project serves as a learning opportunity for common data engineering practices, focusing on ETL pipeline techniques. The skills sharpened here are valuable for small to medium-sized businesses aiming to migrate their local data to the cloud.

![Insert Image](https://github.com/Manjusree-Azure/End-to-End-data-engineering-project/blob/main/Project%20Architecture.png)

## Current Environment





- Utilized the AdventureWorks dataset from Microsoft.
- Set up an on-premises Microsoft SQL server on a personal computer.
- Imported the dataset using Microsoft SQL Server Management Studio.
- ![Insert Image](https://github.com/Manjusree-Azure/End-to-End-data-engineering-project/blob/main/Source%20Data_AdventureWorksLT2017.png)

- ## 1: Resource Setup for the Project
- ![Insert Image](https://github.com/Manjusree-Azure/End-to-End-data-engineering-project/blob/main/Resource%20Setup.png)

- ## 2: Data Ingestion

Data ingestion from the on-premises SQL server to Azure SQL is accomplished via Azure Data Factory. The process involves:

1. Installation of Self-Hosted Integration Runtime.
 
3. Establishing a connection between Azure Data Factory and the local SQL Server.
4. Setting up a copy pipeline to transfer all tables from the local SQL server to the Azure Data Lake's "bronze/RootLayer" folder.

- ![Insert Image](https://github.com/Manjusree-Azure/End-to-End-data-engineering-project/blob/main/Self%20Hosted%20integration%20runtime.png)

- Data in Azure data lake Gen 2
- ![Insert Image](https://github.com/Manjusree-Azure/End-to-End-data-engineering-project/blob/main/Ingest%20data%20in%20ADLGen2.png)

- - ## : Data Ingestion using ADF pipeline using lookup and forEach activity
  - - ![Insert Image](https://github.com/Manjusree-Azure/End-to-End-data-engineering-project/blob/main/ADF%20pipeline.png)

## 2: Data Transformation

After ingesting data into the "bronze/Rootlayer" folder, it is transformed following the medallion data lake architecture (bronze, silver, gold). Data transitions through bronze, silver, and ultimately gold, suitable for business reporting tools like Power BI.

Azure Databricks, using PySpark, is used for these transformations. Data initially stored in parquet format in the "bronze" folder is converted to the delta format as it progresses to "silver" and "gold." This transformation is carried out through Databricks notebooks:

1. Mount the storage.
2. Transform data from "bronze" to "silver" layer.
3. Further transform data from "silver" to "gold" layer.
   
![Databricks Notebooks](https://github.com/Manjusree-Azure/End-to-End-data-engineering-project/blob/main/mount%20storage%20ac.ipynb)
![Databricks Notebooks](https://github.com/Manjusree-Azure/End-to-End-data-engineering-project/blob/main/mount%20storage%20ac.ipynb)
![Databricks Notebooks](https://github.com/Manjusree-Azure/End-to-End-data-engineering-project/blob/main/mount%20storage%20ac.ipynb)

Azure Data Factory is updated to execute the "bronze" to "silver" and "silver" to "gold" notebooks automatically with each pipeline run.

   
    


 


