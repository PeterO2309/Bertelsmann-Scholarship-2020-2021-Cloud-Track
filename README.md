# Bertelsmann-Scholarship-2020-2021-Cloud-Track

3.5-Months-of-Bertelsmann-Scholarship-Cloud-Track

# Day 1 of #60DaysOfUdacity (Friday, December 11th, 2020)

I completed the Lesson 1 in the cloud track "Introduction to Microsoft Azure Development". Basics and history of cloud computing learnt.My tools and environment is set up for configuration and deployment.

- Signed up for an Azure free account https://azure.microsoft.com/en-us/free/ 
- Created a Git repository for this program. 
- Installed python 3.6.
- Downloaded visual studio code editor https://code.visualstudio.com/
- Installed Azure CLI tools for VS Code https://marketplace.visualstudio.com/items?itemName=ms-vscode.azurecli 
- Instaled Azure CLI for my terminal https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest

# Day 2 of #60DaysOfUdacity (Saturday, December 12th, 2020)

https://docs.microsoft.com/en-us/learn/modules/intro-to-azure-compute/?WT.mc_id=udacity_learn-wwl

Learnt about the core cloud services _ Azure compute options which is topic 2 of 16 of Lesson 2. It talked about 
- Esssential Azure compute concepts.
- Azure VMs.
- Containers in Azure. 
- Azure App Service.
- Severless computing in Azure. 

# Day 3 of #60DaysOfUdacity (Sunday, December 13th, 2020)

I successfully set up a resource group in the Azure Portal by following the process below highlighted in the lesson:
- Go to the Azure Portal homepage https://portal.azure.com/#home
- Click "Create a Resource Group"
- Search for "Resource group" and click "Create"
- Selected the subscription for the resource group, named it, and selected a region.
- Make sure once you select "Review and create" to actually review the information! While it doesn't take too much time to go back and create a new resource group, you'll want to check for any typos in the name or if the wrong region was selected. When we work out of Azure CLI later, this becomes even more important, as you could cause other scripts to fail if things are named incorrectly or are in an inappropriate region.
- Click "Create" once you are done reviewing.

- View screenshot here.
https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day03.PNG 
https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day03_2.PNG

- Dashboard showing the created resource groups.
https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day03_3.PNG


# Day 4 of #60DaysOfUdacity (Monday, December 14th, 2020)
Created a Resource Group using the Azure CLI via the command prompt by doing the following steps.
- Installed Azure CLI on Windows using this steps https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli and the CLI documentation https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest&WT.mc_id=udacity_learn-wwl
- Typed  "az login" on the terminal to login to the Azure CLI.
- Used "az account list-locations -o table" to see the list of all locations which was listed in a table format. 
- Used the Azure CLI command "az group create" and passed in two flags:
    resource group --name
    --location which is the same as the "region" field on the Azure portal.
- Therefore, created my resource group in the West US 2 region with the name "resource-group-west-using-cli":
- The command "az group create --name resource-group-west-using-cli --location westus2"
- Viewed all created resource groups using both portal and cli via https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups. See screenshot via https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day04_1.PNG
https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day04_3.PNG
https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day04_4.PNG


- Learnt some of the differences between Virtual Machines(IaaS) and App Services(PaaS). Also, the benefits and disadvantages of each of them. 


# Day 5 of #60DaysOfUdacity (Tuesday, December 15th, 2020)
Created a Linux Virtual Machine and deployed it on Azure using the following steps.

1. Go to the homepage, click "Create a resource"
2. Click on "Compute" in the left menu
3. Click on "Virtual Machine"
4. Create a Linux VM with the following details:

```markdown
- Subscription: Used my default subscription.
- Resource Group: "hello-world-rg"
- VM Name: "linux-vm-west"
- Region: West Europe
- Availability Options: Used default option of "No infrastructure redundancy required".
- Image: Used the latest version of Ubuntun Server, 18.04 LTS
- Azure Spot instance: No
- Size: Clicked on "Select Size" and select "Standard B1ls"
- Authentication type: Password
- Username: Used "udacityadmin"
- Password: Used "Udacityadmin@123"
- Inbound Port Rules: "Allow Select Ports" and make sure from the drop-down menu, 22 and 80 are selected.
- Clicked on "Review create", then "create". 
- Virtual Machine is successfully deployed. 
```

5. Screenshot: https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day05_1.PNG
https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day05_2.PNG


# Day 6 of #60DaysOfUdacity (Wednesday, December 16th, 2020)
D6:  After watching the video in Lesson 2, Lecture 9, I tried severally to connect to the created VM, following the steps highlighted, still no success. I copied the basic flask app from my local machine to the VM by using the command "scp -r <SOURCE-DIR> [ADMIN-NAME]@[PUBLIC-IP]:<TARGET-DIR>"  i.e "scp -r ./web udacityadmin@40.68.58.33:/home/udacityadmin". 

After the completion, connected to the VM using "ssh [ADMIN-NAME]@[PUBLIC-IP]", installed Python Virtual Environment and NGNIX to use as a reverse proxy. 

However, still having issues with configuring Nginx to redirect all incoming connections on port 80 to our app that is running on localhost port 3000

# Day 7 of #60DaysOfUdacity (Thursday, December 17th, 2020)
D7: I finally deployed the flask template app to the VM. I used the admin username "udacityadmin" i set when creating the VM and also the public IP address of my VM (51.143.34.63). Then used the following command to grab the IPs addresses for the particular VM from the CLI— "az vm list-ip-addresses -g <RESOURCE-GROUP> -n <VIRTUAL-MACHINE-NAME>" or use Azure portal. I used GitBash CLI
    
   These are the steps to copy the basic Flask app from my local machine to the VM.
1. Used the secure copy utility. NOTE: The first time you try connecting to the VM, you'll see a message, answer 'yes' to permanently add the IP address to the list of known hosts.
    ```markdown
    scp -r ./web udacityadmin@51.143.34.63:/home/udacityadmin
    ```
2. After the files have been copied to the VM, connect to the VM using—ssh [ADMIN-NAME]@[PUBLIC-IP]
     ```markdown
    ssh udacityadmin@51.143.34.63
    ```
3. We can use ```ls``` to see the web directory we just uploaded.
4. Python 3 is already installed on the VM. Install Python Virtual Environment and NGNIX to use as a reverse proxy
     ```markdown
    sudo apt-get -y update && sudo apt-get -y install nginx python3-venv
    ```
 5. Before we run the app, we have to configure Nginx to redirect all incoming connections on port 80 to our app that is running on localhost port 3000.
        - By default, Nginx has a default page that is displayed. If you visit the public IP address in your browser, you should see this page rendered.
        - Navigate to the /etc/nginx/sites-available directory using this command — ```cd /etc/nginx/sites-available```
        - Unlink the default site using ```sudo unlink /etc/nginx/sites-enabled/default```
        - Create a new file reverse-proxy.conf in the /etc/nginx/sites-available— ```sudo vim reverse-proxy.conf```
        - Add the following code to this file:
     ```markdown
        server {
            listen 80;
            location / {
                proxy_pass http://localhost:3000;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection keep-alive;
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
            }
        }
    ```
 - Activate the directories by creating a sym link to the /sites-enabled directory 
    ```markdown
    sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/reverse-proxy.conf
    ```
 - Restart nginx so the changes take effect. ```sudo service nginx restart```
    
    
 6. cd to ```web``
 7. Create venv ```python3 -m venv venv```
 8. Activate the env ```source venv/bin/activate```
 9. Upgrade pip in our virtual environment and then Install dependencies ```pip install --upgrade pip``` ```pip install -r requirements.txt```
10. Run the app ```python application.py```
11. In the web browser, visit the public IP address of the VM (51.143.34.63) and you should see the application. Type "exit" to disconnect from the VM.
12. See screenshots: https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day07_1_VM_deployed.PNG https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day07_6_connected_to_VM_via_external_source.PNG https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day07_12.PNG
    

# Day 8 of #60DaysOfUdacity (Friday, December 18th, 2020)
Created a Linux VM using Azure CLI doing the following steps. 
1. Login to Azure portal using ```az login```.
2. Create our VM. 

```markdown
az vm create -n linux-vm-west -g resource-group-west --image UbuntuLTS --location westus2 --size Standard_B1ls --admin-username udacityadmin --generate-ssh-keys --verbose
```

Which is same as 

```markdown
az vm create \
   --resource-group "resource-group-west" \
   --name "linux-vm-west" \
   --location "westus2" \
   --image "UbuntuLTS" \
   --size "Standard_B1ls" \
   --admin-username "udacityadmin" \
   --generate-ssh-keys \
   --verbose
```

3. Upon success, a JSON response is displayed.
4. open port 80 to allow outside traffic to our VM.

```markdown
az vm open-port --port 80 --resource-group resource-group-west --name linux-vm-west 
```

5. Upon success, a JSON response is displayed.


# CONNECTING TO THE VM

1. Use the following command to grab the IP address for the VM from the CLI. ```az vm list-ip-addresses -g resource-group-west -n linux-vm-west```
2. Copy a basic Flask app from my local machine to the VM by using the secure copy utility. ```scp -r ./web udacityadmin@52.247.233.222:/home/udacityadmin```
3. Connect to the VM with ```ssh [username]@[IP Address]```. In this case, ```ssh udacityadmin@52.347.233.222```.
    Run ```ls``` to see the web directory we just uploaded.
4. Install Python Virtual Environment and NGNIX to use as a reverse proxy ```sudo apt-get -y update && sudo apt-get -y install nginx python3-venv```
5. Before we run the app, we have to configure Nginx to redirect all incoming connections on port 80 to our app that is running on localhost port 3000.
        - By default, Nginx has a default page that is displayed. If you visit the public IP address in your browser, you should see this page rendered.
        - Navigate to the /etc/nginx/sites-available directory using this command — ```cd /etc/nginx/sites-available```
        - Unlink the default site using ```sudo unlink /etc/nginx/sites-enabled/default```
        - Create a new file reverse-proxy.conf in the /etc/nginx/sites-available— ```sudo vim reverse-proxy.conf```
        - Add the following code to this file:
     ```markdown
        server {
            listen 80;
            location / {
                proxy_pass http://localhost:3000;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection keep-alive;
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
            }
        }
    ```
 - Activate the directories by creating a sym link to the /sites-enabled directory 
    ```markdown
    sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/reverse-proxy.conf
    ```
 - Restart nginx so the changes take effect. ```sudo service nginx restart```
    
    
 # DEPLOYING THE APP TO THE VM
 6. cd to ```web``
 7. Create venv ```python3 -m venv venv```
 8. Activate the env ```source venv/bin/activate```
 9. Upgrade pip in our virtual environment and then Install dependencies ```pip install --upgrade pip``` ```pip install -r requirements.txt```
10. Run the app ```python application.py```
11. In the web browser, visit the public IP address of the VM (51.143.34.63) and you should see the application. Type "exit" to disconnect from the VM.
