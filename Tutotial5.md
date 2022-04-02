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


Copy data from Dim_Date csv file from Azure data lake  to Dim_Date table.

1. Upload the Dim_Date.csv file to datalake.

2. Create a dedicated SQL pool.

<img width="1791" alt="image" src="https://user-images.githubusercontent.com/43130622/161359849-ec7847ac-755a-4628-833d-0b9de46cd1f3.png">

3. Create a new data copy under integrate pane.

<img width="1792" alt="image" src="https://user-images.githubusercontent.com/43130622/161357911-cc988327-f0f6-4400-9111-d6771eedec02.png">


3. Select the built in option and select the connection to the file.

<img width="1785" alt="image" src="https://user-images.githubusercontent.com/43130622/161357927-9ec9ba7d-fe3d-4677-bb79-991894fd61e1.png">

<img width="1792" alt="image" src="https://user-images.githubusercontent.com/43130622/161357961-10b82b5e-e586-4a76-8e90-d3cefb99c280.png">

<img width="1787" alt="image" src="https://user-images.githubusercontent.com/43130622/161357978-521ff0d1-3397-4e35-aef1-cdd5c1d8f23d.png">

4. Choose the connection and select the table name 

<img width="1792" alt="image" src="https://user-images.githubusercontent.com/43130622/161360008-c55198ca-17d3-440e-8392-08a5cc6a72c0.png">


5. Check the column mapping 

<img width="1788" alt="image" src="https://user-images.githubusercontent.com/43130622/161358240-d7464e7b-2878-40c7-8665-2da88154cc5c.png">


6. Deploy the process

<img width="1790" alt="image" src="https://user-images.githubusercontent.com/43130622/161360087-60b4a12b-d96c-4e08-9536-05a5abb857e9.png">


<img width="1136" alt="image" src="https://user-images.githubusercontent.com/43130622/161360135-0857e4f6-3c7b-41e5-9176-99da6325cd04.png">

