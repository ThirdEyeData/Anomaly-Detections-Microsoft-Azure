# Web Log Analytics

## Description
This project processes **Apache compliant web log files** to derive inferences hidden in web log data.
This project cleans, structures web log data and visualizes it. <br/><br/>
Following are some visuals derived from web log data:<br/>
![](https://github.com/ThirdEyeData/Outlier_Detections_Weblogs_Analytics/blob/master/ThirdEye%20-%20Web%20Log%20Analytics%20-%20Power%20BI%20Visuals/Slide2.PNG)
<br/>
![](https://github.com/ThirdEyeData/Outlier_Detections_Weblogs_Analytics/blob/master/ThirdEye%20-%20Web%20Log%20Analytics%20-%20Power%20BI%20Visuals/Slide3.PNG)
<br/>
![](https://github.com/ThirdEyeData/Outlier_Detections_Weblogs_Analytics/blob/master/ThirdEye%20-%20Web%20Log%20Analytics%20-%20Power%20BI%20Visuals/Slide4.PNG)
<br/>
![](https://github.com/ThirdEyeData/Outlier_Detections_Weblogs_Analytics/blob/master/ThirdEye%20-%20Web%20Log%20Analytics%20-%20Power%20BI%20Visuals/Slide5.PNG)
<br/>
![](https://github.com/ThirdEyeData/Outlier_Detections_Weblogs_Analytics/blob/master/ThirdEye%20-%20Web%20Log%20Analytics%20-%20Power%20BI%20Visuals/Slide6.PNG)
<br/>
![](https://github.com/ThirdEyeData/Outlier_Detections_Weblogs_Analytics/blob/master/ThirdEye%20-%20Web%20Log%20Analytics%20-%20Power%20BI%20Visuals/Slide7.PNG)

## Architecture
This project has developed data transformation system using Microsoft Azure technologies.
Following is the list of technologies used in this project:
1. **Azure Storage Account**: To persist unstructured raw data files and archival of processed output.
2. **Azure Data Factory**: Data orchestration and scheduled job execution
3. **Azure SQL DW/DB**: Structured output storage and querying
4. **OnDemand HDInsight Cluster**: To execute spark job for cleaning and structuring of data
5. **Batch Account**: For execution of custom ADF activities
6. **Power BI**: Data visualization

![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/WikiImages/Architecture%20Diagram.JPG)

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
4. Select **Author** tab on ADF studio.  <br/>![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/WikiImages/ADF01.JPG)
5. Press **Triggers** button present at the bottom of ADF Studio.
6. Press **Edit** button present on **PipelineTrigger**.
7. On Edit Trigger pane set **Start Date**, **Recurrence** settings and check **Activated** checkbox.<br/>![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/WikiImages/ADF02.JPG)
8. Press **Finish** button to finalize edits.
9. Press **Publish All** button present on top of ADF studio to activate data factory. <br/> ![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/WikiImages/ADF03.JPG)

### Step 04: Make a data source connection in Power BI
1. Open Power BI Desktop file **ThirdEye - ARM Template-Pattern 1 Insights.pbix** placed in current repository, on your local machine.
2. Hit **Home > Edit Queries** button present on menu bar. <br/> ![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/WikiImages/Power%20BI%2001.JPG)
3. On Query Editor window, press menu **Home > Data source settings**. <br/> ![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/WikiImages/Power%20BI%2002.JPG)
4. Select data source present on Data source settings window and press button **Change Source** present at the bottom of window. <br/> ![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/WikiImages/Power%20BI%2003.JPG)
5. On SQL Server database window, enter the name of SQL server present in Azure resource group provisioned by this deployment. Press **Ok** button at the bottom.<br/> ![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/WikiImages/Power%20BI%2004.JPG)
6. Again select data source present on Data source settings window and press button **Edit Permissions** present at the bottom of window. <br/> ![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/WikiImages/Power%20BI%2005.JPG)
7. On Edit Permissions window, press **Edit** button. <br/> ![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/WikiImages/Power%20BI%2006.JPG)
8. On next popup window, ensure **Database** tab is selected and enter credentials of SQL server supplied while initiating this deployment. Press **Save** button to save credentials.<br/> ![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/WikiImages/Power%20BI%2007.JPG)
9. Close all popup windows, press **Close & Apply** button present on menu bar of Query Editor window to finalize change in database connection.<br/> ![](https://github.com/ThirdEyeData/OutlierDetection/blob/master/WikiImages/Power%20BI%2008.JPG).
<br/>Now have a look on all visuals present on Power BI file.

## Power BI Visuals
Power BI Visuals are described in **ThirdEye - Web Log Analytics - Power BI Visuals.PPTX** file, present in this repository.
