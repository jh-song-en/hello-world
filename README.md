# TFDMP GUI Manual

## Content
1. [Intorduction](#introduction)
    1. [Motivation](#motivation)
    2. [TFDMP](#ammd-db)
    3. [TFMDP GUI](#ammd-db-platform)
2. [Installation](#installation)
3. [Manual](#manual)
    1. [Login & Server setting](#login-and-server-setting)
    2. [Logbook tab](#logbook-tab)
    3. [Upload tab](#upload-tab)
    4. [Search tab](#search-tab)
    5. [Result window](#result-window)

## Introduction
### Motivation
  It is no lie that the discovery of new material leads to the development of new products with better performances. 
Many laboratories and institutions are seeking through the broad area of material space to find materials with better properties than before.

  AMMD (Applied Mechanics & Materials Design) Laboratory is one of these seekers; using combinatorial experiments, AMMD lab studies novel functional/structural materials.
The combinatorial (high-throughput) experiment is more effective than the conventional technique since it can map out a broad composition group with a single experiment.
By depositing the thin film over the substrate with uneven distribution of the material, the material group with a wide combination of composition is acquired. 
In addition, rapid characterization tools have been developed to map out the property of the materials with different compositions.

  AMMD DB is a high-throughput experiment material property database of the data acquired from the combinatorial experiments.
It is developed to preserve the characterization data generated from the laboratory and to enable computational analysis such as machine learning.
The researcher's interest is based on the experimental result that fits the purpose of the experiment. 
However, this may lead to the loss of the generated data that does not fit the research goal.
Also, the unstandardized formatting of each researcher of the characterization data causes a waste of time on reformatting the data to fit the analysis method by different researchers.
Both are the obstacle for the massive analyzation of the material data. The former reduces the amount and abundance of data and the latter becomes a bigger problem as the amount of data becomes vast.
AMMD DB & Platform prevents these problem by offering easy and standardized data storage of the data generated from high-throughput experiments.

### AMMD DB
![image](https://user-images.githubusercontent.com/72897259/147449857-397aa907-894a-4f3f-b35b-15fcead2cc84.png)

AMMD DB is consists of a MySQL database and File server. Metadata, supplementary information of the experimental data are stored in the MySQL database, while the characterized data are stored in the file server. 
Every data from High-throughput characterization is managed based on the Sample table. The sample table includes a detailed log of the deposition condition to enable the regeneration of the sample with similar properties. The information of the project and the person who is related to the sample implemented as a foreign key to manage sample information by different categories. <br>

The experiment condition is also stored in the MySQL server as a tabular form, as shown in the figure above, having id_sample as a foreign key. This primary-foreign key relationship enables the data management centered by the sample, making data related to the sample easy to find and access. The files stored in the file server are labeled by the primary key of the Sample table and property table, (id_sample-id_property) fabricating the relationship between the data and metadata. The benefit of this database structure is that the addition of the database with a new characterization process can be done by adding a single table to the MySQL server and a folder to the file server.



### AMMD DB Platform
![image](https://user-images.githubusercontent.com/72897259/147450416-c07f91a4-504e-4c2b-80e2-7cf0accfd935.png)

  AMMD DB Platform works as a client which connects the AMMD DB server and user. Through the AMMD DB Platform, user can upload, update, retrieve, and download the data, and manage the database itself.
The platform is consist of the logbook tab, search tab, upload tab, manage tab, and the result window.
Through the logbook tab and upload tab, user can upload the substrate sample information and characterization data generated through the high-throughput experiments, and search the sample of interest using the search tab. The detailed manual of each tab are described below.

## Installation
You can download the zip file from [here](https://drive.google.com/file/d/1ev7F_GvSoLW-SfkFEn2idv8Deidbp05j/view?usp=sharing)

    download AMMD_DB_Platform.zip file to your device, and unzip the file.
    Open AMMD_DB_Platform.exe.

![image](https://user-images.githubusercontent.com/72897259/148879324-e619fdf5-d089-48c6-8572-222d7dcf70b5.png)


## Manual
### Login and Server setting

	Press the server setting button and set the server as your server setting. If you installed the server in the same computer, the host will be localhost or 127.0.0.1.
	Press the Save button, and login with the id generated from the AMMD DB initiator

Discription about the id generation are [here](https://github.com/jh-song-en/AMMD_DB/blob/master/README.md#user-management)

![image](https://user-images.githubusercontent.com/72897259/148879474-7d398da0-fb10-46c0-828d-15b30091e2c5.png)


### Logbook tab
![image](https://user-images.githubusercontent.com/72897259/147438029-6f7dc468-3ef1-4e16-bd87-d967824efe68.png)

The logbook tab is used to upload the deposition condition of the synthesized substrate sample and to display the log of the previous deposition. After the sample deposition, the condition data can be stored through this tab and the id of the sample, which is used to manage the characterized data that are saved later, is given by the server. 
You can either ___upload new sample information___ and ___browse the current sample list___ with this tab.
___To upload the new sample information,___
	Choose the project and person related to the sample, and type the deposition date on the Sample general information edit.
    Insert the deposition conditions to the Sample deposition condition edit.
	Press the Save button.
For the user's convenience, quick data insert function is offered by double-clicking the rows of the Logbook table.
Through this process, the data is saved in the sample table in the MySQL server and the id of the sample is given from the server. The characterization data related to the sample can be uploaded, and the sample can be searched through this id.
It is recommended to put the information in detail to enable the regeneration of the sample. By default, the edit is set for the magnetron sputter of the AMMD laboratory, but the list of the edit can be modified by using the manage tab with the manager user.
### Upload tab
![image](https://user-images.githubusercontent.com/72897259/147901379-235a8fbe-73e2-49d7-bcb3-186e41376355.png)
The upload tab is used to upload the property of the thin-film sample, which is generated by the characterization process. The data uploaded must follow the standard process of the laboratory, following the standard format for the uniformity of the data. Different types of data are uploaded by the categories of the characterization process.
The image below is the example of the categorization of AMMD DB and the example of the data from each process.
![image](https://user-images.githubusercontent.com/72897259/147904316-42a21fd4-997d-4a22-b99c-e6c5ed93ac97.png)
Each characterization process generates different types of data. For example, EDS, Resistance, Thickness characterization produces a single or few sets of values, which can be recorded in a single row. These kinds of characterization processes are categorized as a ___Simple___ category. Therefore, these data are saved into a single .csv file, labeled by the cartesian coordinate of the characterized position on the sample surface.
On the other hand, processes such as XRD, Hardness, Image generates the data with a complex data form. Multiple data files are generated by the high-throughput experiment from the single sample substrate. Therefore, these kinds of processes are categorized as a ___Complex___ category. Multiple files can be uploaded during a single upload session. 
The complex category can be divided into two categories again, ___Locational___, and ___Unrestricted___. The data from the complex category should be labeled by the characterization position on the front of the file name.  The unrestricted category enables the data upload without this constraint, adding flexibility to the data upload. 

By following the steps below, you can upload the characterized data to the AMMD DB

![image](https://user-images.githubusercontent.com/72897259/147901752-9b665279-7368-4659-854e-c68c7c153088.png)

1. Characterization process metadata input
<br>
    Choose the characterization process to upload with the upload mode combo box.
    Input the sample id given from the logbook tab and metadata of the process on the property metadata edit.
    Click the file load button to select the file(s) to upload.
2. Data selection
<br>
 
    Select the data using the file browser and press the open button to load the file(s) to upload.
3. Data confirmation
Data can be confimed by the plot view and dobule-clicking the file name on the list view. If the file is in the right format, the platform will show the plot on the plot view.
        
    After checking the data, click the save button to save.
4. Sample confirmation and upload
<br>
    Confirm if the selected sample is the right sample.
    Press ok button to Begin the upload process.
    Press ok button after the platform finishes the upload process.
    
### Search tab

![image](https://user-images.githubusercontent.com/72897259/147912182-076c7ee4-548f-4533-b98f-5ff95e366985.png)

By using the search tab, the summarized information of the sample with the number of measured data can be viewed. There are four search types: Composition, ID, Project, and Person. The user can simply choose the search type on the ```search type combo box``` and input the keyword by typing on the ```search keyword edit``` or using the ```Additional keypad```. 

By double-clicking the rows of the ```search outcome table```, stored data can be reviewed with the review tab.


### Result window

![image](https://user-images.githubusercontent.com/72897259/149838600-d562ed27-9f60-436a-9092-b9ebaff5a84e.png)

Result window shows the information of the selected sample from the search tab.
Characterized data are shown with the deposition condition. The metadata can be modified by edit buttons, and data can be downloaded or deleted in this window.
Only manager user can delete the data or the whole sample data.
