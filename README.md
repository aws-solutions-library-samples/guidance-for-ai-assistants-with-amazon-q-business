# Guidance for AI Assistants with Amazon Q Business

This guidance helps to create sample Amazon Q application for various usecases covering relevant Q's features. This guidance provides One click deployable cloudformation templates .

* HR Assistant (Available)
* Finance Assistant(Coming up)
* Sales Assistant(Coming up)
* Marketing Assistant(Coming up)
* Legal Assistant(Coming up)
* IT Assistant(Coming up)
etc.

## Table of Contents 

1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
    - [Operating System](#operating-system)
3. [Deployment Steps](#deployment-steps)
4. [Deployment Validation](#deployment-validation)
5. [Running the Guidance](#running-the-guidance)
6. [Next Steps](#next-steps)
7. [Cost](#cost)
8. [Cleanup](#cleanup)

## Overview

This guidance aims to showcase how to build an end-to-end business application using Amazon Q, a conversational AI assistant, along with AWS services like CloudFormation, DynamoDB, and Lambda. It demonstrates the integration of Amazon Q to retrieve relevant information, pass it to a language model, and return a response. The guidance also uses Infrastructure as Code to manage the application's resources and includes a sample HR time-off request application built using the Amazon Q custom plugin. The key objective is to provide a blueprint for developers to build conversational AI-powered business applications, leveraging the capabilities of Amazon Q and the AWS ecosystem.

![Architecture Diagram](./assets/archdiagram.png)

## Prerequisites 
- AWS Account that you have admin access.
-  An instance of IAM Identity Center and note down the ARN. [(https://docs.aws.amazon.com/amazonq/latest/qbusiness-ug/idp-sso.html)](https://docs.aws.amazon.com/singlesignon/latest/userguide/get-set-up-for-idc.html)

![IDC](assets/IDC.png?raw=true "IDC")
-  Create a user in identity center.

### Operating System 

Any operating system can be used.

### AWS account requirements

This deployment requires you have a Amazon S3 bucket in your AWS account.

**Resources:**
- S3 bucket 
- Once the bucket is created, you can ingest some sample document provided under the `assets` folder into the bucket.


### Supported Regions 

This guidance applies for all regions where Amazon Q for Business is vaialble. Please check here for availability in your region. https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/


## Deployment Steps

**Step 01**

Clone the repository ```git clone https://github.com/aws-solutions-library-samples/guidance-for-amazon-q-business ```

**Step 02**


- In AWS Cloudformtaion in the console, create a stack and upload the template `Q-HRplugin.yaml` that can be found under `deployment/plugins` folder.


![Plugin Creation CFN](assets/CreatePluginCFN.png?raw=true "Create Plugin CFN")
Once deployment is complete, you can get the value of  **ApiEndpoint** from the **Outputs** tab of the stack.

![API Endpoint](assets/APIEndpoint.png?raw=true "API Endpoint")
- Once the deployment is complete for the above stack, create a new stack and upload the template `Q-App.yaml` that can be found under `deployment` folder.

![Create QApp CFN](assets/CreateQAppCFN.png?raw=true "Create QApp CFN")
- For the paramters, enter the **ApiEndpoint**, name of the S3 bucket you had previously created and provide under **S3BucketName** and the ARN of the IDC instance in **IdentityCenterInstanceArn**

![Create QApp Parameters CFN](assets/CreateQAppParametersCFN.png?raw=true "Create QApp Parameters CFN")

**Step 03**
- Navigate to the newly created Amazon Q business app in the console. Follow the instructions here. Add the user you had created in the `IAM Identity Center` to this application.

![add user](assets/addUser.png?raw=true "Add User")

- Now "Edit" the application and proceed to the step where you create a new service role for the web experience. This would give you an endpoint for your application.

![edit Q](assets/editQ.png?raw=true "Edit Q")
![web experience](assets/webexperience.png?raw=true "Web Experience")
  
**Step 04**

- For **Sync Mode** choose **Full Sync**
  
![sync](assets/sync.png?raw=true "sync")

## Deployment Validation  

* Open CloudFormation console and verify the status of the 2 template to be **CREATE_COMPLETE**
* If deployment is successful, you should see an active Amazon Q application in the console.

## Running the Guidance 

In the newly created Amazon Q appplication, you can now run queries such as 

<u>**Query 1**</u>
- "How can I create a user in Amazon Q?"
- Note: Since your data source references Amazon Q user guide stored in Amazon S3 that has been indexed, it would have the context on what your question is about and give you the answer.

<u>**Query 2**</u>
- If you want to test the plugin, select the ellipsis and choose the plugin.
- Now you can query on vacation balance etc. "What is my vacation balance?"
  
## Next Steps 

You can ingest other documents in S3 or connect to other data sources, to your newly created Amazon Q application.


## Cost 
**Example Breakdown for Amazon Q Business**
You are an enterprise company with **5,000** employees looking to deploy Amazon Q Business. You decide to purchase Amazon Q Business Lite for 4,500 users and Amazon Q Business Pro for 500 users. You have 1 million enterprise documents across sources like SharePoint, Confluence, and ServiceNow that need indexing with an Enterprise Index. Your monthly charges will be as follows:
Enterprise Index for 1M documents will need 50 index units of 20K capacity each (assuming that the extracted text size of 1M documents is less than 200 MB * 50 units = 10 GB) :
* $0.264 per hour * 50 units * 24 hours * 30 days = $9,504
User subscriptions:
* 4,500 users * $3 per user/month = $13,500 
* 500 users * $20 per user/month = $10,000
* Total user subscriptions: $23,500
In summary, your monthly charges are as follows::
* Enterprise Index: $9,504
* User subscriptions: $23,500
* Total per month: $33,004 for 5000 enterprise employees.

We recommend creating a [budget](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-create.html) through [AWS Cost Explorer](http://aws.amazon.com/aws-cost-management/aws-cost-explorer/) to help manage costs. Prices are subject to change. For full details, refer to the pricing webpage for each AWS service used in this Guidance.

### Estimated monthly cost breakdown
The following table provides a sample cost breakdown for deploying this guidance  in the `us-east-1` region for one month.  Please note that these cost calculations are based on the default configuration options of the guidance deployment method described below.
| **AWS service**          | Dimensions | Cost per **month** \[USD\] |
|--------------------------|------------|------------|
| Amazon Q Business  | For 5000 enterprise users| \$33,004 |
| AWS Lambda    | Requests | \$46.91 |
| Amazon API Gateway|Requests| \$5.0 |
| **Total estimate** |  | \$33,200.54  |


## Cleanup 

Delete the two stacks in Cloudformation and make sure that Amazon Q application has been deleted in the console.

## Notices 

*Customers are responsible for making their own independent assessment of the information in this Guidance. This Guidance: (a) is for informational purposes only, (b) represents AWS current product offerings and practices, which are subject to change without notice, and (c) does not create any commitments or assurances from AWS and its affiliates, suppliers or licensors. AWS products or services are provided “as is” without warranties, representations, or conditions of any kind, whether express or implied. AWS responsibilities and liabilities to its customers are controlled by AWS agreements, and this Guidance is not part of, nor does it modify, any agreement between AWS and its customers.*

