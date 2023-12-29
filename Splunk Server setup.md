# How to configure Splunk and set up Universal Forwarder to send logs Via Ec2

## Step 1 Downloading the necessary files

- Go to this website to register for Splunk to download the files you will need:https://www.splunk.com/en_us/download/splunk-cloud.html
  it should look like this:
  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/3b1c947c-9413-4834-b3ae-1019d8b5b4dd)

- Once registered, you will go to the Linux section and click the .tgz file to download, but we are going to use the wget link to pull it through the Command Line 
  it should look like this:
 ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/996596ee-cdb1-4bda-9d3f-f5c69d9bc4bb)

 ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/7bdb440b-34b8-4a80-91c7-afb6f353ed66)

 ## Step 2 Setting up Splunk 

 - We are going to make a directory where we are going to install Splunk. The command will be
   ```sh
   sudo mkdir /opt/splunk/
   ```
- It should look like this:

   ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/f1bd1fae-2de6-4dbc-94f9-40535bbb36b3)

- Once created, cd into the directory. We are going to change the ownership of the directory to the current user, who is
  ec2-user, the command for that will be:
  ```sh
  sudo chown ec2-user /opt/splunk/
  ```
- it should look like this:

  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/adf84544-e38c-4473-8d51-a9f2f29508a4)

- Next, we are going to use the wget command we got from the website to download Splunk into that directory
  it should look like this:
  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/ff98da46-7124-4004-9a1d-5afcff0607eb)
  
- if it was successful, the output should look like this when you run the ls command:
![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/7d3e2eff-6f51-4e52-8169-ef84d854e2d5)

- Next, we are going to untar the contents of the file in the directory with this command:
  ```sh
  tar -xzvC /opt -f (name of the splunk file)
  ```
  It should look like this:
  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/33385619-7354-499f-83c6-711609afa885)

- once it's completed, we are going to start the service, and the command to do that is:
  ```sh
  sudo /opt/splunk/bin/splunk start --accept-license
  ```
  You are going to be prompted to put in a username and password to be able to log into the Splunk webpage. It should look like this:

  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/50e4de36-93dd-4f2e-8698-58e47ff81432)

  Once you have done that, you should get an output that looks like this:
  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/3e00ea6d-a1af-40a4-8deb-17364fce8509)

- you will copy the link it gives you once the service is started, and you can input that into your web browser to access the page. I also forgot to mention that you must have port 8000 open since Splunk uses that  port number.
- you will be prompted to enter the username and password you created. It should look like this:

![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/49c26c6a-c649-48ea-bc85-55c65b60c653)

- Once you log in successfully, your page should be this.  Congrats

   ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/20783708-56ed-4161-b376-3550fb085723)


## Step 3 Configuring Universal Forwarder

- you're going to go into settings, and under settings, you'll click forwarding and receiving. Under receive data click add new. It should look like this:
  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/d062097c-c41c-475a-af62-d6489d9857f4)

  

  


  

  


   
