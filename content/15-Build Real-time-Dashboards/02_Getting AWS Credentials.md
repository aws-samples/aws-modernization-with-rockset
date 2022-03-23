---
title: "Getting AWS Credentials"
chapter: true
weight: 152
---


 
## Get AWS Credentials from CloudShell

1. Navigate to [CloudShell](https://us-east-1.console.aws.amazon.com/cloudshell/home?region=us-east-1#) by clicking the link, or you can also search for it on the AWS search bar: 

<img src="../../images/cloud9.png" style="margin:15px 0px; border:1px solid black"/>

2. Type this in the shell: `aws iam create-access-key --user-name rockset-user`:

<img src="../../images/Picture4.png" style="margin:15px 0px; border:1px solid black"/>

3. Save the JSON in the output window. You’ll need it for future step. 


