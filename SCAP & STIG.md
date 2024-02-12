# How to SCAP & STIG Windows Server 2022 Via AWS EC2


## SCAP & STIG explained

- It is usually used in the DOD (Department of Defense) to harden their Information systems.
 Plus, enterprises follow a checklist to improve their cybersecurity posture.
It helps automate and streamline known vulnerability analysis, security configuration verification, and report generation.


### Step 1 Needed files 

-  go to this website: https://public.cyber.mil/stigs/scap/
-  You are going to download a couple of files. The first file you will need to get is the SCAP tool for
  Windows. The current version is SCC 5.8 Windows. It should look like this:
 ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/a55dc606-f948-4d21-8690-b929984ba21d)

- Next, you are going to get the benchmarks for the SCAP, and this will be for Windows Server 2022
  it should look like this:
  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/b824af5e-862a-40f8-bb0e-9536e6a8eceb)

- Next, we are going to download the GPO (Group Policy Objects), which will help automate a lot of these checks
  it should look like this:
  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/4aaa7787-c979-431c-8e32-fadc2a26dad1)

- Next, we are going to download the manual benchmarks for the STIG for Windows Server 2022
  It should look like this:
  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/b7ea6700-b545-4bca-8ca4-150e6251639f)

- Next, you are going to download the STIG viewer
  It should look like this:
![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/d58de2c0-d37e-4af9-ab54-e568911a158f)

- Lastly, we will Download Microsoft's LGPO to import our GPO, which we downloaded earlier to help automate many configurations.
- here's the link: https://www.microsoft.com/en-us/download/details.aspx?id=55319

   It should look like this:
  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/1a076001-0e7a-4f76-81d1-db9fe0b91ab8)

## Step 2 Run SCAP


- We are going to run our SCAP tool. Once it opens up, you will delete the preloaded benchmarks because they are sometimes out of date
  and install the SCAP benchmark we got. It should look like this: 
![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/bfaf1299-2e3d-4ae5-a3b0-904b074658b5)

- Next, we are going to go into the options tab and change the output directory of the scan to a place that's easy for you to find the results
  It should look like this:
  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/4ff24002-216f-449c-9eeb-70086268cda6)

- Next, we will scan the system to see where we are at. When it comes to compliance, you will hit scan.
  Once finished, you should get a result with a score that should look like this:
  ![Screenshot 2023-12-17 112932](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/fd96ac1f-98f3-4b6d-bf53-1169023ec61e)

- Next, we are going to run STIG viewer and hit open, and then you will locate the manual STIG benchmarks we got earlier and load them.
  It should look like this:
  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/d73357f5-774e-4e70-9f45-b490da5ab6c7)

  Then, you are going to create a checklist by hitting the circle icon, which should look like this:
  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/cbc24907-064c-4350-a266-d5ed09e0b5f5)
  Save it after

 - Next, you are going to hit view results from the SCAP scan and then right-click on the scan session and click open summary  to see the results
   it should look like this:
   ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/178f38b6-b8d5-41cd-8a6f-a10d77b2af96)

   once it opens in the browse under the error header, click HTML, and you will be able to view all the errors
   which will look like this:
   ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/d1499009-d508-4f29-86d7-4420369cfd10)

## Step 3 Importing results to STIG viewer 

- In STIG Viewer, you are going to import the scan results from the SCAP scan drill down in the results folder to find the XML. This will add color to the manual benchmarks to put them in order of highest priority to loweset 
  (CAT I, CAT II, CAT III).

- CAT I: most at risk of serious exploitation. If exploited by a malicious attack, these vulnerabilities are the most significant threats to the wider network. If unchecked (High Risk)
- CAT II: settings or vulnerabilities that potentially result in a cybersecurity issue. Although the risk of an incident is still high, CAT 2 would not cause an immediate loss in the system (Medium Risk)
- CAT III: r settings that lower the defenses of a system or network if left unchecked. These heighten the risk of cybersecurity attacks or system failure but will not lead directly to either. (Low Risk)



   It should look like this:

  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/bf4dc691-1eda-4262-b9bc-ba5f2f123585)

  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/0b747039-e0da-4911-87d7-1dd6fce3545b)

  
  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/2c199c6c-88c4-429e-98f3-762f3b4797d6)


## Step 3 Importing GPOs to automate and remediate


- we are going to run Microsoft LGPO to import the GPOs we downloaded earlier. Locate where you saved it, copy the path in CMD, and put cd before the path to go into the directory. It should look like this:

  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/1fed2c74-1976-49c4-b3b5-812c440b6fee)

- Once you are in the directory, type lgp and hit tab to autocomplete it. It should look like this:
  ```sh
  LGPO.exe /g ""
  ```
  The /g flag is used to Import settings from one or more Group Policy backups 
  in the quotation marks; we are going to put the Path of the GPOs we downloaded. There will
  be two folders, one for users and another for computers. It should look like this:

  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/8c51f296-6b30-41e8-8476-a705cbc993c7)

- I ran this command first
  ```sh
  LGPO>LGPO.exe /g "C:\Users\Administrator\Desktop\IT STUFF\U_STIG_GPO_Package_October_2023\DoD WinSvr 2022 MS and DC v1r4\GPOs\{0868DCD3-069B-4027-89A9-995435DC3064}"
  ```
  It looks like this: 
  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/27849903-34e3-4e39-80cf-1f64d416cde0)

  Next command is this:
  ```sh
  LGPO.exe /g "C:\Users\Administrator\Desktop\IT STUFF\U_STIG_GPO_Package_October_2023\DoD WinSvr 2022 MS and DC v1r4\GPOs\{46680758-56F4-4673-9D15-1AF560115185}"
  ```
  It looks like this:
  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/ed8544e5-0f63-4a9b-8457-a92b75739b9a)

  Now since we updated the Group Policies, we need to update them. The command we will use is
  ```sh
  gpupdate /force
  ```
  ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/de86f73b-f725-4dff-a2c3-813da11e16fb)

 ##Finally RESCAN

 - we will do a SCAP rescan of our system to see how much we are in compliance from before. Our goal is to get over a 90%
 - here are the results of our rescan
   ![Screenshot 2023-12-17 095016](https://github.com/Jec-Ooro/AWSCloudJourney/assets/32017967/f972b35d-49c5-44cf-8702-7eb0fdbf4235)





# Congrats we successfully SCAP'D & STIG'D our Windows Server 2022 over 90%  


  

  


  
  

  

   


  

   

  
  



  


