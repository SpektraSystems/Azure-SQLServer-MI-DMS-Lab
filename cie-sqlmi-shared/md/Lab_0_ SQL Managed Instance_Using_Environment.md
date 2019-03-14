Using Azure SQL MI Pre-Configured Environment

March 2019

Introduction
------------

This lab walks you through how to use the pre-deployed environment for SQL
Managed Instance Lab.

SQL Managed Instance Environment
================================

Exercise 0: Using Pre-configured Environment
--------------------------------------------

### Overview

In this exercise, you will create a source environment.

#### Task 1: Sign Up for pre-configured environment

1.  Navigate to bit.ly link which was provided by instructor and register by
    providing all required information and then click on **SUBMIT** button.  
    

    ![https://github.com/SpektraSystems/Azure-MySQL-DMS-Lab/raw/master/images/sign2.jpg](media/09da56d37f6dc05b5397770546454196.jpg)

2.  Once registration is accepted, you will be automatically redirected to the
    lab activation page. Now, it is advised to save a copy of the URL on the
    browser, which has the activation id. **Click** on the **Launch
    Lab** button.  
    

    ![](media/561adcec8a936b4762cbaa881a6c797e.png)

3.  You will see the environment details soon as shown below:  
    

    ![](media/9ead8797a08cd791242127476a9a5a9a.png)

Exercise 1: Login to Azure Portal
---------------------------------

### Overview

In this exercise, you will connect to your Azure Portal and verify the
Pre-deployed Resource group’s.

#### Task 1: Connect to Azure Portal

1.  Launch a browser and navigate to <https://portal.azure.com>. Once prompted,
    login with the Azure Credentials from the Lab Details Page.  
    

    ![](media/d2474eb335a8b12fdd7b2d66ec1fbfba.png)

2.  In the Stay signed in? pop-up window, click No

3.  In the Welcome to Microsoft Azure pop-up window, click Maybe Later

    Note: If you receive a pop-up for Azure Advisor, click the X in the top
    right corner of the pop-up to close it.

4.  You will be directed to the dashboard.

5.  From the left side of the Page, select Resource Groups

6.  Note that you will have access to three Resource groups:  
    

    ![](media/800d641edaf36d54770b8f0a6b1956fc.png)

7.  Please note down the location of the Resource groups:

    ![](media/dc7177db460cf8eadb1eeee12a0b6736.png)

8.  Here is the use of each resource group

9.  **sqlmi-mi-data-services-XXXXX:** This resource group contains Azure
    Database Migration Service and Azure Database Factory.

10. **sqlmi-onpremises-XXXXX:** This resource group contains a SQL Server
    Virtual Machine named **lab-sql-vm** pre-configured with SQL Server 2008 and
    loaded with sample AdventureWorksDB

11. **SQLMI-Shared-RG:** This resource group contains pre-provisioned SQL
    Managed Instance to be used during the lab. This resource group is shared
    among all participants.

**Consideration during Lab:**

1.  You’ll not be able to create any new resource group. Please use existing
    resource groups.

2.  You’ll not need to create SQL Managed Instance or any of its requirements
    such as virtual network etc.

3.  Always refer to DNS name of your lab virtual machines and Managed Instance
    using the lab details page or using Azure Portal. DNS names given in lab
    guides are for reference purpose and needs to be replaced with actual values
    during lab.
