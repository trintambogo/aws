# Automating Daily reminders with AWS Lambda and Amazon EventBridge

Automating reminders can save time and ensure that important tasks are never missed. In today’s fast-paced world, staying on top of reminders and notifications is crucial. In this article, I will walk you through how I automated a simple meeting reminder to my email using AWS Lambda, Amazon SNS and EventBridge.

# Step 1 : Setting up Amazon SNS (Simple Notification Service)
Before we can send reminders, we need a service that can deliver the message. AWS SNS is a flexible, fully managed messaging service that allows you to send notifications to multiple recipients via SMS, email and even other AWS services.
 ## 1. Creating an SNS Topic
 - In the AWS Management Console, use the search bar to search for SNS (Simple Notification Service)
 - Click on **Create topic**
  ![08f28d81-e45d-4c31-8951-eec57cbba1d9](https://github.com/user-attachments/assets/52332daa-37e0-4a8d-864a-6fa48314ccd8)

 - Choose **Standard** as the topic type.
 - Under Name, enter a descriptive name for your topic, such as **Meeting Reminder**.
   ![e74cd60f-a0ce-4cae-b18f-4d38df22a277](https://github.com/user-attachments/assets/1dbe9492-a366-4b22-ac78-196a21a13c15)
   
 - Click Create topic to create the SNS topic
 - Under Subscriptions, click on **Create Subscription**
 - For the protocol, Select **Email**
 - Click **Create subscription**
 - You will receive a confirmation email. Open your email inbox and click on the confirmation link to **confirm your subscription.**
 - You will be required to confirm your subscription through your email address.
   ![cf526510-ffa0-4288-8377-ad63d70fcf3c](https://github.com/user-attachments/assets/79f81192-a982-400c-ac91-d5bbef41300b)
   
 - Once you've confirmed your subscription, go back to the SNS console and refresh your browser.
 - Take note of the **ARN (Amazon Resource Name)** of your SNS topic, which will be needed when configuring your Lambda function

# Step 2 : Setting up AWS Lambda
AWS Lambda allows us to run code without provisioning or managing servers. For this automation, we shall use Lambda to send a daily reminder to our SNS topic.

 ## 1. Creating a function
 -  Click on **create function**
 -  Select **author from scratch**
 -  Enter your desired function name
 -  Under runtime, select **python**
 -  Click on **create function**

  ![759fec68-1637-4780-91a6-876bd1ad2ff7](https://github.com/user-attachments/assets/247d7a47-97fa-49fa-8871-2dadcd1aeebe)

- Under the Code section, write the function code.
- The function below takes the ARN for the SNS topic, the message, and the subject for the email, and returns a response indicating whether the message delivery was successful.

  ![358475f3-f042-4c26-b224-c744c26a371e](https://github.com/user-attachments/assets/bb84b7b3-3353-4636-a5fa-1d323de0852b)

- Go to the **IAM role** associated with your **Lambda function.**
- Select the role that AWS creates automatically for the Lambda function
  
  ![1cf8e020-588b-47fa-8d67-18f54e615bf4](https://github.com/user-attachments/assets/0456b0ca-db5e-4444-955a-c07774c18325)

- Click on **Add permissions** and select Attach policies.
- Search for and attach the **AmazonSNSFullAccess policy** to the role

 ![bb84ca08-a668-4760-80e7-0f03398f118c](https://github.com/user-attachments/assets/61a5d0ca-d63f-4d0b-b787-f8f830225918)

- Create new test event, deploy the function and test it.

 ![838f2981-c8f8-4ebe-bf6a-88d1adf275c0](https://github.com/user-attachments/assets/fbb4aee4-fdf4-4e48-a340-5e9cb94344dd)


# Step 3: Setting up Amazon EventBridge

EventBridge helps you connect different applications by sending events between them. We shall use eventbridge to trigger an AWS Lambda Function to send notifications through amazon SNS. 

- Search for **Amazon EventBridge** in the AWS Management Console.
- In the EventBridge dashboard, search for **Schedules**.
- Click Create schedule and enter a **schedule name** eg: 'Meeting Reminder' .
- Choose whether you want the reminder to be **recurring** or a **one-time reminder**.
- Select the **date** you want to receive the reminder.
- Set the **time for the reminder**, ensuring to account for the timezone.
- Choose a **flexible time window**

  ![ae7c83a9-803a-444b-9c59-f3a32f98c57f](https://github.com/user-attachments/assets/3f7c6898-5914-4a77-8273-63100900cd9b)

- Select target API, and select AWS Lambda.
- On the lambda function, select the lambda function you craeted.
  
  ![70db95d5-4f49-4811-8607-b974dbb232e4](https://github.com/user-attachments/assets/519f66e2-5a29-4234-8cc1-602748ace4e3)

-  Click on next,and **Create Schedule**

# Step 4 : Verify if You Will Receive an Automated Email Notification
- At the scheduled time, open your email inbox.
- Check for the email notification that was sent to remind you about the meeting.
- Below is a screenshot showing that I set a reminder for 5:40 PM to notify me about an upcoming meeting.

   ![16461bf0-4fa7-4bf6-b2a0-ffee9be37b0d](https://github.com/user-attachments/assets/7c41dbb7-83a3-4dd6-8356-53c196a1cfb3)










