# 1.	Adventure work Database (SQL Server) to Fabric Lakehouse
LookupActivity:-\
Query :-\
select B.Name 'SchemaName', A.name 'TableName' from sys.tables A\
inner join sys.schemas B ON A.schema_id=B.schema_id\
where B.name='SalesLT'

 <img width="566" height="400" alt="image" src="https://github.com/user-attachments/assets/57dde4b6-e36c-4777-8a28-7904064ae33f" />

<img width="715" height="788" alt="image" src="https://github.com/user-attachments/assets/74f8beef-af94-4721-9156-95cc344be3a8" />


## Foreach Activity:-
@activity('Lookup1').output.value

<img width="975" height="296" alt="image" src="https://github.com/user-attachments/assets/28f3ae10-5df9-453b-afa5-ef2e6c2ded83" />

 
## Copy activity:- ( Source and Destination connection)

First you need to configure on premise Gateways for SQL connection and establish SQL server Conection
 
<img width="866" height="588" alt="image" src="https://github.com/user-attachments/assets/dfd1b584-481b-4f82-a8ed-f204449d02aa" />

 <img width="849" height="500" alt="image" src="https://github.com/user-attachments/assets/d371ed45-961c-4ced-9d67-3ae9e8217135" />

<img width="849" height="500" alt="image" src="https://github.com/user-attachments/assets/60d3e633-3505-4d3f-bdb2-1a0ca1661452" />



File path:- @concat('Bronze','/',item().TableName)\
File Name:- @concat(item().TableName,'.parquet')

# 2.	MY SQL to Fabric Lakehouse
Configure Gateway and establish connection for MY SQL server\

Source

<img width="975" height="561" alt="image" src="https://github.com/user-attachments/assets/08f9817a-5d4d-4ed1-8e18-88513ecf643e" />


Destination
 
 <img width="975" height="442" alt="image" src="https://github.com/user-attachments/assets/4f2b4f5e-90eb-4fe1-9623-a7746f16ad19" />

 
File Path: - @concat('Bronze','/','Employee')\
File Name: - @concat('Employee','.parquet'


### Note:-
If you are getting error for connecting MY SQL server then run below power shell script

### Powershell script

[System.Data.Common.DbProviderFactories]::GetFactoryClasses()|ogv
