# Web Log Analytics

## Description
This project processes **Apache compliant web log files** to derive inferences hidden in web log data.
This project cleans, structures web log data and visualizes it. <br/><br/>
![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/ServerTraffic.JPG)
[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/)
## Architecture
This project has developed data transformation system using Microsoft Azure technologies.
Following is the list of technologies used in this project:
1. **Azure Storage Account**: To persist unstructured raw data files and archival of processed output.
2. **Azure Data Factory**: Data orchestration and scheduled job execution
3. **Azure SQL DW/DB**: Structured output storage and querying
4. **OnDemand HDInsight Cluster**: To execute spark job for cleaning and structuring of data
5. **Batch Account**: For execution of custom ADF activities
6. **Power BI**: Data visualization

![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/Architecture%20Diagram.JPG)

User will drop or design system which can drop web log files to particular container in Azure Storage Account provisioned by this deployment at at regular intervals. In the backend Azure Data Factory will pickup these files at the same frequency and perform operations on it to clean and structure the data. Structured data will be persisted in SQL DB / SQL DW. This structured data will be visualized using Power BI.

## Deployment Steps

### Step 01: Create Azure AD App
Create Azure AD application and obtain App id and Authentication key by following steps mentioned at this [link.](https://docs.microsoft.com/en-au/azure/active-directory/develop/howto-create-service-principal-portal)

### Step 02: Deploy Azure Resources
1. Hit [deployment link](https://deploy.azure.com/?repository=https://github.com/ThirdEyeData/OutlierDetection#/form/setup)to open **Deploy to Azure** page.
2. Select appropriate **Directory** and **Subscription**.
3. Select option **Create New** for Resource Group and enter desired resource group name.
4. Enter appropriate user name and password in **Sql User Name** and **Sql Password** field respectively. Note down this credentials as it would be used for accessing SQL Server provisioned by this deployment.
5. Enter Azure AD App Id and Authentication Key obtained in step 01 as **Service Principal ID** and **Service Principal Key** respectively.
6. Press **Next** button at the bottom to start deployment.

### Step 03: Activate Azure Data Factory Pipeline
1. Visit Azure Portal and open resource group provisioned through this deployment.
2. Open Azure Data Factory instance inside the resource group.
3. Click **Author and Monitor** button present on Azure Data Factory overview blade to open ADF studio.
4. Select **Author** tab on ADF studio.  <br/>![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/ADF01.JPG)
5. Press **Triggers** button present at the bottom of ADF Studio.
6. Press **Edit** button present on **PipelineTrigger**.
7. On Edit Trigger pane set **Start Date**, **Recurrence** settings and check **Activated** checkbox.<br/>![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/ADF02.JPG)
8. Press **Finish** button to finalize edits.
9. Press **Publish All** button present on top of ADF studio to activate data factory. <br/> ![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/ADF03.JPG)
