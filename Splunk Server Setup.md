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

- you're going to go into settings, and under settings, you'll click forwarding and receiving. Under receive data, click add new. It should look like this:
  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/d062097c-c41c-475a-af62-d6489d9857f4)

- You will be prompted to enter a port number, and the port you will type in is 9997, which the forwarder will use to hit save.

- Next, you will go to the Splunk webpage as we did before and download the Universal Forwarder with the Wget link, which we will plug into the command line. It should look like this:
  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/65bdad69-2ab5-47d2-8525-4cd4ff7ced02)

- Once you get the Wget link, go into the Command line of your second EC2 and cd to the /opt folder. This is where we will install the Universal Forwarder. It should look like this:
  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/c5842859-b857-455b-a092-73800b1df6d6)

- Once we download it, we are going to untar the file with this command:
  ```sh
  sudo tar xvzf (name of the universal forwarder) -C /opt 
  ```
  It should look like this:
  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/3aed08be-e93c-442f-bc9b-e27f389db753)

- Next, you're going to cd /opt/splunkforwarder/bin and start the service, and it should look like this:
    ```sh
    sudo /opt/splunkforwarder/bin/splunk start
    ```
    ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/5edef0fc-87ed-465f-b2c6-3144a18619b3)
    ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/8f919031-bff1-4698-9c50-668afcfe9840)

- Next, we will Configure a Forwarder connection to the Index Server. The command will be this:
    ```sh
    sudo /opt/splunkforwarder/bin/splunk add forward-server hostname.domain:9997
    ```
- If you are successful, you will  get a message that says this:

     ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/d393a2d8-4099-4617-a38d-0bca68ee1c09)

- Next, we will add /var/log files to be indexed by the server. The command for that will be this:
      ```sh
      sudo /opt/splunkforwarder/bin/splunk add monitor /var/log
      ```
- If you are successful, it should look like this:

    ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/a033d71a-62f6-4af0-91da-bc3bb365756d)

- Go back to your Splunk server and click Search your data:
  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/d6b3cc24-a84a-446a-bc79-da785fb8920e)

- Once you are in, find the data summary, click it, and if it was all successful, you should see your host with 
  IP address and the files you wanted to be indexed in the sources tab and it should look like this:

  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/372a56e0-78ea-435a-8a9f-5c05509d32ee)
  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/744d0302-c778-491b-88d3-9e0224331965)
  ![register ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/4e369534-0df9-4ed0-a0b6-8d34b70cffa8)



# Congarts we have successfully configured a Splunk Server and Universal Forwarder to receive logs 

  



    

  

  

  

  

  


  

  


   
