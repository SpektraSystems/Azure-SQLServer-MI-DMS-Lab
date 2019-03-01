# Azure-SQLServer-MI-DMS-Lab
Migrating SQL Server to Managed Instances

<!-- TOC -->  
- SQL Database Managed Instance Lab  
  - [Overview](#overview)  
  - [Abstract and learning objectives](#abstract-and-learning-objectives)  
  - [Lab Registeration experience](#lab-registeration-experience)  
  - [Exercise 1: Exploring the SQL Managed Instance and the associated resources](#excercise-1-exploring-the-sql-managed-instance-and-the-associated-resources)  
  - [Exercise 2: Accessing the pre-deployed envrionment](#excercise-2-accessing-the-pre-deployed-envrionment)  
  - [Exercise 3: Configuring Shared folder in the SQL Server for Backup](#exercise-3-configuring-shared-folder-in-the-sql-server-for-backup)    
  - [Exercise 4: Create a migration project](#exercise-4-create-a-migration-project)          
  - [Exercise 5: Verifying the successful migration of Databases](exercise-5-verifying-the-successful-migration-of-databases)  
  - [After the hands-on lab](#after-the-hands-on-lab)  
    - [Task 1: Delete the resource group](#task-1-delete-the-resource-group)

<!-- /TOC -->  

# Overview

Managed instance is a deployment option of Azure SQL Database, providing near 100% compatibility with the latest SQL Server on-premises (Enterprise Edition) Database Engine, providing a native virtual network (VNet) implementation that addresses common security concerns, and a business model favorable for on-premises SQL Server customers. The managed instance deployment model allows existing SQL Server customers to lift and shift their on-premises applications to the cloud with minimal application and database changes. At the same time, the managed instance deployment option preserves all PaaS capabilities (automatic patching and version updates, automated backups, high-availability ), that drastically reduces management overhead and TCO.  

<img src="/images/what is sql mi.png"/>  

# Abstract and learning objectives  

This hands-on lab is designed to provide exposure to Azure SQL Managed Instance and migration exisitng on premises Databases to SQL Managed Instance.In this lab, you migrate the WorldWideImporters database from an on-premises instance of SQL Server to an Azure SQL Database managed instance by using the Azure Database Migration Service.


By the end of the lab, you will be able to migrate a SQL Database from a SQL Server to an Azure SQL Managed Instance using Data Migration Service.

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

# Excercise 1: Exploring the SQL Managed Instance and the associated resources    

For a Managed Instance to perfrom desirably over a virtual netwotk, there some preparations to be done such as setting up route tables, setting up the Network Security Group with the required set of rules. The Managed Instance will itself take care of all the necessary actions and preparations that are necessary for its smooth operation.To explore SQL Managed instances and the associated resources proceed as follows.  

1. Navigate to the **SQLMI-VNET-RG** in which the Managed Instance and the associated resources are deployed.  

2. Select the **route table** as shown below.  

<img src="/images/route-table-click.png"/>  

3. Click on **Routes** to see all the entries to route the traffic related to the Managed Instance will be displayed.  

<img src="/images/routes-route-table.png"/>  

4. After reviewing the Route Table, navigate to the **Network Security Group** as shown below.  

<img src="/images/select-nsg.png"/>

5. In the **Overview** section under **Settings**, click on **Inbound security rules** view all the inbound security rules created.  

<img src="/images/see-inbound-rules.png"/>  

6. Similarly Navigate to the **Outbound security rules** to view the Outbound security rules.  

<img src="/images/see-outbound-rules.png"/>  

7. After reviewing the Network Security Group, navigate to the **SQL Managed Instance** as shown in the image below.  

8. In the **Overview** section of the SQL Managed Instance, all the information will be displayed. **Copy** the value of the **Host** as shown below. This will be needed in the further exercises.  



# Excercise 2: Accessing the pre-deployed envrionment  
To login in to the pre-deployed environment proceed as follows:  

1. From the **ODL details** page copy the username and password.  
<img src="/images/username and password odl.png"/>    


2. Login to Azure by using the provided credentials. To login to azure go to [portal.azure.com](https://portal.azure.com/)  

3. The details of the SQL Server VM is also provided in the Lab details page.  
<img src="/images/sql server details.png"/>      


# Exercise 3: Configuring Shared folder in the SQL Server for Backup  

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



# Exercise 4: Create a migration project  

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
    
13. After the migration completes, select **Download report** to get a report listing the details associated with the migration process.  

# Exercise 5: Verifying the successful migration of Databases  

To verify whether the migration of the databases were successfull, proceed as follows:  

1. Navigate to the **lab-jump-vm** and start a RDP session.  

2. Click on the **Start** button to open the start menu. Expand **Microsoft SQL Server Tools 17** and open **Microsoft SQL Server Management Studio.**    

<img src="/images/select sql mgmt studio.png"/>  

3. When the login page appears, enter the following details:  
  * Server Type: Database engine    
  * Server Name: *Enter the ip address of the Managed Instance**  
  * Authentication: SQL Server Authentication  
  * Login: demouser  
  * Password: demolabpassword1!  
  
  After entering the details click on **Connect**.  

<img src="/images/connect to sqlmi via ssms.png"/>   

4. On the **Object Explorer**, expand **Databases** and you can see the database that is migrated.  

<img src="/images/world-wide-imp-check.png"/>  

## After the hands-on lab

Duration: 10 mins

In this exercise, you will delete any Azure resources that were created in support of the lab. You should follow all steps provided after attending the Hands-on lab to ensure your account does not continue to be charged for lab resources.

### Task 1: Delete the resource group

1. Using the [Azure portal](https://portal.azure.com), navigate to the Resource group you used throughout this hands-on lab by selecting Resource groups in the left menu.

2. Search for the name of your research group, and select it from the list.

3. Select Delete in the command bar, and confirm the deletion by re-typing the Resource group name, and selecting Delete.

You should follow all steps provided *after* attending the Hands-on lab.
    
