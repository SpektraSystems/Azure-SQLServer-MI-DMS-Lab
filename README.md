# Azure-SQLServer-MI-DMS-Lab
Migrate SQL Server to Managed Instances

<!-- TOC -->
1. [Lab Registeration experience](#lab-registeration-experience)  
2. [Accessing the pre-deployed envrionment](#pre-deployed-envrionment)  
3. [Create a migration project](#create-a-migration-project)          

<!-- /TOC -->

# Lab Registeration Experience  

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


# Accessing the pre-deployed envrionment  
To login in to the pre-deployed environment proceed as follows:  

1. From the **ODL details** page copy the username and password.  
<img src="/images/username and password odl.png"/>    


2. Login to Azure by using the provided credentials. To login to azure go to [portal.azure.com](https://portal.azure.com/)  

3. The details of the SQL Server VM is also provided in the Lab details page.  
<img src="/images/sql server details.png"/>      


# Configuring Shared folder in the SQL Server for Backup  

Duration: 20 mins  

To configure the **shared folder** in the SQL Server, proceed as follows:  

1. Login to the SQL Server with the credentials provided in the lab details page.  

2. Create a new folder on the desktop named **backup**.  

3. **Right click** on the folder named **backup** and click on **Properties**.  
<img src="/images/right click properties.png"/>  

4. In the folder properties, click on **Security**. Now click on **Edit** as shown below.  
<img src="/images/folder permission edit.png"/>  

5. Now click on **Add**.  
<img src="/images/add permissions.png"/>  

6. Type **Everyone** and click on **Check Names**. Then click on **OK**.  
<img src="/images/add everyone.png"/>    

7. For **Everyone** **check** the box corresponding to **Full control**. Now click on **Apply** and then **OK**.  
<img src="/images/full control everyone.png"/>  

8. To share the folder proceed as follows.  

9. In the folder properties, click on **Sharing**. Now click on **Share** as shown below.  
<img src="/images/sharing backup folder.png"/>  

10. Click on the **Share** button as shown below.   
<img src="/images/sharing backup folder to demouser.png"/>  

11. Click on **Done**.  
<img src="/images/backup_done_1.png"/>    



# Create a migration project  

Duration: 30 mins  

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
    * Authentication type: **SQL Authentication**  
    * Username: **dbuser** (dbuser is a pre created user which has all the required permissions to perform the migration)  
    * Password: **demolabpassword1!**  
    Make sure both the boxes under **Connection properties** are checked.
    
    Click on **Save**  
    
    <img src="/images/sql authentication source details.png"/>   

8. Click on **Select target** and enter the following details.  
    * Target server name: **Enter the Host DNS of the Managed Instance**   
    * Authentication type: **SQL Authentication**  
    * Username: **demouser**  
    * Password: **demolabpassword1!**  
    
    Click on **Save**.  
    
    <img src="/images/select target details.png"/>    

9. Click on **Select databases** and check the box corresponding to **WideWorldImporters**. Click on **Save**.  
<img src="/images/world_wide_importers.png"/>  

10. Click on **Select logins** and check the box near **SOURCE LOGINS**. Click on **Save**.  
<img src="/images/selecting logins.png"/>    

11. Click on **Configure migration settings** and enter the following details.  
    * Choose source backup options: **I will let Azure Database Migration Service create backup files**.  
    * Network share location that Azure Database Migration Service can take database backups to: **\\192.168.0.4\backup**  
    * Windows User Azure Database Migration Service impersonates to upload files to Azure Storage: **lab-sql-vm\<username>**  
    * Password: **enter your password**  
    * SAS URI for Azure Storage contianer that Azure Database Migration Service will upload the files to: **Enter the SAS URI of the storage account**  
    
    Click on **Save**.  

<img src="/images/configure migration settings.png"/>  

12. Now enter the following details.  
    * Activity Name: **migration-activiy**  
    * Validation option: **Do not validate**  
    
    Now click on **Run migration**  
    
    <img src="/images/migration summary.png"/>  

## After the hands-on lab

Duration: 10 mins

In this exercise, you will delete any Azure resources that were created in support of the lab. You should follow all steps provided after attending the Hands-on lab to ensure your account does not continue to be charged for lab resources.

### Task 1: Delete the resource group

1. Using the [Azure portal](https://portal.azure.com), navigate to the Resource group you used throughout this hands-on lab by selecting Resource groups in the left menu.

2. Search for the name of your research group, and select it from the list.

3. Select Delete in the command bar, and confirm the deletion by re-typing the Resource group name, and selecting Delete.

You should follow all steps provided *after* attending the Hands-on lab.
    
