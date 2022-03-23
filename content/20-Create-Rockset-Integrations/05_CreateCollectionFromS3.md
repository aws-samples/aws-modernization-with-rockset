---
title: "Creating Collection from S3 Integration"
chapter: true
weight: 205
---

##    CREATE A COLLECTION FROM THE S3 INTEGRATION ON ROCKSET

<h4> 1. CREATE A COLLECTION FROM THE S3 INTEGRATION ON ROCKSET</h4>

- This brings you to the integration page. Click on the upper right **Create Collection from Integration**:

  <img src="../../images/Picture40.png" style="margin:15px 0px; border:1px solid black"/>
 
 <h4> 2. GRAB THE S3 URI THAT CONTAINS THE CSV FILE </h4>

- Grab the S3 URI that contains the CSV file. Navigate back to the S3 service and click on the bucket that has this naming pattern: **rockset-data-lake-[AccountID]**:

  <img src="../../images/s3-bucket-name.png" style="margin:15px 0px; border:1px solid black"/>

 
- _Refer to the image below_: 
<br> a) Keep clicking down the path until you see **carCompanyInformation.csv** (see the top red box for the path)
<br> b) Copy the S3 URI (2nd red box on the right):

<img src="../../images/Picture41.png" style="margin:15px 0px; border:1px solid black"/>
     
 <h4> 3. PREVIEW AND CREATE THE S3 DATA COLLECTION ON ROCKSET</h4>

- Navigate back to Rockset. _Refer to the image below_: 
    <br> a) Name your collection **CarCompanies** (1st red box). 
    <br> b) Make sure you have the right integration [2nd red box]
    <br> c) Paste the S3 URI  from the previous step where you see **S3 PATH**- it should follow this naming pattern:  **s3://rockset-data-lake-[ACCOUNTID]/rocksetworkshopdata/carCompanyInformation.csv** (3rd red box
    <br> d) Choose the CSV/TSV file extension in the drop-down menu (4th red box)
    <br> e) You should see a preview of the data on the right, Source Preview
    <br> f) Click **Create** at the bottom left. Your collection should look like this:

<img src="../../images/Picture42.png" style="margin:15px 0px; border:1px solid black"/>

 <h4> 4. WAIT FOR THE COLLECTION TO GET CREATED</h4>

- Wait for Collection to be created.
 _Refer to the image below_:
    <br> a) Creating the collection may take a few minutes. Once the state reads **READY** (The 1st red box on the image below), you can write your first analytical query. 
   <br> b) Click **Query this Collection** (2nd red box on the image below) on the top right.
    
<img src="../../images/Picture43.png" style="margin:15px 0px; border:1px solid black"/>




  
