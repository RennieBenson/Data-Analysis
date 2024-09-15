
**Descriptive Analysis**


**Project Description:** Descriptive Analysis of City of Vancouver Building Permits Issuance Data.

**Project Title:** Understanding the Building Permit Issuance Time for different Job Types.
**Objective:**

The primary goal of this project is to enable the City of Vancouver to improve its building permit issuance services to customers. Here the number of ‘Elapsed days’ for Building Permit Issuance is analyzed. The ‘Elapsed days’ represent the number of days from the application submission date to the issuance of the permit date. Through this analysis, the intention is to evaluate the average permit elapsed days for the different types of jobs, identify the trends and recommend strategies to reduce the time gap. 
**Dataset:** 

The dataset includes transactional data from the City of Vancouver's data portal website under the section ‘Building Permits Issuance’. The dataset is downloaded for the years 2023 and 2024 for the geographical area ‘Kensington-Cedar Cottage.’ The building Permits dataset comprises the following key features:
**_Permit Number:_** The unique number that identifies each Permit.

**_Application Created Date:_** This is the date of application of the customer for the Permit.

**_Permit Issued Date:_** This is the date of issuance of the Permit.

**_Permit Elapsed Days:_** Difference between the Application creation date and the Permit Issue Date.

**_Type of Work:_** Distinguishes the type of work carried out- ‘Demolition’, ‘Alteration’, ‘New Building’ or ‘Salvage and Abatement’.

**_Project Value:_** The value of the Project.

**_Applicant Address:_** The address of the applicant.

**_Property Use:_** Identifies the purpose of the property, whether used for residential purpose or office use or retail or service use. 

**_Geolocation:_** The location of the property.

The below given screenshot displays the 2023 Building Permits dataset.


![2023 Issued Building Permits Dataset](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/2023%20dataset.png)

The below given screenshot displays the 2024 Building Permits dataset.

![2024 Issued Building Permits Dataset](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/2024%20dataset.png)

**Methodology:**

**1.	Data Collection and Preparation:**

From the City of Vancouver's data portal website, 2023 and 2024 dataset in excel format has been downloaded for the year 2023 and 2024 for the geographical location mentioned above. In AWS S3 service folders have been created. The main bucket name is “Propertyanddevelopment-issuedbldgpermits-rennie” and subfolders are created under it. For storing 2023 and 2024 dataset two separate subfolders by the name ‘2023’ and ‘2024’is created.  Under each of these folders, three subfolders namely, Landing, Raw, Trusted and Curated are created. The Landing folder will contain the excel dataset downloaded from the city of Vancouver data portal. The Raw folder will contain the cleaned and structured dataset. Once cleaning and structuring is completed data governance is carried out by applying dataset quality and privacy rules. The results of data governance will be stored in the Trusted folder. The ETL implementation results will finally be stored in the Curated folder.

Given below is Trusted folder for 2023 dataset
![Trustedfolder2023](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/2023%20Trusted%20folder.PNG)


Given below is Trusted folder for 2024 dataset
![Trustedfolder2024](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/2024%20trusted%20folder.PNG)


Using draw.io the AWS services and the flow of the process from S3 bucket Landing folder to the Curated folder is represented below along with the AWS services used at each stage. 

![drawio](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/drawio.png)


**2.	Descriptive Statistics:**

   The descriptive metric ‘Average Permit Elapsed Days for Type of types’ is used here to evaluate the average time for permit issuance for the different type of jobs like demolition, alteration, new building or salvage works. This metric will give insights into the type of work that takes longer for permit issuance. Hence stakeholders can identify the job types that face delays and focus on improving the operational aspects in the required areas. When the problematic areas can be identified, corrective steps can be taken by the stakeholders to improve the services.

   
![metric](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/metric.png)

The following diagram created using draw.io displays four metrics that were created- the descriptive, diagnostic, predictive and prescriptive. As part of this project the descriptive metric is used.


![drawio1](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/drawio1.png)
![drawio2](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/drawio2.png)


**3.	Implementation of the Descriptive Metric:**


**_•	Data Pipeline Design_**

Using Draw.io data lineage diagram for the 'Issued Building Permits dataset,' depicting the processes required to compute the average elapsed time for various task types for the two years 2023 and 2024 was prepared. This diagram was designed with the aim to analyze and check the comparative job-wise average for both years. This design will be used to construct the ETL using the AWS Glue service. The screenshots of the lineage diagram are provided below. 


![drawioetl1](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/drawioetl1.png)
![drawioetl2](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/drawioetl2.png)
![drawioetl3](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/drawioetl3.png)


**_•	Data Cleaning and Structuring_**


The Building Permits dataset for the year 2023 and 2024 cannot be directly utilized to implement the data pipeline designed above. This data needs to be cleaned and structured before being used. This action can be achieved using AWS Data Brew service. Using the service two separate projects were created with the relevant dataset from the Landing folder. Upon execution of the job the cleaned and structured data was stored in the respective Raw folders. 


Projects Created in Databrew

![projectsdatabrew](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/2%20Projects%20created%20in%20databrew.PNG)

AWS Data brew data cleaning for ‘Issued Building Permits’ 2024 dataset

![databrewcleaning2024](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/Databrew%20for%202024%20data%20project.PNG)

AWS Data brew data cleaning for ‘Issued Building Permits’ 2023 dataset

![databewcleaning 2023](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/databrew%20for%202023%20data%20project.PNG)

2 jobs created for the ‘Issued Building Permits’ datasets

![jobs](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/two%20jobs%20created%20in%20databrew.PNG)


‘Issued Building Permits’ 2024 results are stored in the Raw folder

![Raw](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/raw%20folder.jpg)


**_•	Data Protection_**
Data Protection is of utmost importance whether the data is in motion or at rest. The data faces constant threat from unauthorized or invalid users in terms of Confidentiality (C), Integrity (I) and Availability (A). Hence implementing a CIA protection layer is critical. In this project using AWS Key Management Service (KMS) encryption key was generated. A role defined in the Identity and Access Management Service with policy documents linked to it containing the permissions was assigned to access and administer this newly created key. This key was then used to encrypt the data stored in the S3 bucket ‘Propertyanddevelopment-issuedbldgpermits-rennie’ subfolder. Hence, all documents stored in the folder will be encrypted. The authorized user decrypts the information and views it when downloaded. 

Creation of Key using KMS

![KMS](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/key%20creation%20in%20KMS.PNG)

Encryption key connected to the folder in AWS S3 

![bucket encryption](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/encryptionrule%20enabled%20in%20s3%20bucket.PNG)

In order to ensure Availability, replication of the folder is required. Replication rule is first defined and a backup folder is created and the rule is linked to the folder. 

Replication Rule

![replication rule](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/replication%20rule.PNG)

Backup folder linked with Rule

![backup](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/backup%20folder%20created%20in%20s3%20bucket.PNG)


**_•	Data Governance_**
Although the data is protected from invalid users, data governance needs to be carried out to ensure the quality, privacy, protection and compliance of data with the laws and regulations. For the two Issued Permits datasets, data privacy and quality rules were applied. After implementing the rules, the datasets were stored in the Trusted folder. The rules were implemented using the service AWS Glue. These datasets can now be used to implement the ETL pipeline that was designed.

2023 Dataset ETL

![2023PRQR](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/ETL%202023.PNG)

2024 Dataset ETL

![2024PRQR](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/Glue-PRQR-2024.PNG)



**_•	Data Pipeline Implementation_**

The two datasets from the Trusted folder are now used to implement the ETL design using the AWS Glue service. The end results are then stored into the Curated folder for further action.


![etl](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/ETL-pipeline%20-fullscreen.PNG)

The output of the ETL Implementation for ‘Issued Building Permits’, which shows the Average Permit Elapsed Days for different job types against the years 2023 and 2024, is given below.


![output](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/ETL-Pipeline%20-%20Output.PNG)


After preparing the ETL, the ‘Run’ command was executed. 

![run](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/ETL%20Run.PNG)


The result is stored in the Curated folder shown below.

![curated](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/Curated%20folder.PNG)


**_•	Data Analysis_**


Data analysis is to be carried out to facilitate data visualization. Using AWS Athena, a database was created by name ‘propertyanddevelopment_permits_database_rennie’ and then a table ‘propertyanddevelopment_permits_table_rennie’ with three columns ‘Type of Work,’ ‘AveragePermitElapsedDays 2024’ and ‘AveragePermitElapsedDays 2023’ was created. This step is important because the implemented ETL results need to be converted to an understandable format so that clear insights can be obtained. These insights are the basis of the action steps or optimization operations that will be conducted by the City of Vancouver to improve their services. 


![athena](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/athena.png)

The records in the table are as follows. The query result is set to get updated in the Dataproducts folder under the curated folder. 


![result](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/athena%20result.png)


The result obtained in this step is downloaded in an excel file format. This excel file will be used for visualization for this project. 


**4.	Data Visualization:**


Using the excel file downloaded in the previous step, the graphical representation of the data is generated using the graphical tools available in Excel. 


![output](https://raw.githubusercontent.com/RennieBenson/Data-Analysis/main/WS%20output2.PNG)


**5.	Insights and Findings:**
The average elapsed days for different job types were compared for the period 2023 and 2024 and the insights obtained are as follows:

•	The maximum issuance time is taken for issuing permits for ‘New Buildings’ job type and the least time is taken for issuing permits for ‘Salvage and Abatement’ jobs. 

•	The graph shows that issuance duration for the year 2024 has increased when compared with 2023 for each of the job types. This indicates a slow down in the permit issuing process. 

•	The issuance duration percentage increase in the year 2024 is highest in the case of Addition / Alteration jobs. It was approximately 37% higher in 2024 compared to 2023. This is a big increase in the issuance time, and it needs to be addressed urgently.

•	There was also a 34% increase in issuance time for ‘New Building’ jobs. This is also a big increase and causes concerns as the amount of time for new constructions are delayed due to delay in permit issuance. 

**6.	Recommendations:**

•	The issuance period time span increase should result from various factors like understaffing or inefficient processes or increased volume of applications. A root cause analysis needs to be carried out to identify what the reason for the issuance delay is and why there has been an increase in delay from 2023 to 2024.

•	A study must be conducted to identify if the request load is maximum during any particular season and if issuance delays are maximum during this time. If so, more resources need to be allocated to the job types with maximum demand on a seasonal, temporary basis.

•	Since the issuance time has increased for all job types from 2023 to 2024, it is clear that the problem needs to be managed for all job types. Hence, if the delay is due to improper resources allocation, then more staff members need to be hired.

•	The procedures for permit issuance should be reanalysed and changes can be brought in to streamline or optimize the different stages.

•	Automating tools may be added to reduce repetitive tasks.

•	Implement Performance Monitoring system so that delays and bottlenecks can be identified at a faster pace and steps can be taken early to mitigate the delays.

•	Obtaining feedback from applicants with regards to which process they faced maximum delay can help identify processes that need to be optimized. For some common issues that may arise like incomplete applications contribute to the delays, then this can be resolved by offering clear guidance on application process to the applicants prior to submission. Also offering services like pre-submission checks could help reduce submission errors thereby speeding up the process.

•	Offering training programs to the employees on a regular basis and setting performance goals linked to employee evaluations can help enhance employee productivity. 

**Tools and Technologies:**

•	ETL design and some diagrams were created in draw.io

•	Stages from Data Preparation, Cleaning, Structuring, Storing, ETL implementation and implementation were all done using various AWS services like S3, Data brew, Glue, KMS.

•	Data analysis was performed using AWS Athena Service.

•	Data visualization was done using excel.

**Deliverables:**

•	At the end of the analysis, the stakeholders need to be provided with detailed findings and recommendations for improvement. 

•	This can be in the form of a direct presentation to the team to communicate the findings and recommendations for improvement.
Hence, through this analysis project a comprehensive understanding of the permit issuance time with regards to the different types of jobs can be carried out. The insights obtained from the project can be used to improve the processes, procedures of operations and enhance the services to cater to the needs of the city in the most efficient manner.

