# Serverless Data Analysis Platform

## Problem Statement

**Title**: Serverless Data Analysis Platform

**Project Description**: Create a serverless data analysis platform that allows Lambda functions to access and process data from both a public RDS database and a private RDS database. The platform should store results in an S3 bucket.

### Components:
- **RDS**
- **Lambda**
- **S3**
- **VPC and Subnets**

## Solution Overview

### Privately Accessible RDS
![Privately Accessible RDS](./mnt/data/Capture.PNG)

### Publicly Accessible RDS
![Publicly Accessible RDS](./mnt/data/Diagram%20Two.PNG)

### Problem Statement
![Problem Statement](./mnt/data/Problem%20Statement.PNG)

## Project Steps

### 1. Creating the VPC
1. **Create a VPC**:
   - Navigate to the VPC Dashboard in the AWS Management Console.
   - Click "Create VPC".
   - Provide a name for the VPC and set the CIDR block (e.g., 10.0.0.0/16).

2. **Create Subnets**:
   - Create a public subnet (e.g., 10.0.1.0/24) and a private subnet (e.g., 10.0.2.0/24).

3. **Create an Internet Gateway**:
   - Attach the Internet Gateway to the VPC.
   - Modify the route table of the public subnet to route traffic to the Internet Gateway.

### 2. Setting up AWS Lambda with Layers
1. **Create a Lambda Layer**:
   - Navigate to the Lambda Dashboard.
   - Click "Layers" and create a new layer.
   - Upload your file and provide a name and description.

2. **Create a Lambda Function**:
   - Create a new Lambda function.
   - Attach the previously created layer to this function.

3. **Configure Lambda Function**:
   - Set the runtime environment and handler for the function.
   - Add necessary permissions and environment variables.

### 3. Configuring RDS
1. **Create an RDS Instance**:
   - Navigate to the RDS Dashboard.
   - Create a new RDS instance (MySQL/PostgreSQL).
   - Ensure the RDS is in the same VPC as created above.

2. **Security Group Settings**:
   - Create or modify the security group to allow inbound traffic on the desired port (e.g., 3306 for MySQL).
   - Add your IP address to the inbound rules to allow access.

### 4. Connecting RDS using DBeaver
1. **Get the RDS Endpoint**:
   - Go to the RDS Dashboard and note down the endpoint of the RDS instance.

2. **Configure DBeaver**:
   - Open DBeaver and create a new connection.
   - Enter the RDS endpoint, port, database name, username, and password.

3. **Troubleshooting Connection Timeout**:
   - Ensure the RDS instance is publicly accessible.
   - Verify the security group settings.
   - Check VPC route tables and NACLs to ensure proper configuration.

### 5. Troubleshooting Connection Timeout Issue
1. **Security Group**:
   - Ensure that the security group attached to the RDS allows inbound traffic from your IP.

2. **Public Access**:
   - Ensure that the RDS instance is set to be publicly accessible if you are connecting from outside the VPC.

3. **Network ACLs**:
   - Check Network ACLs associated with the subnets for any restrictions.

4. **VPC Peering (if applicable)**:
   - Ensure proper VPC peering settings if your RDS is in a different VPC.

## Presentation Summary
- **Overview**: Created a VPC with public and private subnets and an Internet Gateway.
- **Lambda Setup**: Stored a file in Lambda layers and attached it to a function.
- **RDS Configuration**: Created an RDS instance and adjusted security groups for external access.
- **Issue and Solution**: Faced a timeout issue connecting to RDS via DBeaver; resolved by adjusting security settings and ensuring public accessibility.

---

This README provides a comprehensive guide to your project and serves as a helpful resource for anyone looking to understand or replicate your setup.
