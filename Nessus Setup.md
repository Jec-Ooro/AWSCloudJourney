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
  
## Step 3 Nessus Expert setup

- Once you type the URL. You will be brought to the Setup webpage, and you will select Register for Nessus Expert
- When it's done initializing after the setup, you will be brought to the homepage. It should look like this:

![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/841fb3b1-0c91-4db4-97a7-a6d0900a11b5)

- Next, we will go to my scans and click Create a new scan. We are going to select advanced scan since it's going to be a credentialed scan on our second
  EC2 instance. It should look like this: 

![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/da120602-1d1a-45fb-aa37-094f0d8a5ddc)

You must allow port 8834 to go through for your inbound rules on the second EC2 instance for it to communicate with Nessus.
  
- Now, we will set up a name in the name section and the target section; you will put the IP address of the host, and we will run the scan against  

![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/a0844a9b-1525-446c-a1bd-32e9b76f5ba1)

## Step 4 Credential scan set up 

- We will click credentials, and in that tab, we will select SSH. This is how we are going to set up the scan
  It should look like this:  

![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/e5dcfc25-991d-47f9-aa00-d462e7489a7f)

- Next, we will follow this link:https://community.tenable.com/s/article/SSH-Public-Key-Authentication?language=en_US
  to set up SSH public key authentication for scanning our second EC2 running redhat.

- Log on to our second EC2 instance through SSH, and we will follow the document, but we will go away from it in certain parts to achieve the same result
- First, we will create a user using the useradd command and passwd for a password It will look like this:
  ```sh
  useradd (whatever name you want)
  passwd (whatver name you want) 
  ```
![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/bd2cee6e-8c33-46e8-b520-b6c670f55fdb)

- Additionally, we will make a directory labeled /home/cat_man/.ssh. We will do this with the mkdir command:
  It will look this:
  ```sh
  mkdir /home/cat_scan/.ssh
  ```
![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/c5055c32-e565-49f9-b306-900c9695e1e8)

- Next, we will now need to create an SSH key pair. It will create a public and private key. We are going to need to get the key into our second EC2 instance, which will be the public key
  but the private key will be used for Nessus in the credentialed section.

- We are going to create the Key pair in Powershell, and the command to do that is:
  ```sh
  ssh-keygen -t ecdsa -m pem
  ```
  You are going to hit enter until you get your randomart image it should look like this:
![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/9ffd3a95-f4de-4f48-bf69-5906435b0e20)

- it created two files, private and public keys, but to work on Nessus, it has to be a .pem file extension. We are going to change it to that.
  We are going to go to the location where they are saved, open the id_ecdsa file, which is the private key with Notepad, choose save as, and change the extension
  to .pem it should look like this:

![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/fdf146ad-bf28-4d43-b619-eebeeb1926ff)

- Once you save the file, we are going to go back to Nessus and put the username and the .pem file we just created in the credential tab
  It should look like this:

![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/f234db8b-6579-4c3a-8aef-36070d88725e)

## Step 5 Moving the public key to our second EC2 instance

- We will move the .pub file and the public key to our second instance using the S3 bucket.
  The command to that is:
  ```sh
  aws s3 cp my_copied_file.ext s3://my_bucket/my_folder/my_file.ext
  ```
![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/13531615-ac9a-453c-8b1a-641942bfad07)

- Once that is uploaded, we will go to our second EC2 instance and download it. The command for that is:
```sh
aws s3 cp s3://my_bucket/my_file.ext my_copied_file.ext
```
![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/8223689c-2bcd-4610-98ef-90251571f25b)

- Next, we will go back to the document; we need to create an authorized_keys file in the directory we made earlier and add the public key.
  It should look like this:
![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/624e45dd-e044-41ed-ae37-d2f736b8bb4e)

- Now, we will set the permissions on the files and directories we created. The commands will be:
  ```sh
  chown -R scan_man:scan_man /home/user-you-created/.ssh/
  chmod 0600 /home/user-you-created/.ssh/authorized_keys
  chmod 0700 /home/user-you-created/.ssh
  ```
  
![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/542191ee-d35d-4e8c-a032-eee38dacc875)

- Also, we will go back into the credential tab and set elevated privileges with sudo and you will also put the password of the user we created in sudo password.\
  it should look like this:

![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/517e479d-3178-45ff-80ad-5fc07d50d467)


## Step 6 Run the scan 

- We will run the scan to get the results. Here is the completed scan:

![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/87e4189b-d2bb-4601-bbd0-f28d645b525c)

As you can see, it was also a credentialed scan, and to check if it was for sure, you can go to the vulnerabilities. Then hit filter and 
In the drop-down menu, find the plugin ID and type 19506.

![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/5751cd85-5e30-4322-8674-4e2bd8498e09)

- You will open the result and expand the output, and you should look for this:

![294723852-b608486d-20d9-4a12-a787-29cb6ed3c283](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/e2fc24ae-3215-461b-ab7f-2db17c8b8ebf)

- It was a successful credentialed scan

## Congrats, you just set up a credentialed vulnerability scan with Nessus on your Redhat 9 EC2




  
   
  




  
  



   
  

  
  


   
