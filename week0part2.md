# Connect Health Dashboard to SNS via EventBridge for Real-time Service Notifications(AWS CLI via Gitpod)



## Create an SNS Topic


```sh
 aws sns create-topic --name(whatevernameyouwant).
```
 - this creates the sns topic that will be used to send notifications
 ![creating sns topic for put rule to subcribe too (2)](https://github.com/Jec-Ooro/aws-bootcamp-cruddur-2023/assets/32017967/fee8f1e8-9fd2-47af-aa3c-2fd4731f2278)
 - you should get an output like that for a TopicARN if successful as seen in the image

  ## Create The EventBridge Rule to detect Health Dashboard events


  - The put-rule command  creates an EventBridge rule that filters for Health Dashboard events.
    ```sh
    aws events put-rule --name HealthDashboardRule --event-pattern "{\"source\": [\"aws.health\"]}"
    ```
    ![put rule setup(2)](https://github.com/Jec-Ooro/aws-bootcamp-cruddur-2023/assets/32017967/c7c325f2-adaf-4d89-abee-27c47ffd1c8f)

   - The Black circle is important the ending of the command has to be in json format to work since  used to define parameters or filters when interacting with AWS services. Especially setting up EventBridge rules or filters.


## Create a Target for the Event Rule

- the EventBridge rule will forward matched events to the SNS topic.
  ```sh
  aws events put-targets --rule (whatever name you want)  --targets "Id"="1","Arn"="(SNS TOPIC ARN you got ferom creating the SNS Topic)"
  ```
  ![put targets --rule](https://github.com/Jec-Ooro/aws-bootcamp-cruddur-2023/assets/32017967/783a7c6b-65ed-45fc-8b10-737cdeb5d751)

- If you can't recall your SNS Topic ARN the command to show all sns topics: "aws sns list-topics"

  ## Subscribe an Endpoint to the SNS Topic

- Subscribe an email address or any other endpoint to the SNS topic to receive notifications.

  ```sh
  aws sns subscribe --topic-arn (SNS TOPIC ARN) --protocol email --notification-endpoint your-email@example.com
  ```
-  you should receive email that looks like this and hit confirm 
  ![aws put subscribe](https://github.com/Jec-Ooro/aws-bootcamp-cruddur-2023/assets/32017967/e05f8928-4914-4fd9-aa50-c7336e051153)


# Congratulations You Connect a Health Dashboard to SNS via EventBridge

```sh
Resources used AWS Documentation and ChatGPT
```

    
    



