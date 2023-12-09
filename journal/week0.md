#  Creating a billing alarm in AWS through GitPod(CLI) 

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

## Create Alarm

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

## Congrats you made your SNS Topic utilizing Cloudwatch alarms  
```sh
- Resoruces used AWS Documentation, ChatGPT
```




 
 
