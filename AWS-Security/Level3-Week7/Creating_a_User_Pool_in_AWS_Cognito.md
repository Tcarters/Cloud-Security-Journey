# Creating a User Pool in AWS Cognito


## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/936afc25-8813-4405-9e5c-4c0396c4a8e9)



## Task 2: Creating a User Pool


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/85ff399e-254b-4639-a44c-8f14c52278c9)


## Task 3: Configure sign-in experience

- Add details in the configure sign-in experience : 

Provider Types : Select Cognito user pool

Cognito user pool sign-in options : Select Email

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a3554103-7a55-4ff0-8d46-144e73ae43af)


## Task 4: Configure Security Requirements

1. Password Policy:
   - Password Policy Mode : Select Cognito defaults
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/dc236e82-b771-48a2-b935-4d7db18963a5)

2. We give the Minimum Password Strength and can add the required parameters like numbers, lowercase, uppercase and special characters. Here, we are selecting Cognito defaults. We can customize this password as well.

3. Multi-Factor Authentication (MFA) increases security for your end users. Phone numbers must be verified if MFA is enabled. We choose No MFA for this lab.


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/508729b5-cbc9-483c-98aa-65d4bd13bf52)

## Task 5: Configure sign-up experience

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/da61bf6c-ae53-454e-85e7-5ec05a79fa22)

- We choose to allow users to sign themselves up, where the users can sign up themselves without administrator interference.

- Attribute verification and user account confirmation: 

Keep the changes as default. 

Required Attributes: 

- We can choose the Standard Attributes, which will be required while performing a sign-up. Here, we choose Name, Preferred Username, Phone Number which are required to perform a signup.

- We can also customize our attributes that are required while signup by clicking on Add custom attribute.



![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/15b6ca98-1c4d-4ddb-b748-4c6a3182ff7c)


## Task 6: Configure Message delivery

- Here, we are going to provide users with the option to configure message delivery, specifically email delivery, from the user pool. Users can choose to send emails using Amazon SES (Simple Email Service) and specify whether higher daily email limits are required. This task allows users to set up email communication for various purposes, such as user verification or password recovery.

- You can send emails from an SES verified identity. Before you can send an email using Amazon SES, you must verify each identity that you're going to use as a From, Source, Sender, or Return-Path address to prove that you own it. For now, we leave it blank.

- Amazon SES Configuration: Cognito will send emails through your Amazon SES configuration. Select Yes if you require higher daily email limits, otherwise select No. Here, we select Send email with Cognito in the Email provider.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2484a356-20dc-4014-a95d-d7920006b08c)

## Task 7: Integrate your app

 In this task, we are going to guide users in integrating their app with the user pool. Users can specify the user pool name and create an initial app client with a unique ID and an optional secret key. This integration step enables the app to authenticate and interact with the user pool for user management and authentication purposes.

- You can create a user pool.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5bd5ca80-25c4-49c3-9be2-625f2f2ee8aa)

- The app clients that we add will be given a unique ID and an optional secret key to access this user pool. Initial app client:

App client name: Enter **kekeclient**

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3f4344e9-18b8-452a-9cfa-4ee580a32e3c)


## Task 8: Review

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/abb4c91c-e6f7-4205-be48-1a70baaa36a0)

- Create user:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3eb88aa1-5ea1-4839-b887-ea1a9eaacdaa)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/11748c82-a825-4289-a03e-775f79cfbc7e)

Done..... 🎌

