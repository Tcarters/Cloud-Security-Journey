# Creating an Application Gateway

__What is an Application Gateway?__
- An Application Gateway is a web traffic load balancer that works on layer 7 of the OSI model

- It can make routing decisions based on additional attributes of an HTTP request, for example URI path.

- It supports SSL/TLS termination at the gateway, after which traffic typically flows unencrypted to the backend servers

- It is a fully managed Application Delivery Controller (ADC) service for securing, optimizing, and load balancing web traffic in Azure.

- ## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1cf180ed-6c05-4cb9-840d-50ace01565ce)


## Task 2: Create a Virtual Network

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ab961ff6-dce7-4678-a1f9-0e606df5cf5e)

- Subnets:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/34177744-047a-4193-8772-0b59387e3933)

## Task 3: Create Virtual Machines

- Add 1rst Machine:
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5ea65ec1-5506-4fc9-9d7d-e1d37cf55a45)

- Select Backend Pool subnet:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/67b51f1d-201e-4d29-a23e-a8893972312f)

- Add second VM on same subnet BackendPool

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f7d54116-4019-4514-b761-2b549801b7a2)

## Task 4: Install IIS in both Virtual Machines

- Connect VM1 and Install WEB server

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b8abee20-9b89-4483-bc5e-b79652a14285)

- Access web server
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d997c033-513c-40e9-b3a7-77738d83e059)

- Create a new folder for images on the server

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d9ebf014-62e8-482f-8626-864ee5d48a51)


  
- Connect VM2 and Install WEB server

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/49fc07ba-11d2-444e-a093-2d2df48f612d)


## Task 5: Create an Application Gateway

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/cea5506d-d98b-4446-9323-e715e7e0021f)

- Add Frontend in APp gateway:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4a6d71dc-60f2-482f-b115-99e3640d7c70)

- Add backendPool

  ![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/fb7d002f-f899-45f9-a2c3-8cc74be4c625)

- Add Secoond BackendPool for VIdeo

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4232c84d-cda8-4ceb-bd33-9e2eeeb4f894)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a5a7cdff-e64f-43d7-9fe0-92a47cd4aba7)

- Next Add Routing Rule:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4b23a794-14ad-4c77-8cfc-412b083ab3c3)

- For Listener RUle:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7049c0d0-ddb7-49c4-86a4-43246ada70b3)

- Config multi

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ad774515-0b45-4403-a37d-daf4930b8df7)

- Add second path multi sites

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5e33af3f-8950-4b22-af68-e53551af44e8)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/645053f6-d39e-4ee8-84ee-b53a27344178)

## Task 6: Test the Application Gateway

DOne.


