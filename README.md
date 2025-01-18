# Setting-up-a-Web-Server-with-AWS-CloudFormation

## Features
- Launch an EC2 instance in AWS.
- Automatically configure security groups to allow HTTP traffic.
- Deploy the web server and access it via a public URL.

## Prerequisites
1. An AWS account with access to the CloudFormation service.
2. A valid EC2 Key Pair to enable SSH access to the instance (if applicable).
3. Basic knowledge of YAML and AWS services.

## Steps to Deploy
1. Create a CloudFormation template in YAML format. Save it as `web-server.yaml`.
2. Log in to the AWS Management Console.
3. Navigate to the CloudFormation service.
4. Click on **Create Stack** and select **Upload a Template File**.
5. Upload the `web-server.yaml` file.
6. Provide a stack name (e.g., `WebServerStack`).
7. If needed, enter your EC2 Key Pair name in the Parameters section.
8. Keep other settings at their default values and click **Next**, then **Submit**.
9. Once the stack is created, locate the `WebsiteURL` output tag in the stack details.
10. Click the URL or copy and paste it into your browser to access the web server.

## Outputs
- The public IP address or URL to access the web server.

## Example CloudFormation Template
```yaml
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  WebServerInstance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      ImageId: ami-0c02fb55956c7d316 # Amazon Linux 2 AMI
      SecurityGroups:
        - !Ref WebServerSecurityGroup
      UserData:
        Fn::Base64: |
          #!/bin/bash
          yum update -y
          yum install -y httpd
          systemctl start httpd
          systemctl enable httpd
  WebServerSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Enable HTTP access
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
![image](https://github.com/user-attachments/assets/6fcc0b4e-5c99-47dd-8aee-b8d576f10dca)
![image](https://github.com/user-attachments/assets/e84eefce-1933-4a21-abad-2a24eaffb476)


