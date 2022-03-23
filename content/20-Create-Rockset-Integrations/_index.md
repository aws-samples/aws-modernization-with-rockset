+++
title = "Create a Rockset integration"
chapter = true
weight = 20
autoNav = true
+++

## Create a Rockset integration & collection with AWS DynamoDB and S3
We have some transactional data in DynamoDB, and we also have a static CSV file in S3 that contains the car companies' detailed information.  Data from these sources will be stored in separate Rockset collections – 1 collection for DyanmoDB and another for S3. Once the Rockset collections are populated with data, we will write analytical queries that JOIN, aggregate, and search across these collections.
