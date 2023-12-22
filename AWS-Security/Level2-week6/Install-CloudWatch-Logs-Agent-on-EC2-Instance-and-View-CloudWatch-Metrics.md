#  Install CloudWatch Logs Agent on EC2 Instance and View CloudWatch Metrics


## Diagram:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ed857b28-eac7-4d38-af0a-33545e535b9c)


## Task 2: Launching an EC2 Instance

- Create SG
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/16c5df0d-00a4-415d-9557-11171e09c066)

- Select a IAM profile

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0e81526a-9b3e-43b3-a3f6-eb22f62e6a58)


## Task 3: SSH into the EC2 Instance


## Task 5: Download and Install the Cloudwatch Agent

-  Download the Cloudwatch Unified Agent

```bash
wget https://s3.amazonaws.com/amazoncloudwatch-agent/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm

```

- Install

```bash
sudo rpm -U ./amazon-cloudwatch-agent.rpm
```
- Going to step to install the agent.
  
__On which OS are you planning to use the agent? : Enter 1

Are you using EC2 or On-Premises? : Enter 1

Which user are you planning to run the agent? : Enter 1

Do you want to turn on the StatsD daemon? : Enter 2

Do you want to monitor metrics from CollectD? : Enter 2

Do you want to monitor any host metrics? Enter 1

Do you want to monitor CPU metrics per core? Enter 1

Do you want to add ec2 dimensions into all of your metrics if the info is available? : Enter 1

Would you like to collect your metrics at high resolution? : Enter 1 (1s)

Which default metrics config do you want?: Enter 2

Are you satisfied with the above config? Enter 1

Do you have any existing CloudWatch log Agent configuration file to import for migration? : Enter 2

Do you want to monitor any log files? : Enter 2

Do you want to store the config in the SSM parameter store? : Enter 2 __


- Start the Agent:

```bash

sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s

```

- Check status of service cloudwatch:

```bash
systemctl status amazon-cloudwatch-agent

```

## Task 7: View the CloudWatch Metrics

Go to cloudWatch > all metrics, we should be able to see our agent running ...

DOne...🎌

