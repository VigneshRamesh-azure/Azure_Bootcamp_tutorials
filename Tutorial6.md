# Tutorial 6

In this tutorial, you will create an IOT hub input source for Azure Stream analytics and create a stream analytics job to receive streaming data and store it in blob storage.


1. Create an IOT hub.

<img width="917" alt="image" src="https://user-images.githubusercontent.com/43130622/161384972-098519fc-9152-4af3-b841-f5bfe133825e.png">


2. Add a device to IOT hub and copy the connection string.

<img width="1347" alt="image" src="https://user-images.githubusercontent.com/43130622/161385487-7dfab20d-22ff-4d5e-ac36-6fddf2de5cff.png">


3. Create a container in the Azure storage account 

<img width="1785" alt="image" src="https://user-images.githubusercontent.com/43130622/161385588-fa4f2729-a228-48bd-92d2-ee8ad94bc107.png">

4. Create a stream analytics job

<img width="1088" alt="image" src="https://user-images.githubusercontent.com/43130622/161385692-060ad06c-afa1-4953-b8b2-4e5a58ac4a0b.png">


5. Add an input to the stream analytics job

<img width="1792" alt="image" src="https://user-images.githubusercontent.com/43130622/161385729-9a3a6018-693e-4eae-9f0a-b4fd99179203.png">

6. Configure job output

<img width="458" alt="image" src="https://user-images.githubusercontent.com/43130622/161385833-6341ca61-47d5-41f3-b00a-3b39ea20797c.png">


7. Define the transformation query to read the data from IoT Hub and copy it to a new file in the blob. Select Save.

<img width="1170" alt="image" src="https://user-images.githubusercontent.com/43130622/161385885-f58527b1-39a6-418b-8873-025898e927a8.png">


8. Run the IOT simulator by replacing the connection string of the IOD hub saved earlier.

https://azure-samples.github.io/raspberry-pi-web-simulator/

<img width="1790" alt="image" src="https://user-images.githubusercontent.com/43130622/161385981-a38db523-529d-4e93-b766-7b9fc68c9d90.png">

9. Start the stream analytics job.

<img width="1149" alt="image" src="https://user-images.githubusercontent.com/43130622/161386017-c20d5db0-8138-43af-b60e-f3b1d967c6cd.png">

10. Test the result and check the blob storage.

<img width="1214" alt="image" src="https://user-images.githubusercontent.com/43130622/161386125-fe301365-78cc-49cc-91c3-72ba7679bb57.png">

<img width="1544" alt="image" src="https://user-images.githubusercontent.com/43130622/161386179-c5a204ef-0ae6-4875-b060-77c94f67940d.png">

