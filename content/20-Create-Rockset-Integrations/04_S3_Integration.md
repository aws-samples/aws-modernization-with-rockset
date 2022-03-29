---
title: "S3 Integration"
chapter: true
weight: 204
---

## Create S3 Integration

_While the_ _**CarPurchases**_ _collection is being populated with the DynamoDB data_, let’s now create a second integration with AWS S3. We will load a Rockset’s Collection with the CSV data from S3. This will allow us to write a JOIN query that combines the car company information with the data from DynamoDB.  


<h4> 1. CREATE AN S3 INTEGRATION</h4>

- Navigate to the left panel and click on <b>Integration</b>. From there, click on <b>Add Integration</b>:

    <img src="../../images/Picture29.png" style="margin:15px 0px; border:1px solid black"/>

<h4> 2. USE THE AWS S3 DATA CONNECTOR</h4>

- Click on the AWS S3 data connector and click on **Start**:

<img src="../../images/Picture30.png" style="margin:15px 0px; border:1px solid black"/>
    
<h4> 3. GIVE YOUR INTEGRATION A NAME</h4>

- Name your integration **CarCompanyInformation**.

    <img src="../../images/Picture31.png" style="margin:15px 0px; border:1px solid black"/>

    
<h4> 4. CREATE AN AWS IAM POLICY</h4>

- Copy the bucket name that contains the CSV data from the <a href="https://s3.console.aws.amazon.com/s3/home?region=us-east-1">S3 service</a> . We’re going to use it in the following step. It’ll have this naming pattern: <b>rockset-data-lake-[AccountID]</b>. The **AccountID** will be a different value for every participant:

<img src="../../images/s3-bucket-name.png" style="margin:15px 0px; border:1px solid black"/> 

- Navigate to the [AWS IAM Policy](https://us-east-1.console.aws.amazon.com/iamv2/home#/policies) section and click on **Create Policy**:

    <img src="../../images/Picture32.png" style="margin:15px 0px; border:1px solid black"/>
    
- Go ahead and override the JSON tab with this JSON snippet:

           {
               "Version": "2012-10-17",
               "Statement": [
                 {
                   "Effect": "Allow",
                   "Action": [
                     "s3:List*",
                     "s3:GetObject"
                   ],
                   "Resource": [
                     "arn:aws:s3:::rocksetawsworkshop",
                     "arn:aws:s3:::rocksetawsworkshop*"
                   ]
                 }
               ]
             }
             
             
       It should look like this:
   
       <img src="../../images/Picture33.png" style="margin:15px 0px; border:1px solid black"/>
   

- When you’re done, click on **Next: Tags**.
- Immediately, click on **Next: Review**.
- Set the policy name to <b>RocksetS3Policy</b> and then click **Create policy**:  

 <img src="../../images/s3policy-8.png" style="margin:15px 0px; border:1px solid black"/>


<h4> 5. CREATE AN AWS IAM ROLE</h4>  

- Switch back to AWS and navigate to the [AWS IAM Role](https://us-east-1.console.aws.amazon.com/iamv2/home#/roles). Click **Roles** on the left-nav. From there, click **Create role**:   
    
 <img src="../../images/create-role.png" style="margin:15px 0px; border:1px solid black"/>
  

- Switch over to the Rockset Console and copy the **Rockset Account ID** and **external ID** on the Rockset DynamoDB Integration page:

<img src="../../images/Picture35.png" style="margin:15px 0px; border:1px solid black"/>

- _Refer to the image below_:
 <br> a) The next section on the integration page is for creating the AWS IAM Role.  Click on the **AWS account** box (2nd red box). 
<br> b) Then click on **Another AWS account** (which is the 3rd red box). 
<br> c) Put the **Rockset Account ID** from the Rockset S3 integration page in the text box. 
<br> d) In the Options section, check the  **Require external ID** box. 
<br> e) Paste the **external ID** from the Rockset S3 integration page in the text box (4th red box). 
<br> f) Click **Next** on the bottom right of this page.

<img src="../../images/Picture34.png" style="margin:15px 0px; border:1px solid black"/>
 
- To find the policy we just created in step 4, type **RocksetS3Policy** in the search bar. Click the policy to attach it to the role. Afterward, click **Next**:


<img src="../../images/create-s3-role-9.png" style="margin:15px 0px; border:1px solid black"/>


- Name the role **RocksetS3Role**. On the bottom right, click on **Create role**:

<img src="../../images/finalize-s3-role-10.png" style="margin:15px 0px; border:1px solid black"/>

<h4> 6. RETRIEVING THE ROLE ARN</h4>
   
- Navigate back to the **Roles**, and search for the role you just created, **RocksetS3Role**. Click on the role link:

<img src="../../images/find-s3-role-11.png" style="margin:15px 0px; border:1px solid black"/>

- Copy the Role ARN from AWS:

<img src="../../images/copys3arn-14-redo.png" style="margin:15px 0px; border:1px solid black"/>

- Navigate back to Rockset and paste the ARN Role in **Role ARN** on Rockset and click **Save Integration**:

<img src="../../images/save-s3integration-15-redo.png" style="margin:15px 0px; border:1px solid black"/>

