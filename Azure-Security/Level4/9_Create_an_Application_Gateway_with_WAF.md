# Create an Application Gateway with WAF

__What is an Application Gateway?__
- An Application Gateway is a web traffic load balancer that works on layer 7 of the OSI model

- It can make routing decisions based on additional attributes of an HTTP request, for example, URI path.

- It supports SSL/TLS termination at the gateway, after which traffic typically flows unencrypted to the backend servers

__What is a Web Application Firewall (WAF)?__

1. A WAF or web application firewall helps protect web applications by filtering and monitoring HTTP traffic between a web application and the Internet. 

2. It typically protects web applications from attacks such as cross-site forgery, cross-site scripting (XSS), file inclusion, and SQL injection, among others. 

3. A WAF is a protocol layer 7 defence (in the OSI model), and is not designed to defend against all types of attacks. This method of attack mitigation is usually part of a suite of tools which together create a holistic defence against a range of attack vectors.

4. By deploying a WAF in front of a web application, a shield is placed between the web application and the Internet. 


## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c0db773b-6ee2-4186-b814-237d9e311275)


## Task 2: Create a Virtual Network

- Subnet 1

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/23ca77c1-f0ca-4d2c-9c2f-6a40f2134910)

- Subent 2 myBackendSubnet

  ![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f7c2dff5-3243-4607-b5ef-57e1ac1a6dcc)

## Task 3: Create an Application Gateway with WAF Enabled
-  create an Application Gateway with Web Application Firewall (WAF) enabled in Azure. This gateway acts as a secure entry point for web traffic, providing protection against web-based threats and attacks while efficiently routing requests to backend servers, enhancing the security and performance of your web applications.

- WAF policy

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1324c6fa-c5e3-4712-ac3a-22d289805426)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a3838680-146d-4a32-aa20-e5c5e566798b)

- gwpublic IP

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c16f1849-9658-409b-83d5-d652e72cc67d)

- Click on the Next: Backends option and click on Add a backend pool.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ae16b305-71cd-49a9-8b94-77e04fe86c65)

- Click on the Next: Configuration option and select +Add a routing rule.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6090e36b-b40e-475d-a38d-a632a70bc190)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/40eebac0-d7fc-4e19-ac4c-27f5b0c4e05c)



## Task 4: Create Virtual Machines

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5ae4d76f-8882-474c-8c1e-23076850689e)

- Select myBackendSubnet

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/9bacd457-1b7c-4199-a4e0-a4afbfac7866)

- Same for VM2 with same subnetgw and ports 80,3389 enabled

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ba1e6d11-f7a7-4448-aa60-a011a4d11334)


## Task 5: Install IIS in the Virtual Machines

- install Internet Information Services (IIS) on the virtual machines. IIS is a web server role that enables hosting and serving web applications on Windows-based VMs, allowing you to deploy and run your websites on these virtual machines

```ps1
$location = 'east us'
Set-AzVMExtension -ResourceGroupName <your_resource_group_name> -ExtensionName IIS -VMName myWhizlabsVM1 -Publisher Microsoft.Compute -ExtensionType CustomScriptExtension -TypeHandlerVersion 1.4 -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:COMPUTERNAME)"}' -Location $location

```
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5dd0d0bd-5f0d-4579-93a7-491fa93e7c62)

- Same for VM2

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ab9e3069-ddb3-4766-9d78-4c5f3db39b0d)


## Task 6: Add backend servers to the backend pool

- Edit Backend Pool

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0e6738e0-1d93-4f02-adb4-2f46e1f5c429)


## Task 7: Test the Application Gateway 

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2bc3d843-bfd4-46cd-83b5-ca4bba7d11f9)

- Paste in browser public IP of gateway: 20.127.141.130

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e09e8cf0-3ac6-45a5-8062-d94846e199be)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b9ddd5a8-0f30-4bda-a33f-04b38a032d80)

- - -
DOne ...



