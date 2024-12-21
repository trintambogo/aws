# Automating Daily reminders with AWS Lambda and Cloudwatch 

Automating reminders can save time and ensure that important tasks are never missed. In today’s fast-paced world, staying on top of reminders and notifications is crucial. In this article, I will walk you through how I automated a simple meeting reminder to my email using AWS Lambda and CloudWatch.

# Step 1 : Setting Up sns (simple notification service)
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
