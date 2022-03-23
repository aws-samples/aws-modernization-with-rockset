+++
title = "Hackathon"
chapter = true
weight = 40
autoNav = true
+++

## Mini Hackathon

For the second half of the workshop, you’ll extend what you built during the first half. This is an opportunity to explore the transactional data and build other types of real-time applications like real-time personalization or real-time leaderboards. You can also continue building out the real-time dashboard you started on Grafana.  

We’ll have multiple zoom breakout rooms and you’ll be randomly partnered with a few people for the remaining time. You can build any real-time application you want, use any 3rd-party SDKs or libraries, and so on. Be creative! Each team will have an opportunity to share their work at the end. The hosts will pop into break-out rooms to help.

If you're completing this workshop on your own time (i.e. you're not attending a live session), you can submit pictures of your results on the Rockset Community, under [Showcase](https://community.rockset.com/c/34-category/showcase/42) to receive feedback.

At the end of the hackathon, we’ll have some giveaways !!

## Prompts:

<h4> Prompt #1 </h4>

You’ll notice in the S3 dataset, companyId is a string datatype: 

<img src="../../images/Picture74.png" style="margin:15px 0px; border:1px solid black"/>  

Re-ingest the S3 file, apply SQL transformations, and write a SQL query that transforms companyId to an int type. Now, when we query companyId in the Query Editor, it’ll show up as an int:

<img src="../../images/Picture75.png" style="margin:15px 0px; border:1px solid black"/> 

<h4> Prompt #2 </h4>
Write an analytical SQL query that shows the most popular car color bought.

<h4> Prompt #3 </h4>
Write an analytical SQL query that shows which car was most clicked on.
Hint: you’ll need to use UNNEST.

<h4> Prompt #4 </h4>
Write an analytical SQL query that shows which companies and cars users clicked on.
Hint: you’ll need to write a common table expression


## Grafana Panels:

Build Grafana panels with the 3 analytical SQL queries you just wrote above (from Prompt #2 - #4) . Add it to the dashboard we created earlier from the workshop. 
Real-time app:

Once you’ve completed the 4 prompts and Grafana panels, build your own real-time app! You can continue building out the Grafana dashboard, or you can switch gears and build something completely different! 

- Real-time personalization: make recommendations based on what the user clicked and bought.
- Real-time leaderboard application: show the most popular car bought, companies who had the most transactions, and so on!  
- Continue building real-time dashboards with Grafana or experiment with Retool!


