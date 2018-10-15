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


# Create a Shared folder in the SQL Server for Backup  

To create a **shared folder** in the SQL Server, proceed as follows:  

1. Login to the SQL Server with the credentials provided in the lab details page.  

2. **Create** a **New folder** in the desktop. **Right click** on the desktop and select **New** and then select **Folder** as shown below.   
<img src="/images/new folder create.png"/>  

3. **Right click** on the created folder and click on **Properties**.  
<img src="/images/right click properties.png"/>  

4. In the folder properties, click on **Security**. Now click on **Edit** as shown below.  
<img src="/images/folder permission edit.png"/>  

5. Now click on **Add**.  
<img src="/images/add permissions.png"/>  

6. Type **Everyone** and click on **Check Names**. Then click on **OK**.  
<img src="/images/add everyone.png"/>    

7. For **Everyone** **check** the box corresponding to **Full control**. Now click on **Apply** and then **OK**.  
<img src="/images/full control everyone.png"/>  

# Create a Managed Instance  
To create a managed instance proceed as follows:  
1. Login to azure using the provided credentials.  

2. Click on **+ Create a resource** and in the search bar type **Azure SQL Managed Instance**.  
<img src="/images/type mi.png"/>  

3. In the results that appear **select** the **Azure SQL Managed Instance**.  
<img src="/images/results mi.png"/>  

4. **Click** on the **Create** button.  
<img src="/images/create button mi.png"/>  

5. Enter the following details to proceed.  
    * **Subscription**: Choose the subscription.  
    * **Managed instance name**:  A unique name to be given to the managed instance.  
    * **Managed instance admin login**: demouser   
    * **Password**: demolabpassword1!  
    * **Resource group**: SQLServer-MI-DMS-Lab  
    * **Location**: East US  
    * **Virtual network**: vnet-milabdemo/ManagedInstance (Make sure you select the correct subnet. If you use any other subnet, the deployment may take up to 6hrs)    
    
    <img src="/images/managed instance.png"/>  

6. Now click on **Pricing Tier**. Cofigure the pricing tier as follows:  
    * Compute Generation: Gen4  
    * vCores: 8  
    * Storage: 32  
    
    Click on **Apply**.  
    
    <img src="/images/vcores for mi.png"/>  
    
7. After entering and verifying all the details, click on **Create**.  
<img src="/images/create mi final.png"/>    


# Configure connectivity between virtual networks  
In order to complete the migration successful, we need to ensure connectivity between the Virtual Network of the Managed Instance and the Virtual Network of the sql server(lab-sql-vm). Proceed as follows to establish vnet peering between the virtual networks.  

1. Navigate to  **Resource groups > SQLServer-MI-DMS-Lab > Overview > lab-vent**.     
<img src="/images/select lab-vnet image 1.png"/>  


# Create a migration project
To create a migration project proceed as follows:  
1. Login to azure using the provided credentials. 

2. Click on **Resource groups** and select the Resource group as shown below. 

<img src="/images/selecting rg.png"/>    

3. In the **Overview** blade of the Resource group, select the **Azure Database Migration Service**.  

<img src="/images/selecting the DMS.png"/>  

4. In the **Overview** blade of the DMS, **click** on the **+New Migration Project**.  

<img src="/images/new migration project.png"/>  

5. Enter the following details.  
    * Project name: **sql-mi-01**  
    * Source server type: **SQL Server**  
    * Target server type: **Azure SQL Database Managed Instance**  
    * Choose type of activity: **Offline data migration**  
    
    After entering details, click on **Create and run activity**    

<img src="/images/create and run migration project.png"/>  

6. Now the **Migration Wizard** window comes up.  

7. Click on **Select source** and enter the following details.  
    * Source SQL Service instance name: **Enter the DNS name of the lab-sql-vm**  
    * Authentication type: **Windows Authentication**  
    * Username: **lab-sql-vm\demouser**  
    * Password: **demopassword1!**  
    Make sure both the boxes under **Connection properties** are checked.
    
    Click on **Save**  
    
    <img src="/images/migration source details.png"/>   

8. Click on **Select target** and enter the following details.  
    * Target server name: **Enter the Host DNS of the Managed Instance**   
    * Authentication type: **SQL Authentication**  
    * Username: **demouser**  
    * Password: **demolabpassword1!**  
    
    Click on **Save**.  
    
    <img src="/images/select target details.png"/>    

9. Click on **Select databases** and check the box corresponding to **AdventureWorks2016CTP3**. Click on **Save**.  
<img src="/images/select databases.png"/>  

10. Click on **Select logins** and check the box near **SOURCE LOGINS**. Click on **Save**.  
<img src="/images/select logins.png"/>  

