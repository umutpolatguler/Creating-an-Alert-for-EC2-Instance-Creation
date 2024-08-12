# Creating an Alert for EC2 Instance Creation

In this guide, I will show how to create an alert for EC2 instance creation in the Frankfurt region (eu-central-1) and have it delivered as an email.

- From AWS Management Console, navigate to SNS (Simple Notification Service) dashboard.

  ![Screenshot 2024-08-12 at 13-39-12 Topics Simple Notification Service eu-central-1](https://github.com/user-attachments/assets/fcc04f4d-772a-4601-94de-4ccb69c07bb6)

- Click on "Create topic". Give it a name and select the type as "Standart."
  
  ![Screenshot 2024-08-12 at 13-43-45 Create topic Topics Simple Notification Service eu-central-1](https://github.com/user-attachments/assets/f682032b-ba35-445d-9548-5aa716b2bc6f)

- After creating the topic, click "Create subscribtion" in the "Subscriptions" tab.

  ![Screenshot 2024-08-12 at 13-47-56 Create subscription Subscriptions Simple Notification Service eu-central-1](https://github.com/user-attachments/assets/c05e8c0a-d87d-43c0-93d7-680abd0b72ae)

- Set "Protocol" to "Email" and enter the email adress where you want to receive the alerts. Confirm the verification email.

- Now navigate to EventBridge console. Choose "Rules" under "Events" in the sidebar, and then choose "Create rule".

  ![Screenshot 2024-08-12 at 14-39-41 Create rule Rule detail Amazon EventBridge eu-central-1](https://github.com/user-attachments/assets/102d5f5d-0845-4c2b-97b3-47a518659e77)

  ![Screenshot 2024-08-12 at 14-47-43 Create rule Build event pattern Amazon EventBridge eu-central-1](https://github.com/user-attachments/assets/e3791550-c212-43b3-8afd-3460b9820ba4)

- Use the settings mentioned above. Choose the desired state(s) to have notifications about.

- In the "Target" section, use the settings mentioned below. Click on "Configure input transformer".

  ![Screenshot 2024-08-12 at 14-50-51 Create rule Select target(s) Amazon EventBridge eu-central-1](https://github.com/user-attachments/assets/79ba35d2-38ff-46e3-9a50-d7b549504a6e)

- In the "Target input transformer" tab, enter this as the input path: `{"instance-id":"$.detail.instance-id", "state":"$.detail.state", "time":"$.time", "region":"$.region", "account":"$.account"}`

  ![Screenshot 2024-08-12 at 14-49-07 Create rule Select target(s) Amazon EventBridge eu-central-1](https://github.com/user-attachments/assets/a57279dd-b48d-4ce3-8541-abf5f18d257d)

- Enter this as the template: `"At <time>, the status of your EC2 instance <instance-id> on account <account> in the AWS Region <region> has changed to <state>."`

- Leave the tags empty and select "Create rule".

  ![Screenshot 2024-08-12 at 14-51-39 Rules Amazon EventBridge eu-central-1](https://github.com/user-attachments/assets/cf842c20-b8b2-411f-b286-62632737856d)

- Et voilà ! It shall all be set up. Check by starting an EC2 instance.
  ![Capture](https://github.com/user-attachments/assets/a9319e48-4f12-4d0b-b4e1-163a79bebf1c)
