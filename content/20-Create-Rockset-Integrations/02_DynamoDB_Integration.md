---
title: "Create DynamoDB Integration"
chapter: true
weight: 202
---

## CREATE A ROCKSET COLLECTION WITH DATA FROM DYNAMODB

Rockset has a managed DynamoDB connector that bulk loads data into a Rockset collection. After the bulk load is complete,  Rockset continuously syncs data whenever there is a change in the DynamoDB table through DynamoDB’s Stream API.  As soon as there is a change in the **rockset_carpurchases** table, Rockset reflects that change within seconds. This is because Rockset leverages Change Data Capture (CDC) streams. 

<h4> 1. CREATE A ROCKSET ACCOUNT AND DYNAMODB INTEGRATION </h4>

- Go to the [Rockset Console](https://console.rockset.com/) →  click on the **Integration** tab on the left nav and then click on the button **Create your first integration**:
         <img src="../../images/Picture7.png" style="margin:15px 0px; border:1px solid black"/>
         
<h4> 2. SELECT THE AMAZON DYNAMODB DATA SOURCE </h4>

- Click on the DynamoDB data connector and **Start**:
     
      <img src="../../images/Picture8.png" style="margin:15px 0px; border:1px solid black"/>
      
<h4> 3. FILL IN THE INTEGRATION NAME </h4>
      
- Create an integration called **DDBCarPurchasesIntegration**. 
      
       <img src="../../images/Picture9.png" style="margin:15px 0px; border:1px solid black"/>
       
<h4> 4. CREATE AN AWS IAM POLICY</h4>

-  Navigate to [AWS IAM services](https://us-east-1.console.aws.amazon.com/iamv2/home#/home) and click on the **Policies** tab. Click on the **Create Policy** button:


<img src="../../images/Picture10.png" style="margin:15px 0px; border:1px solid black"/>
        
- Grab the empty S3 bucket name from the [S3 service](https://s3.console.aws.amazon.com/s3/home?region=us-east-1). It’ll have this naming pattern: <b>rockset-data-integration-[AccountID]</b>.The **AccountID** will be a different value for every participant:    

  <img src="../../images/Picture11.png" style="margin:15px 0px; border:1px solid black"/>
     
- When you create the AWS IAM Policy for DynamoDB, you must replace the S3 bucket name’s **AccountID** with the value you have.

- Overwrite and paste the below in the JSON tab (don’t forget to update the S3 bucket name in the JSON below):

            {
                 "Version": "2012-10-17",
                 "Statement": [
                   {
                     "Effect": "Allow",
                     "Action": [
                       "dynamodb:GetShardIterator",
                       "dynamodb:Scan",
                       "dynamodb:DescribeStream",
                       "dynamodb:DescribeExport",
                       "dynamodb:GetRecords",
                       "dynamodb:DescribeTable",
                       "dynamodb:DescribeContinuousBackups",
                       "dynamodb:ExportTableToPointInTime",
                       "dynamodb:UpdateTable",
                       "dynamodb:UpdateContinuousBackups",
                       "s3:PutObject",
                       "s3:GetObject",
                       "s3:ListBucket"
                   ],
                   "Resource": [
                       "arn:aws:dynamodb:*:*:table/rockset_carpurchases",
                       "arn:aws:dynamodb:*:*:table/rockset_carpurchases/stream/*",
                       "arn:aws:dynamodb:*:*:table/rockset_carpurchases/export/*",
                       "arn:aws:s3:::bucketname",
                       "arn:aws:s3:::bucketname/*"
                   ]
                   }
                 ]
               }


- It should look like this:

   <img src="../../images/Picture12.png" style="margin:15px 0px; border:1px solid black"/>
    
  - When you’re done, go ahead and click on **Next: Tags** 
 
 - Immediately click on **Next: Review**.  
  
 - Give the policy name as **RocksetDynamoDBPolicy**. Then, click on **Create policy**:
   
   <img src="../../images/Picture13.png" style="margin:15px 0px; border:1px solid black"/>
   
   
<h4> 5. FILL IN S3 BUCKET INFORMATION ON ROCKSET</h4>

- Enter the S3 Bucket information on Rockset using the following naming convention: **rockset-data-integration-[AccountID]**. Replace the **[AccountID]** with the value you see in the bucket name. 

      
   <img src="../../images/Picture14.png" style="margin:15px 0px; border:1px solid black"/>
   
<h4> 6. CREATE AN AWS IAM ROLE</h4>
 
 - Navigate to the <a href="https://us-east-1.console.aws.amazon.com/iamv2/home#/roles">AWS IAM services</a> and click on the **role** on the left-nav bar. From there, click on **Create role**: 
   
   <img src="../../images/Picture15.png" style="margin:15px 0px; border:1px solid black"/>
   
   - Switch to <b>Rockset Console</b> and grab the **Rockset Account ID** and **external ID** on the Rockset DynamoDB Integration page
   
   <img src="../../images/Picture16.png" style="margin:15px 0px; border:1px solid black"/>
      
   - _Refer to the image below_: 
    <br> a) Switch back to the [AWS Role](https://us-east-1.console.aws.amazon.com/iamv2/home#/roles) page and click on the **AWS account box** (2nd red box image). 
    <br> b) From there, you are going to click on **Another AWS account** (3rd red box image).
    <br> c)Paste the **Rockset Account ID**. 
    <br> d) Under Options, check the **Require external ID** box. Paste the **external ID** you see on the Rockset DynamoDB integration page in the text box here (4th red box image). 
    <br> e) Afterward, click **Next** on the bottom right.
    
   <img src="../../images/Picture17.png" style="margin:15px 0px; border:1px solid black"/>
    
    
   - To find the policy we just created in step 4, go ahead and type the policy name in the search bar— **RocksetDynamoDBPolicy**. Be sure to click the policy so you can attach it to the role. Afterward, click on **Next**.  
     
   <img src="../../images/Picture18.png" style="margin:15px 0px; border:1px solid black"/>
      
   -  Give the Role Name: **RocksetDynamoDBRole**. On the bottom right, click on **Create role**:   
   
   <img src="../../images/Picture19.png" style="margin:15px 0px; border:1px solid black"/>
    
    
<h4> 7. RETRIEVING THE ROLE ARN </h4>
 
- Navigate back to the role, and search for the role you created, **RocksetDynamoDBRole**. From there, click on the role:
     
   <img src="../../images/Picture20.png" style="margin:15px 0px; border:1px solid black"/>
      
- Grab the Role ARN on the AWS side and paste on the Rockset Integration section:
    
   <img src="../../images/Picture21.png" style="margin:15px 0px; border:1px solid black"/>
     
- Navigate back to the Rockset DynamoDB Integration page and paste the ARN Role value under **Role ARN** and **Save Integration**:
    
   <img src="../../images/Picture22.png" style="margin:15px 0px; border:1px solid black"/>
       
 <h4> 8. CREATE A COLLECTION FROM THE DYNAMODB INTEGRATION</h4>
       
- You’ll be brought back to the integration page. Click on the upper right **Create Collection from Integration**:   
       
<img src="../../images/Picture23.png" style="margin:15px 0px; border:1px solid black"/>
        
- _Refer to the image below_: 
     <br> a)Go ahead and give your collection the name **CarPurchases**. 
     <br> b)From there go ahead and put the table name, **rockset_carpurchases** 
     <br> c) The region should be **us-east-1**. 
     <br> d) You should see a preview of the data on the right. 
     <br><br>Your collection should look like this:
     
    <img src="../../images/Picture24.png" style="margin:15px 0px; border:1px solid black"/>
      
- Towards the bottom at **Configure Ingest**, we have an opportunity to do query-based field mappings, also known as QBFMs. This is where we can massage the data as it’s being ingested into Rockset. QBFMs allow you to do SQL-based field mappings. This saves on storage and compute at query time (also known as run time). Click on **Configure SQL rollups and/or transformations**:   
   
    <img src="../../images/Picture25.png" style="margin:15px 0px; border:1px solid black"/>
