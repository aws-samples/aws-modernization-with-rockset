---
title: "About Rockset"
chapter: true
weight: 101
---

## Rockset Pairs with DynamoDB for Complex Analytics
While DynamoDB is great for real-timef transactions, it can be paired with Rockset for analytical workloads, like complex aggregations and JOINs. Rockset is a real-time analytics database that’s able to ingest data with a data freshness of 1 - 2 seconds and execute heavy analytical SQL queries that JOINs,  aggregates, and searches in milliseconds. When data is ingested from DynamoDB,  it’s indexed via Rockset’s Converged Index™, so terabytes of deeply nested data are returned in under a second. Rockset’s Converged Index™indexes all fields in the document via 3 different ways: a row index, columnar index, and an inverted index.  Rockset also supports real-time updates, inserts, and deletes.  

Below is an architecture diagram of what sources you can integrate with Rockset to write and execute queries that  Search, JOIN, and aggregate. Once the queries are executed on Rockset, you can power real-time applications, like leaderboards, dashboards, personalization, and much more within seconds:

 <img src="../../images/Picture1.png" style="margin:15px 0px; border:1px solid black"/>