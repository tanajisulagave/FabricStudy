# Meta Driven Pipeline using MSSQL and MYSQL server
Suppose we have 2 databases 
1)	MSSQL server
2)	MySQL server \
I need to transfer the all tables data from these 2 sources to lakehouse destination in Microsoft fabric
## A.	Create one metadata table name is “Config” 

Create table Config\
(\
Id int primary key,\
SourceType varchar(100),\
SourceConn varchar(100),\
[Database] varchar(100),\
SourceTable varchar(100),\
TargetLakehouse varchar(100),\
TargetTable varchar(100),\
FileFormat varchar(100)\
)

select * from Config

## Add meta data information into this table

Insert into Config values (\
1,'MSSQL','MSSQL_Connection','AdventureWorksLT2017','BuildVersion','FabricLakehouse','buildversion','parquet'),\
(2,'MySQL','MySQL_Connection','tanajidb','Employee','FabricLakehouse','employee','parquet'),\
(3,'MSSQL','MSSQL_Connection','AdventureWorksLT2017','SalesLT.Address','FabricLakehouse','Address_New','parquet')
\
\
 <img width="975" height="148" alt="image" src="https://github.com/user-attachments/assets/dc25456a-07a6-4516-a7ad-163549f29aeb" />


## B.	Gateway configuration
Install on premises gateway and configure the same. \

 <img width="767" height="770" alt="image" src="https://github.com/user-attachments/assets/423ca4fb-de54-44f6-93e7-90e3192fa0f5" />


Once gateway connected please check connection established in fabric. \
Go to setting --> Managed connections and Gateways --> on-premises data gateway

<img width="1103" height="222" alt="image" src="https://github.com/user-attachments/assets/c1f711e0-edd7-422e-adac-6d1d2661f17f" />

 
## C.	Lookup Activity to read the metadata tables

So now metadata table available in MSSQL server so our connection is MSSQL server

Sample connection setting for MSSQL:- provide server name, Database Name, modify connection name as per your requirement , select Gateway and choose authentication method.


 <img width="561" height="544" alt="image" src="https://github.com/user-attachments/assets/8aeb6192-d745-4e8e-958a-fa13254b6ac2" />

 <img width="477" height="552" alt="image" src="https://github.com/user-attachments/assets/6dae9f95-1adb-4977-90b1-04dd5ae90d8a" />


## D.	Foreach Activity :-
Connect foreach activity to one by one data reading from lookup activity
<img width="975" height="453" alt="image" src="https://github.com/user-attachments/assets/cd2dfe4c-1c95-4f7b-aecd-a6f9b77cb05e" />
 

## E.	If Condition:-
Into Foreach activity use IF condition --> In this IF condition in expression we can use add dynamic content --> “@equals(item().SourceType, 'MSSQL')”.\
Means true condition we can read SQL server data 


<img width="621" height="645" alt="image" src="https://github.com/user-attachments/assets/f8874143-90f9-4393-a1a8-2fad581ad6dc" />
 
## F.	True Condition: - Copy Activity:-
Source:-

 <img width="604" height="554" alt="image" src="https://github.com/user-attachments/assets/7323449a-6e10-4744-9fff-6c9d7ef96f10" />

Destination:-

<img width="752" height="621" alt="image" src="https://github.com/user-attachments/assets/14b8ba32-f500-40f6-9c51-699f71e7e133" />
 
False Condition (MYSQL) :- 
Source

<img width="805" height="653" alt="image" src="https://github.com/user-attachments/assets/6bd91535-9ceb-4716-9115-511c79aa9119" />

Destination:- 

<img width="973" height="820" alt="image" src="https://github.com/user-attachments/assets/0962c0c4-8e54-4aa2-8c93-151d7fed4db2" />
 

Note – If you wanted to check all connection
Go to Setting  Managed Connections and gateways 
 
