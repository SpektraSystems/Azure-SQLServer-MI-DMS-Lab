# Azure-SQLServer-MI-DMS-Lab
Migrate SQL Server to Managed Instances

<!-- TOC -->
1. [AEC Registeration experience](#aec-registeration-experience)  
2. [Pre-deployed envrionment](#pre-deployed-envrionment)  
3. [](#register-and-activate-sophos-trial)    
4. [](#verify-iis-website-working)    
5. [](#remove-public-ip-from-windows-vm)      
6. [](#configure-web-application-firewall-in-sophos-and-public-the-iis-Website-via-xg)      

<!-- /TOC -->

# AEC Registeration Experience  

1. Navigate to the URL provided to sign-up for the lab.  

2. Enter the following details:  
   * **First Name**  
   * **Last Name**  
   * **Work email**  
   * **Organization**  
   * **Country**  
   
   After entering the details click on **SUBMIT**.  
   
<img src="/images/AEC registeration.png"/>  

3. After entering the details, **click** on the **LAUNCH LAB** button to proceed further.      

<img src="/images/launch lab button.png"/>  


# Pre-deployed envrionment  
To login in to the pre-deployed environment proceed as follows:  

1. From the **ODL details** page copy the username and password.  
<img src="/images/username and password odl.png"/>    


2. Login to Azure by using the provided credentials. To login to azure go to [portal.azure.com](https://portal.azure.com/)  


# Create a Managed Instance  
To create a managed instance proceed as follows:  
1. Login to azure using the provided credentials.  

2. Click on **+ Create a resource** and in the search bar type **Azure SQL Managed Instance**.  
<img src="/images/type mi.png"/>  


# Create a migration project
To create a migration project proceed as follows:  
1. Login to azure using the provided credentials. 

2. Click on **Resource groups** and select the Resource group as shown below. 

<img src="/images/selecting rg.png"/>    

3. In the **Overview** blade of the Resource group, select the **Azure Database Migration Service**.  

<img src="/images/selecting the DMS.png"/>  

4. In the **Overview** blade of the DMS, **click** on the **+New Migration Project**.  

<img src="/images/new migration project.png"/>  
