#  Create an Application Gateway with WAF


__Cloud challenge details__

__You are a cloud solutions architect working with a fictional company called "TechWidgets Inc." They have recently developed a business-critical web application that processes customer orders and sensitive financial information. The company's leadership is concerned about the increasing number of cyberattacks targeting web applications and wants to ensure that their application is secure and available for their customers.

Your task is to design and implement an Azure Application Gateway with Web Application Firewall to protect the web application from common web vulnerabilities and ensure its availability and performance. You'll need to follow best practices, configure appropriate settings, and provide documentation explaining your decisions.

Follow the below instructions to complete this challenge.

__
1. Create a Virtual network:
   - Region: East US
   - IP address space: Select 10.0.0.0/16
   - Add a subnet:Starting Address: Enter 10.0.0.0, Subnet size: Select /24
   - Add another subnet: IP address space: Select 10.0.0.0/16, Subnet size: Select /24

2. Create an Application Gateway with WAF Enabled:
   - Region: Select East US
   - Tier: Select WAF V2

3. Add Virtual Machines
   - Region: Select East US
   - Availability options: Select No infrastructure redundancy required
   - Image: Select Windows Server 2022 Datacenter: Azure Edition - Gen2
   - Azure Spot instance: Leave the default unchecked.
   - Size: Select Standard_B2s
   - OS disk type: Select Standard SSD

__Solution__

Refers to this: 
https://github.com/Tcarters/Cloud-Security-Journey/blob/master/Azure-Security/Level4/8_Creating_an_Application_Gateway.md


