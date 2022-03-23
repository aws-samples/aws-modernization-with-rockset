---
title: "Creating Field Mappings"
chapter: true
weight: 203
---

## Creating Field Mappings

We’ll be doing 3  different types of field mappings: 

<h4> 1. CONVERT A DATE THAT COMES IN AS A STRING INTO A TIMESTAMP </h4>

We can convert the date that comes in as a string into a timestamp data type  by using **PARSE_DATETIME_ISO8601**. You can learn more here in this [Rockset Community post](https://community.rockset.com/t/taking-a-date-time-that-comes-as-a-string-converting-it-to-a-timestamp-obj/573). When you’re done, your SQL transformations should be written  like this:

    SELECT PARSE_DATETIME_ISO8601(_input.timeiso8601) AT TIME ZONE 'America/Los_Angeles' as _event_time
    FROM _input

You’ll notice that at the bottom, you’ll see the results of the SQL transformation as ```_event_time```:

 <img src="../../images/Picture26.png" style="margin:15px 0px; border:1px solid black"/>
 
 <b>Note</b> that we'll be iterating on this SQL query throughout this section. _Don't click_ **Apply** until the end. 

 
<h4> 2. CONVERT PRICE THAT COMES IN AS A STRING INTO A FLOAT </h4>

This <a href="https://community.rockset.com/t/convert-price-that-comes-in-as-a-string-into-a-float/636">Rockset Community post</a>  covers how to convert a price that comes in as a string into a float. 

When you’re done, the SQL transformations in the editor should be written like this. Please note that the below includes the previous transformation:

    SELECT PARSE_DATETIME_ISO8601(_input.timeiso8601) AT TIME ZONE 'America/Los_Angeles' as _event_time, try_cast(REGEXP_REPLACE(_input.payment.price, '[^\d.]') as float) as price_float
    FROM _input

You’ll notice the final results have both  ```_event_time_```  and **price_float**:

<h4> 3. CONVERT THE CREDIT CARD NUMBER INTO A HASH </h4>

Rockset supports PHI/PII masking, which stores only the hashed value and not the original value. This [Rockset Community post](https://community.rockset.com/t/sql-transformation-pii-phi-masking/638) covers PHI/PII masking. To convert the credit card number into a hash, copy the below, which again is inclusive of the above transformations:

    SELECT PARSE_DATETIME_ISO8601(_input.timeiso8601) AT TIME ZONE 'America/Los_Angeles' as _event_time, try_cast(REGEXP_REPLACE(_input.payment.price, '[^\d.]') as float) as price_float, TO_HEX(SHA256(_input.payment.credit_card_number)) as credit_card_number FROM _input


<h4> 4. FINAL COMBINED TRANSFORMATION QUERY </h4>


When we incorporate the fields that don’t need transformation, our final SQL transformation query will look like this: 
 
    SELECT try_cast(REGEXP_REPLACE(_input.payment.price, '[^\d.]') as float) as price_float, PARSE_DATETIME_ISO8601(_input.timeiso8601) AT TIME ZONE 'America/Los_Angeles' as _event_time, car, company_id, id, ip_address, _input.items_clicked_on, person,TO_HEX(SHA256(_input.payment.credit_card_number)) as credit_card_number, _input.payment.discount, _input.payment.credit_card_type
    FROM _input

 Once you’re done, **Apply** the transformation:
 
  <img src="../../images/Picture27.png" style="margin:15px 0px; border:1px solid black"/>
  
  From there, **Create** the collection: 
  
   <img src="../../images/Picture28.png" style="margin:15px 0px; border:1px solid black"/>
