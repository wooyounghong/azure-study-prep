# Chapter 1: Implement Websites

- Microsoft Azure Websites = fully managed platform-as-a-services (PaaS)
  - enables:
    - build, deploy, scale enterprise-grade web apps in seconds

# 1.1 Deploy Websites

    ***Objectives***
      - Create Azure Website
      - Define deployment slots
      - Publish an application
      - Swap Deployment Slots
      - Define and deploy WebJobs

      ## Create Azure Website
        - creates unique DNS name (specifying the region the website will run, adds additional resources such as Microsoft Azure SQL Database or Microsoft Azure Storage Account)
        - Can be created with following tools:
          - Microsoft Azure management portal
          - Azure PowerShell cmdlets
            - What is Azure Powershell?
              * command-line tool that is more powerful
              * Azure PowerShell programmers use preset scripts called cmdlets to perform tasks such as...
                - provisioning virtual machines (VMs)
                - creating cloud services
          - Other UI and command-line tools

      ## Defining Deployment Slots
        - Every Azure websites include one deployment slot (production deployment slot) by default where production version of your app will be deployed
        - Option to add four additional deployment slots
          ** Example of deployment slots
            1. Dev
            2. Test
            3. QA
            4. Staging - example: https://jokes-web-staging.azurewebsites.net
            5. Production - default example: https://jokes-web.azurewebsites.net
      ## Swapping Deployment Slots
        - Swapping contents of slots:
          example: switching Staging Slot with Production Slot
            * Use Azure management portal to make the swap
            * PowerShell
              - example: `$wsStaging = 'Staging'
                         $wsProduction = 'Production'
                         Switch-AzureWebsiteSlot -Name $wsName -Slot1 $wsStaging -Slot2 $wsProduction`
        ****** Why do we need to swap? Can't we just update ? Why make the swap from Staging to Production but back to Prodution to Staging for older version?
          - For rollback purposes!

      ## Deploying Web Jobs
        - A WebJob is an application or script that can be run as a background task in Azure website
        - A WebJob can be configured as On-Demand, Continuously Running, or Scheduled Task
          - If deployed as On-Demand or Continuously Running Task,
            * You only need to specify the name of WebJob, and path to the .zip file

      ## Publishing an Azure Website
        - Process in which web app (or code) is copied to one of the deployment slots
          1. Source control systems is used for continuous integration model where the website is deployed as code changes are checked into source control system
          2. FTP clients such as FileZilla
          3. Windows PowerShell
            - example of how app publishment to the Staging slot for website:
              `$pkgPath = "E:\Contoso-Web.zip"
              Publish-AzureWebsiteProject -Name $wsName -Slot $wsStaging -Package $pkgPath`
          4. Web Deploy
          5. Visual Studio
          6. Git

     ### Objective Summary ###

      1. Which Azure PowerShell cmdlet is used to create a new Azure website?
        -- Answer: New-AzureWebsite
          Why?
            -- New-AzureWebsite is the cmdlet used to create a new Azure website. At a minimum, you need to specify the location for the website and a unique DNS name
          Why not?
            - Publish-AzureWebsite is the cmdlet used to publish the web app (or code) into deployment slot of the website
            - New-AzureWebsiteJob is the cmdlet used to create a WebJob
            - Set-AzureWebsiteJob is the cmdlet used to set website properties, such as application settings, connection strings, framework versions and more

      2. Which of the following are valid task types for a WebJob?
        -- Answer: On-Demand, Continuously, Scheduled

      3. Which Azure Websites feature should you enable for running WebJobs?
        -- Answer: Always-On
          Why?
            -- Always-On is recommended for continuously running WebJobs
          Why not?
            - Autoscale is used to scale the number of standard instances of a website up and down
            - SSL is used to encrypt traffic on wire
            - Backup is a feature to back up the website contents and databases to Azure Blob Storage
      4. Which Azure PowerShell cmdlet is used to swap deployment slots in a website?
        -- Answer: Switch-AzureWebsiteSlot
          Why?
            - Switch-AzureWebsiteSlot is the cmdlet used to swap deployment slots. If a website has only 1 additional deployment slot, it is not necessary to specify the Slot2 parameter. If there are more than 2 deployment slots, it is necessary to specify Slot1, and Slot2
          Why not?
            - Get-AzureWebsite is the cmdlet used to get a list of the websites in a current subscription or configuration settings for a specified website
            - Restart-AzureWebsite is cmdlet used to stop and then restart a specified website
            - Show-AzureWebsite is cmdlet you can use to launch a browser and navigate to the URL of a spefied website

# 1.2 Configure Websites

<!-- 1.2 Configure Web Apps from book -->

**_ Objectives _**

- Configure Site Settings
- Configure custom domains
- Configure SSL certificates
- Configure Microsoft Azure Traffic Manager
- Configure handler mappings
- Configure virtual applications and directories
- Use the Azure Cross-Platform Command-Line Interface Tools for Configuration tasks

## Configure Site Settings

### Connection Strings and Application Settings

- Connection Strings: Unique Way to provide connection string setting to database rather than creating webconfig file || a string that specifies information about a data source and the means of connecting to it
  - SQL Database: A connection string for an Azure SQL database
  - SQL Server: A connection string for a SQL server running ona physical machine or Azure Virtual Machine
  - mySQL: A connection string for MySQL database
  - Custom: A connection string for NoSQL storage option such as Azure storage account
- Site settings for connection strings and application settings are defined as key/value pairs;
  - Example:

    - Key = "NowOrLaterDBConnectionStr" Value = "Server=tcp:noworlater.database.windows.net, 1433:Database=noworlater-database; User ID=AdminUser@noworlater; Password={myPW}; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;"
