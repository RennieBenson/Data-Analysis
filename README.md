
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


![2023 Issued Building Permits Dataset](https://github.com/RennieBenson/Data-Analysis/blob/main/2023%20dataset.png)

The below given screenshot displays the 2024 Building Permits dataset.

![2024 Issued Building Permits Dataset](https://github.com/RennieBenson/Data-Analysis/blob/main/2024%20dataset.png)

**Methodology:**

**1.	Data Collection and Preparation:**

From the City of Vancouver's data portal website, 2023 and 2024 dataset in excel format has been downloaded for the year 2023 and 2024 for the geographical location mentioned above. In AWS S3 service folders have been created. The main bucket name is “Propertyanddevelopment-issuedbldgpermits-rennie” and subfolders are created under it. For storing 2023 and 2024 dataset two separate subfolders by the name ‘2023’ and ‘2024’is created.  Under each of these folders, three subfolders namely, Landing, Raw, Trusted and Curated are created. The Landing folder will contain the excel dataset downloaded from the city of Vancouver data portal. The Raw folder will contain the cleaned and structured dataset. Once cleaning and structuring is completed data governance is carried out by applying dataset quality and privacy rules. The results of data governance will be stored in the Trusted folder. The ETL implementation results will finally be stored in the Curated folder.

Given below is Trusted folder for 2023 dataset
![Trustedfolder2023](https://github.com/RennieBenson/Data-Analysis/blob/main/2023%20Trusted%20folder.PNG)


Given below is Trusted folder for 2024 dataset
![Trustedfolder2024](https://github.com/RennieBenson/Data-Analysis/blob/main/2024%20trusted%20folder.PNG)


Using draw.io the AWS services and the flow of the process from S3 bucket Landing folder to the Curated folder is represented below along with the AWS services used at each stage. 

![drawio](https://github.com/RennieBenson/Data-Analysis/blob/main/drawio.png)


**2.	Descriptive Statistics:**

   The descriptive metric ‘Average Permit Elapsed Days for Type of types’ is used here to evaluate the average time for permit issuance for the different type of jobs like demolition, alteration, new building or salvage works. This metric will give insights into the type of work that takes longer for permit issuance. Hence stakeholders can identify the job types that face delays and focus on improving the operational aspects in the required areas. When the problematic areas can be identified, corrective steps can be taken by the stakeholders to improve the services.

   
![metric](https://github.com/RennieBenson/Data-Analysis/blob/main/metric.png)

The following diagram created using draw.io displays four metrics that were created- the descriptive, diagnostic, predictive and prescriptive. As part of this project the descriptive metric is used.


![drawio1](https://github.com/RennieBenson/Data-Analysis/blob/main/drawio1.png)
![drawio2](https://github.com/RennieBenson/Data-Analysis/blob/main/drawio2.png)


**3.	Implementation of the Descriptive Metric:**


**_•	Data Pipeline Design_**

Using Draw.io data lineage diagram for the 'Issued Building Permits dataset,' depicting the processes required to compute the average elapsed time for various task types for the two years 2023 and 2024 was prepared. This diagram was designed with the aim to analyze and check the comparative job-wise average for both years. This design will be used to construct the ETL using the AWS Glue service. The screenshots of the lineage diagram are provided below. 


![drawioetl1](https://github.com/RennieBenson/Data-Analysis/blob/main/drawioetl1.png)
![drawioetl2](https://github.com/RennieBenson/Data-Analysis/blob/main/drawioetl2.png)
![drawioetl3](https://github.com/RennieBenson/Data-Analysis/blob/main/drawioetl3.png)


**_•	Data Cleaning and Structuring_**


The Building Permits dataset for the year 2023 and 2024 cannot be directly utilized to implement the data pipeline designed above. This data needs to be cleaned and structured before being used. This action can be achieved using AWS Data Brew service. Using the service two separate projects were created with the relevant dataset from the Landing folder. Upon execution of the job the cleaned and structured data was stored in the respective Raw folders. 


Projects Created in Databrew

![projectsdatabrew](https://github.com/RennieBenson/Data-Analysis/blob/main/2%20Projects%20created%20in%20databrew.PNG)

AWS Data brew data cleaning for ‘Issued Building Permits’ 2024 dataset

![databrewcleaning2024](https://github.com/RennieBenson/Data-Analysis/blob/main/Databrew%20for%202024%20data%20project.PNG)

AWS Data brew data cleaning for ‘Issued Building Permits’ 2023 dataset

![databewcleaning 2023](https://github.com/RennieBenson/Data-Analysis/blob/main/databrew%20for%202023%20data%20project.PNG)

2 jobs created for the ‘Issued Building Permits’ datasets

![jobs](https://github.com/RennieBenson/Data-Analysis/blob/main/two%20jobs%20created%20in%20databrew.PNG)


‘Issued Building Permits’ 2024 results are stored in the Raw folder

![Raw](https://github.com/RennieBenson/Data-Analysis/blob/main/raw%20folder.jpg)


**_•	Data Protection_**
Data Protection is of utmost importance whether the data is in motion or at rest. The data faces constant threat from unauthorized or invalid users in terms of Confidentiality (C), Integrity (I) and Availability (A). Hence implementing a CIA protection layer is critical. In this project using AWS Key Management Service (KMS) encryption key was generated. A role defined in the Identity and Access Management Service with policy documents linked to it containing the permissions was assigned to access and administer this newly created key. This key was then used to encrypt the data stored in the S3 bucket ‘Propertyanddevelopment-issuedbldgpermits-rennie’ subfolder. Hence, all documents stored in the folder will be encrypted. The authorized user decrypts the information and views it when downloaded. 


