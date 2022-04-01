
# Tutorial 4

This tutorial shows how to create a data factory in Azure and built a pipeline to transform and move data to databases.

This tutorial teaches the following steps with regard to Azure Data Factory:

                                      1. Create an Azure Data factory in Portal
                                      2. Ingest data from Azure blob storage to Azure Data lake
                                      3. Publish the pipeline and explore the triggers
                                      4. Create dataflow to transform data and sync it to Database



We will be loading the population split by age group file from Azure Blob storage to Azure Data lake using Copy activity and will be wrapping this up in the pipeline. 



## 1. Create an Azure Data factory in Portal

1. Create the Azure Data factory resource by selecting the configuration as shown.

<img width="1205" alt="image" src="https://user-images.githubusercontent.com/43130622/161150180-0a641d20-b58c-43f7-b975-1e3a5c1fad0e.png">

***

2. Validate the configuration and deploy the resource.

<img width="1350" alt="image" src="https://user-images.githubusercontent.com/43130622/161150767-19063675-8689-4bea-80eb-53f0e5b59509.png">


***


3. The deployment is complete and we have our ADF ready now.

<img width="1592" alt="image" src="https://user-images.githubusercontent.com/43130622/161150850-cf9c2017-ee79-4c4d-8309-09c87cec8894.png">

## 2. Create an ADF pipeline to copy data from Blob storage to the Azure data lake

1. The requirement here is to copy the population_by_age.tsv.gz from Blob storage to the Azure data lake we created earlier and unzip the file.

2. Open the Azure Data factory you created previously.Go to the Manage tab and click on 'Linked Services' 

<img width="1180" alt="image" src="https://user-images.githubusercontent.com/43130622/161165548-327e4f2c-f797-4b8b-a47d-0361ffe5fa0a.png">

***

3. Create a linked service for Azure Blob storage

<img width="1187" alt="image" src="https://user-images.githubusercontent.com/43130622/161165727-416a683c-8436-4371-8dfd-a32657dc2472.png">

<img width="633" alt="image" src="https://user-images.githubusercontent.com/43130622/161165912-bd5064a7-d86a-4478-8912-55f9b424eb32.png">

<img width="631" alt="image" src="https://user-images.githubusercontent.com/43130622/161165943-4a0bc440-9e45-4969-b4d7-26d129eb98ae.png">


4. Repeat the same steps and create a Linked service for data lake storage - Gen 2

<img width="1192" alt="image" src="https://user-images.githubusercontent.com/43130622/161166545-0c59df0c-7589-47fe-9ff4-0925ff0f35c8.png">

<img width="1196" alt="image" src="https://user-images.githubusercontent.com/43130622/161166619-2b2a9759-8495-405d-a1f8-69fc235a0796.png">

<img width="939" alt="image" src="https://user-images.githubusercontent.com/43130622/161166646-350c3ff5-23fc-4fb2-ab38-43ead291dac7.png">

4. Create a dataset for accessing the file in Azure Blob storage

<img width="1194" alt="image" src="https://user-images.githubusercontent.com/43130622/161166836-a6c15a7d-19e7-475b-b65b-0808a13b03cf.png">

<img width="1206" alt="image" src="https://user-images.githubusercontent.com/43130622/161166890-9063094c-6754-450b-b404-703a23a4c59c.png">

<img width="1196" alt="image" src="https://user-images.githubusercontent.com/43130622/161166921-35af966b-f084-43e8-9d88-856571b8a6ff.png">

<img width="1201" alt="image" src="https://user-images.githubusercontent.com/43130622/161166977-a5f9208a-f325-4b62-96b3-419769d879eb.png">

<img width="1204" alt="image" src="https://user-images.githubusercontent.com/43130622/161167116-7c4ccff2-5d89-40ed-9354-c8b415431d45.png">

***

5. Repeat the same steps and create a dataset for target Data lake


<img width="1197" alt="image" src="https://user-images.githubusercontent.com/43130622/161167347-c05261d1-973c-47bf-93d2-3a81252d7ddd.png">

<img width="1193" alt="image" src="https://user-images.githubusercontent.com/43130622/161171392-4e3d443d-20f4-4f93-947e-771b0c317d51.png">


***

6. Validate the datasets and publish the dataset.

<img width="1792" alt="image" src="https://user-images.githubusercontent.com/43130622/161171566-06f72100-7b9e-44fd-815d-3a6ee3289a0f.png">

<img width="1790" alt="image" src="https://user-images.githubusercontent.com/43130622/161171593-df4490bb-d59b-4100-af60-a77a2bfebb93.png">

***

7. Create a pipeline pl_ingest_population_data to copy the data from Azure blob storage to Data lake using the copy activity.

<img width="840" alt="image" src="https://user-images.githubusercontent.com/43130622/161171971-c76d49a0-c6b6-40b5-ac05-f3cc46fb61da.png">

<img width="1198" alt="image" src="https://user-images.githubusercontent.com/43130622/161172454-786149dd-9342-44f4-8d3f-119b771aae3d.png">

<img width="1197" alt="image" src="https://user-images.githubusercontent.com/43130622/161172362-9f137142-6da9-4a93-8719-fdd7d794b559.png">

8. Check whether the file is copied to the Azure Data lake.

## 3. Publish the pipeline and explore the trigger

<img width="631" alt="image" src="https://user-images.githubusercontent.com/43130622/161175775-68bd9168-4220-4456-8fd2-6d7250293026.png">

## 4. Create Data flow to transform data


We will be doing the following transformations in the cases_deaths.csv file uploaded to Datalake.

                     1. We will do a lookup transformation to lookup 2 digit country code instead of 3 digit.

                     2. We will create a filter transformation to filter out Europe only data.

                     3. We will calculate the cases count and death count from indicator and daily count.

                     4. We will remove the unwanted columns from the file.

1. Create a folder lookup in the population container and upload the file to the directory.Also upload the cases_deaths.csv to the population container.

2. Create a data flow from the dataflow pane.

<img width="1199" alt="image" src="https://user-images.githubusercontent.com/43130622/161193789-f77eddab-ba67-41f3-8a98-c62482fcceec.png">

3. Create a source stream by pointing to the cases_deaths.csv file.

<img width="849" alt="image" src="https://user-images.githubusercontent.com/43130622/161194463-511324c8-0bb3-4fd0-a2f5-8e55b88c7879.png">

4. Create a filter transformation to filter data only related to Europe and filter the others.

Use the following expression to the filter :

continent == 'Europe' && not(isNull(country_code))

<img width="1193" alt="image" src="https://user-images.githubusercontent.com/43130622/161195717-fd50d479-ba70-4535-814b-5b3a5c90b816.png">

5. Create a select transformation to select only relevant column and filter out the columns which are not required.

name == 'date' then 'report'+ 'date'

<img width="1479" alt="image" src="https://user-images.githubusercontent.com/43130622/161201181-fc5a65f0-cdb3-49f1-9d43-047dd540e5db.png">

6.  Create a pivot transformation to get the cases count and death count from indicator and daily count.

<img width="1338" alt="image" src="https://user-images.githubusercontent.com/43130622/161201839-bb0479e8-10dd-49c0-818a-7947813c3305.png">

<img width="1092" alt="image" src="https://user-images.githubusercontent.com/43130622/161201925-c5b589f5-3627-4c95-a35a-8b6f59a85717.png">

<img width="1197" alt="image" src="https://user-images.githubusercontent.com/43130622/161202050-8242e904-051b-4f8d-959c-e4d2614586c7.png">

<img width="1225" alt="image" src="https://user-images.githubusercontent.com/43130622/161202593-f65c327f-7a3d-47df-af68-b849606c8acc.png">

7. Create a dataset to the lookup file uploaded earlier:

<img width="1792" alt="image" src="https://user-images.githubusercontent.com/43130622/161208237-3360453a-3548-40c5-b9c5-6ddae99b028d.png">

8. Create a source transformation an lookup transformation to lookup the 2 digit country code based on country.

<img width="1696" alt="image" src="https://user-images.githubusercontent.com/43130622/161209457-f156f604-d87b-4e06-8915-1532261f210a.png">

9. Create a source transformation to remove the unwanted columns.

10. Create a dataset to SQL database and point to the table.

<img width="663" alt="image" src="https://user-images.githubusercontent.com/43130622/161213348-78b170bb-4195-40d6-8377-b71931a4cf8f.png">

11. Check all the mappings are in sync and create the sinc.

<img width="994" alt="image" src="https://user-images.githubusercontent.com/43130622/161213721-d99feab9-d7a2-4079-ae50-e30f628051f2.png">

12. Add the dataflow to the existing pipleine and publish it after configuring it.

<img width="1429" alt="image" src="https://user-images.githubusercontent.com/43130622/161215897-32a03a94-c98c-489f-91f3-bf025feabfe6.png">

13. Run the pipeline and check whether the value is updated in SQL table.

<img width="1732" alt="image" src="https://user-images.githubusercontent.com/43130622/161219280-8e9fa218-a550-4e55-8916-ed144743b305.png">









 
















