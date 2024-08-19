# Guidance for Amazon Q Business

This guidance helps to create a Amazon Q application, connect with data sources and have a chat with a HR application through a custom plugin.

## Table of Contents 

1. [Overview](#overview)
    - [Cost](#cost)
2. [Prerequisites](#prerequisites)
    - [Operating System](#operating-system)
3. [Deployment Steps](#deployment)
4. [Deployment Validation](#deployment)
5. [Running the Guidance](#running-the-guidance)
6. [Next Steps](#next-steps)
7. [Cleanup](#cleanup)

## Overview

This guidance aims to showcase how to build an end-to-end business application using Amazon Q, a conversational AI assistant, along with AWS services like CloudFormation, DynamoDB, and Lambda. It demonstrates the integration of Amazon Q to retrieve relevant information, pass it to a language model, and return a response. The guidance also uses Infrastructure as Code to manage the application's resources and includes a sample HR time-off request application built using the Amazon Q custom plugin. The key objective is to provide a blueprint for developers to build conversational AI-powered business applications, leveraging the capabilities of Amazon Q and the AWS ecosystem.

![Architecture Diagram](./assets/archdiagram.png)

### Cost 



### Sample Cost Table 


## Prerequisites 
- AWS Account that you have admin access.
-  An instance of IAM Identity Center and note down the ARN. Enabled an IAM Identity Center instance, provisioned at least one user, and provided each user with a valid email address. (https://docs.aws.amazon.com/amazonq/latest/qbusiness-ug/idp-sso.html)

### Operating System 

These deployment instructions are optimized to best work on **<MacI>** you can also use Cloud9.  

### AWS account requirements (If applicable)

This deployment requires you have a Amazon S3 bucket in your AWS account.

**Resources:**
- S3 bucket with folders names  **HR**, **Finance**, **Legal**, **Marketing**, **Sales**
- Once the folders are created, you can ingest some sample documents into each folder.


### Supported Regions (if applicable)

This guidance applies for all regions where Amazon Q for Business is vaialble. Please check here for availability in you region. https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/


## Deployment Steps
**Step 01**
Clone the repository ```git clone [<this repo name>](https://github.com/aws-solutions-library-samples/guidance-for-amazon-q-business) ```

**Step 02**

- In AWS Cloudformtaion in the console, create a stack and upload the template Q-HRplugin.yaml that can be found under deployment folder. Once deployment is complete 
- Once the deployment is complete for the above stack, create a new stack and upload the template Q-App.yaml that can be found under deployment folder.
- For the paramters, 


 
**Example:**

1. Clone the repo using command ```git clone xxxxxxxxxx```
2. cd to the repo folder ```cd <repo-name>```
3. Install packages in requirements using command ```pip install requirement.txt```
4. Edit content of **file-name** and replace **s3-bucket** with the bucket name in your account.
5. Run this command to deploy the stack ```cdk deploy``` 
6. Capture the domain name created by running this CLI command ```aws apigateway ............```



## Deployment Validation  

<Provide steps to validate a successful deployment, such as terminal output, verifying that the resource is created, status of the CloudFormation template, etc.>


**Examples:**

* Open CloudFormation console and verify the status of the template with the name starting with xxxxxx.
* If deployment is successful, you should see an active database instance with the name starting with <xxxxx> in        the RDS console.
*  Run the following CLI command to validate the deployment: ```aws cloudformation describe xxxxxxxxxxxxx```



## Running the Guidance 

<Provide instructions to run the Guidance with the sample data or input provided, and interpret the output received.> 

This section should include:

* Guidance inputs
* Commands to run
* Expected output (provide screenshot if possible)
* Output description



## Next Steps 

Provide suggestions and recommendations about how customers can modify the parameters and the components of the Guidance to further enhance it according to their requirements.


## Cleanup 

- Include detailed instructions, commands, and console actions to delete the deployed Guidance.
- If the Guidance requires manual deletion of resources, such as the content of an S3 bucket, please specify.
 *“For any feedback, questions, or suggestions, please use the issues tab under this repo.”*


## Notices 

*Customers are responsible for making their own independent assessment of the information in this Guidance. This Guidance: (a) is for informational purposes only, (b) represents AWS current product offerings and practices, which are subject to change without notice, and (c) does not create any commitments or assurances from AWS and its affiliates, suppliers or licensors. AWS products or services are provided “as is” without warranties, representations, or conditions of any kind, whether express or implied. AWS responsibilities and liabilities to its customers are controlled by AWS agreements, and this Guidance is not part of, nor does it modify, any agreement between AWS and its customers.*

