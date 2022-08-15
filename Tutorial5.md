# Tutorial_5

In this tutorial, you will create an Azure Synapse Analytics Workspace and will explore options to read data from an external table.

Prerequisite: 

Create an Azure Synapse Analytics workspace.

<img width="1446" alt="image" src="https://user-images.githubusercontent.com/43130622/161353298-427cb71e-ffdb-4317-9d63-ddd95158b6b8.png">


Step 1: Create a new database 'coviddemo' using the command:

CREATE DATABASE covid_demo;

Step 2: Select the Coviddemo database as your current database

<img width="1789" alt="image" src="https://user-images.githubusercontent.com/43130622/161354532-b2c2cf23-0aa8-4b30-a824-51cb394d5d9b.png">


Step 3: Add the Covid-19 dataset from the gallery

<img width="361" alt="image" src="https://user-images.githubusercontent.com/43130622/161357248-fda03252-3d31-4ba8-a42c-746613988516.png">


Step 4: Create an external data source to this dataset

IF NOT EXISTS (SELECT * FROM sys.external_data_sources WHERE name = 'public_pandemicdatalake_blob_core_windows_net') 
	CREATE EXTERNAL DATA SOURCE [public_pandemicdatalake_blob_core_windows_net] 
	WITH (
		LOCATION   = 'https://pandemicdatalake.blob.core.windows.net/public', 
	)
Go

Step 4: Create a file format to access parquet using the following command

IF NOT EXISTS (SELECT * FROM sys.external_file_formats WHERE name = 'SynapseParquetFormat') 
	CREATE EXTERNAL FILE FORMAT [SynapseParquetFormat] 
	WITH ( FORMAT_TYPE = PARQUET)
GO

Step 5: Create an external table pointing to this location 

CREATE EXTERNAL TABLE covidcases.covid19data (
	[id] int,
	[updated] date,
	[confirmed] int,
	[confirmed_change] int,
	[deaths] int,
	[deaths_change] smallint,
	[recovered] int,
	[recovered_change] int,
	[latitude] float,
	[longitude] float,
	[iso2] varchar(8000),
	[iso3] varchar(8000),
	[country_region] varchar(8000),
	[admin_region_1] varchar(8000),
	[iso_subdivision] varchar(8000),
	[admin_region_2] varchar(8000),
	[load_time] datetime2(7)
	)
	WITH (
	LOCATION = 'curated/covid-19/bing_covid-19_data/latest/bing_covid-19_data.parquet',
	DATA_SOURCE = [public_pandemicdatalake_blob_core_windows_net],
	FILE_FORMAT = [SynapseParquetFormat]
	)
GO


Step 5: Query the table to read data from the external table.

<img width="1391" alt="image" src="https://user-images.githubusercontent.com/43130622/161357343-5f10e648-d004-4c27-9a52-9f2da1852602.png">




