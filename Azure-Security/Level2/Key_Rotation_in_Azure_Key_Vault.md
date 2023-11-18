# Key Rotation in Azure Key Vault

What is Azure Key Vault?
Azure Key Vault is a cloud service for securely storing and accessing secrets. Key Vault service supports two types of containers: vaults and managed hardware security module(HSM) pools. Vaults support storing software and HSM-backed keys, secrets, and certificates. Managed HSM pools only support HSM-backed keys.

With Azure Key Vault, we can individually backup secrets, keys, and certificates

Automated key rotation in Key Vault allows users to configure Key Vault to automatically generate a new key version at a specified frequency. You can use a rotation policy to configure rotation for each individual key.

## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4a94f65c-52c7-4ca4-a553-cef0863005b5)

## Task 2: Create a key vault and Key in Key Vault

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/9e2e6cd6-10e2-482c-b13a-3426035b4e7e)


- Access user for the Key:

 ![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b12a3bfe-4275-4887-8ba1-2801e1d82395)

## Task 3: Create a Key in the Key Vault 

- create a new RSA key with a key size of 2048 in the Key Vault.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4df1194e-846b-499c-ae14-b3f63129eb04)

## Task 4: Configure the Key Rotation

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/279f5e0b-af0c-492b-a146-b30ff8720d01)


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/abed73f1-b03b-46cb-98d5-88ecb7dba8f1)

 Done .
  - - -
