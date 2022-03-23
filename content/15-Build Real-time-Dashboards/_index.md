+++
title = "Build Real-time Dashboards"
chapter = true
weight = 15
autoNav = true
+++

## Build Real-time Dashboards 

This part of the tutorial will walk you through building real-time dashboards using car transactional data, DynamoDB, Rockset, and Grafana. 

### Architectural Overview 

We’ll be simulating real-time transactional data that’ll be stored in DynamoDB. Our goal is to analyze that data on Rockset with SQL and then build a real-time dashboard with Grafana. Here’s what our architecture will look like:

<img src="../../images/Picture2.png" style="margin:15px 0px; border:1px solid black"/>


1. We’ll write a script that’ll periodically send transactional car data to DynamoDB. 
1. Separately, we’ll store static detailed information about the car companies in S3.
1. In the Rockset Query Editor, we’ll write complex analytical SQL queries that will JOIN and aggregate data from DynamoDB and S3.
1. Finally, we’ll create live dashboards on Grafana that’ll display the results from the queries.
