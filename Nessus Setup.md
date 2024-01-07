# Setting up Nessus via AWS EC2 to discover vulnerabilities

## Step 1 Download the necessary file
- Go to this website:https://www.tenable.com/downloads/nessus?loginAttempted=true
- Register, and it should bring you to the download page, which should look like this:
  ![NEssus ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/4f82fc49-5ce9-424d-8698-dad773f3f737)

- We are going to download the (Linux - RHEL 9 - x86_64) version and put it into our S3 bucket and 
  move it into our EC2. It should look like this:

  ![NEssus ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/f0ae0258-43f2-4604-82e3-779f0b7f4a3c)

- Log into your EC2 instance and go to the Command Line. and the command you will use to copy contents
  from your S3 bucket to your EC2 instance is
  ```sh
  aws s3 cp s3://my_bucket/my_folder/my_file.ext my_copied_file.ext
  ```
  It should look like this:
![NEssus ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/dfbb130f-4f66-484a-83ef-1340df854eab)

## Step 2 Installing Nessus

- Once you have the RPM file, we will install Nessus. we are going to do it with this command
  ```sh
  sudo yum install /path/on/eC2/Nessus-10.6.3-es9.x86_64.rpm
  ```
  It should look like this:

  ![NEssus ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/a0cc55fa-1602-418c-8533-c79d14011394)

  ![NEssus ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/47f39dd7-b8ad-42a5-83b6-d8627b3b3a4f)

- Next, we will start the service using the command in the image above, then go to our browser and type in the URL.
  
## Step 3 Nessus Essentials setup

- Once you type the URL. You will be brought to this webpage, and you will select Register for Nessus Essential
  It should look like this:

  ![NEssus ](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/b608486d-20d9-4a12-a787-29cb6ed3c283)


   
  

  
  


   
