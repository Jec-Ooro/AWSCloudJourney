#  Creating a billing alarm in AWS Via GitPod(CLI) 

## Create a SNS topic

- The SNS topic will deliver us alerts when we go over a certian amount.
-  Heres a link to help guide you on creating one [https://docs.aws.amazon.com/cli/latest/userguide/cli-services-sns.html]

 The command to create SNS Topic
```sh 
aws sns create-topic --name "whatever name you want"
```
![sns creation](https://github.com/Jec-Ooro/aws-bootcamp-cruddur-2023/assets/32017967/34a99497-7815-4cfd-9aa5-9292ecf94cb8)

after you run the command it will return you a TopicARN which you will neeed to create a subscription 

The command to subscribe to the Topic
```sh
aws sns subscribe  --topic-arn TopicARN(the one you got from creating the SNS Topic)   --protocol email  --notification-endpoint your@email.com
```
![sns subsribe](https://github.com/Jec-Ooro/aws-bootcamp-cruddur-2023/assets/32017967/0bf43df2-0018-439e-81a6-cef0c279a496)

After excuting the command you should get an email and hit subscribe and it should look like this 
![sns confirm](https://github.com/Jec-Ooro/aws-bootcamp-cruddur-2023/assets/32017967/33347616-7e59-4f7e-afca-017bfceb2012)

### Create Alarm

-  Heres a link to help guide you on creating one [https://docs.aws.amazon.com/cli/latest/reference/lightsail/put-alarm.html]
-  the command to create the alram and the paramaters I will use
  ```sh
aws cloudwatch put-metric-alarm   --alarm-name "BudgetExceededAlarm"  --alarm-description "Alarm triggered when budget exceeds threshold"   --namespace "AWS/Billing"  --metric-name "EstimatedCharges"  --statistic Maximum   --period 86400   --threshold 30.0   --comparison-operator GreaterThanThreshold   --evaluation-periods 1   --alarm-actions arn:aws:sns:us-west-2:123456789012:arn:aws:sns:us-west-:YourTopic --dimensions Name=Budget,Value=Budget
```
![alaram creation](https://github.com/Jec-Ooro/aws-bootcamp-cruddur-2023/assets/32017967/55de5a13-3951-41ad-8652-210821818385)

Once you run the command and it goes throuhgh correctly you can check
to see your cloud watch alarms that are on your account with this command 
```sh
aws cloudwatch describe-alarms
```
![cloudwatch output](https://github.com/Jec-Ooro/aws-bootcamp-cruddur-2023/assets/32017967/8a5d8d3e-4994-4c44-a7ab-df4390cb4b36)



### Logical Architecture Design
![lucid diagram ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/23900f58-21bf-4d14-a67e-cd570fd4824d)



# Challenge   

## Connect Health Dashboard to SNS via EventBridge for Real-time Service Notifications(AWS CLI via Gitpod)



### Create an SNS Topic


```sh
 aws sns create-topic --name(whatevernameyouwant).
```
 - this creates the sns topic that will be used to send notifications
 ![creating sns topic for put rule to subcribe too (2)](https://github.com/Jec-Ooro/aws-bootcamp-cruddur-2023/assets/32017967/fee8f1e8-9fd2-47af-aa3c-2fd4731f2278)
 - you should get an output like that for a TopicARN if successful as seen in the image

  ### Create The EventBridge Rule to detect Health Dashboard events


  - The put-rule command  creates an EventBridge rule that filters for Health Dashboard events.
    ```sh
    aws events put-rule --name HealthDashboardRule --event-pattern "{\"source\": [\"aws.health\"]}"
    ```
    ![put rule setup(2)](https://github.com/Jec-Ooro/aws-bootcamp-cruddur-2023/assets/32017967/c7c325f2-adaf-4d89-abee-27c47ffd1c8f)

   - The Black circle is important the ending of the command has to be in json format to work since  used to define parameters or filters when interacting with AWS services. Especially setting up EventBridge rules or filters.


### Create a Target for the Event Rule

- the EventBridge rule will forward matched events to the SNS topic.
  ```sh
  aws events put-targets --rule (whatever name you want)  --targets "Id"="1","Arn"="(SNS TOPIC ARN you got ferom creating the SNS Topic)"
  ```
  ![put targets --rule](https://github.com/Jec-Ooro/aws-bootcamp-cruddur-2023/assets/32017967/783a7c6b-65ed-45fc-8b10-737cdeb5d751)

- If you can't recall your SNS Topic ARN the command to show all sns topics: "aws sns list-topics"

  ### Subscribe an Endpoint to the SNS Topic

- Subscribe an email address or any other endpoint to the SNS topic to receive notifications.

  ```sh
  aws sns subscribe --topic-arn (SNS TOPIC ARN) --protocol email --notification-endpoint your-email@example.com
  ```
-  you should receive email that looks like this and hit confirm 
  ![aws put subscribe](https://github.com/Jec-Ooro/aws-bootcamp-cruddur-2023/assets/32017967/e05f8928-4914-4fd9-aa50-c7336e051153)


# Congratulations You Connect a Health Dashboard to SNS via EventBridge and Created a billing alaram

    
    








 
 
