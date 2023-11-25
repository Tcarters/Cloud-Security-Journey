# Challenge 1 -  Key Rotation in Azure Key Vault

## Cloud challenge details

> You are an Azure administrator responsible for ensuring the security of cryptographic keys in an Azure Key Vault for a sensitive application. As part of your responsibilities, you need to perform key rotation for this Key Vault to enhance security. Your goal is to complete key rotation tasks within a controlled Azure environment.


Please follow the below instructions to complete this challenge.

1. Create an Azure Key Vault.
- Region: Select East US
- Pricing tier: Select Standard
- Days to retain key vault: Enter 90
2.Generate a cryptographic key and add it to the Key Vault.
3.Develop a key rotation plan and implement it.
- Expiry date: Enter 1 months
- Rotation time: Enter 18 days


## Solution 

### Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4420cf4b-4cf8-4342-a59c-0b4863b56569)

### 1.  Create an Azure Key Vault.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/efeff4f6-f1f4-49af-bf75-4f6b758cb023)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c6fc6720-6291-4468-a407-c0d4544be760)

- Configure Access user for the Key:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/550df676-60d4-44c0-8175-e907405b4a16)

### 2. Generate a cryptographic key and add it to the Key Vault.

- create a new RSA key with a key size of 2048 in the Key Vault.
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e82f9fcd-421a-4a9a-adcf-226bdf19c0a8)


### 3. Develop a key rotation plan and implement it.

- Enable Rotation Policy

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/22f293e7-d42c-4288-99ea-6771b3f235c4)

- And Save it:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a15546d1-56b6-480c-a0d2-2e8d5360459f)

Game Over :pushpin:	

- - -

