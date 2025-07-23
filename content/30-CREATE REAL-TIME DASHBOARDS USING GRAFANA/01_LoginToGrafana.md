---
title: "Login to Grafana"
chapter: true
weight: 301
---

## Login to Grafana

<h4> 1. LOCATE THE USERNAME AND PASSWORD TO LOG IN TO GRAFANA </h4>

- On AWS, search for **EC2** and click on the first icon that pops up:

   <img src="../../images/Picture53.png" style="margin:15px 0px; border:1px solid black"/>

- Click on **Instances** on the left nav.   

- Check the box next to **EC2-Grafana-box** and click on **Connect** in the upper right-hand corner.
   
  <img src="../../images/Picture54.png" style="margin:15px 0px; border:1px solid black"/>

- Connect to the **Session Manager** so we can interact with the EC2 instance.  Finally, click on **Connect**:
  
  <img src="../../images/Picture55.png" style="margin:15px 0px; border:1px solid black"/>

- Once you connect to the instance, run the following script to get the username and password for Grafana. Please store these credentials somewhere. You’ll need them later:   

        grep admin_password /opt/bitnami/grafana/conf/grafana.ini


<h4> 2. INSTALL THE ROCKSET PLUGIN  </h4>
    
- Now we’ll edit the **[plugins]** section in the grafana.ini file. It’s important to note that this section is towards the bottom of the file. 
   
        sudo vim  /opt/bitnami/grafana/conf/grafana.ini
        
 - Scroll down to the **[plugins]** section. To edit the file, type i and type this below the **[plugins]** section (PLEASE, DO NOT COPY AND PASTE). Type:     

        allow_loading_unsigned_plugins = “rockset-backend-datasource” 
        
- To save the file, press the **escape** key and type: ```wq!```    
    
 <img src="../../images/Picture56.png" style="margin:15px 0px; border:1px solid black"/>  

  
- Run the following script to restart the server: 

         sudo systemctl restart bitnami 
         
- Open up the public IPv4 address with port 3000. MAKE SURE IT’S **HTTP**-.  i.e. http://xx.xxx.xxx.xxx:3000/login        
    
     <img src="../../images/Picture57.png" style="margin:15px 0px; border:1px solid black"/>
     
- It should pull up the homepage. Use the username and password you saved earlier:     

    <img src="../../images/Picture58.png" style="margin:15px 0px; border:1px solid black"/>
