# Encrypt and Decrypt data at rest


What is Encryption and Decryption?
Data at rest in Azure Blob storage and Azure file shares can be encrypted in both server-side and client-side scenarios.

Azure Storage Service Encryption (SSE) can automatically encrypt data before it is stored, and it automatically decrypts the data when you retrieve it. The process is completely transparent to users.

Storage Service Encryption uses 256-bit Advanced Encryption Standard (AES) encryption, which is one of the strongest block ciphers available. AES handles encryption, decryption, and key management transparently.

Azure SQL Database is a general-purpose relational database service in Azure that supports structures such as relational data, JSON, spatial, and XML. SQL Database supports both server-side encryption via the Transparent Data Encryption (TDE) feature and client-side encryption via the Always Encrypted feature.

TDE is used to encrypt SQL Server, Azure SQL Database, and Azure Synapse Analytics data files in real time, using a Database Encryption Key (DEK), which is stored in the database boot record for availability during recovery.

TDE protects data and log files, using AES and Triple Data Encryption Standard (3DES) encryption algorithms. TDE is now enabled by default on newly created Azure SQL databases.


## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/68fb9dc6-62b4-46e9-90a8-9d60ec43fb1f)


## Task 2: Create a Storage Account

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8e34eb3e-c1aa-4d2c-9044-21ab8ad1e8f5)

## Task 3: Analyze Storage Service Encryption (SSE)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7ca62d0f-5599-4d20-a3b2-5069dfa41f93)

- Create key vault:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/21655f28-e9dd-48fa-b77e-dc0d110c2193)

- Enable Access policy for key:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/fc6ad8fa-bab6-4b41-ad67-9246f1b49762)

- Create key:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7c22f14d-c104-4a97-84c5-11f1985b560b)

- Select key for storage encryption

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a2b8a283-2bbe-4cf9-b64c-52e2691e6480)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/00fc6849-b943-4953-ac8b-69f636ff94ea)


## Task 4: Create a SQL Database server

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/31f5f3df-e107-44b6-b30b-9d245db3e8ad)


## Task 5: Analyze Transparent Data Encryption (TDE)

Azure Transparent Data Encryption (TDE) is a service provided by Microsoft Azure to enhance the security of data stored in Azure SQL Database and Azure Synapse Analytics (formerly known as Azure SQL Data Warehouse). TDE helps protect sensitive data at rest by automatically encrypting the database files, including backups and transaction log files, with a symmetric encryption key.


- TDE Enabled

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/bc2f8107-7575-464d-88a8-94e8c262059b)


Done .
