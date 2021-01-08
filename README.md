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
- Viewed all created resource groups using both portal and cli via https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups. 


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
   -After inserting, click ```esc```, then ```shift + :```, then type ```wq!``` then press ```enter```
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
    

# Day 8 of #60DaysOfUdacity (Friday, December 18th, 2020)
Created a Linux VM using Azure CLI doing the following steps. 
1. Login to Azure portal using ```az login```.
scnshot: https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day08_01_login_to_azure.PNG 
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
6. VM appears on portal. 


## CONNECTING TO THE VM

1. Use the following command to grab the IP address for the VM from the CLI. ```az vm list-ip-addresses -g resource-group-west -n linux-vm-west```
screenshot: https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day08_08_get_ipaddress_of_vm.PNG

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
 -After inserting, click ```esc```, then ```shift + :```, then type ```wq!``` then press ```enter```
 - Activate the directories by creating a sym link to the /sites-enabled directory 
    ```markdown
    sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/reverse-proxy.conf
    ```
 - Restart nginx so the changes take effect. ```sudo service nginx restart```
 
    
    
 ## DEPLOYING THE APP TO THE VM
 6. cd to ```web``
 7. Create venv ```python3 -m venv venv```
 8. Activate the env ```source venv/bin/activate```
 9. Upgrade pip in our virtual environment and then Install dependencies ```pip install --upgrade pip``` ```pip install -r requirements.txt```
10. Run the app ```python application.py```
11. In the web browser, visit the public IP address of the VM (52.347.233.222) and you should see the application. Type "exit" to disconnect from the VM.

 ## DELETING A RESOURCE GROUP
 If we no longer need a resource, we can delete them through the portal. The quickest way to do this from the CLI is to delete the resource group. This will delete all resources in that group
```markdown
az group delete -n resource-group-west
```

# Day 9 of #60DaysOfUdacity (Saturday, December 19th, 2020)
I took the following steps to create an App Service Web App using the Azure Portal.

- On the homepage, click "Create a resource"
- Search for "Web App"
- Click "Create"
- Select your subscription
- Select your resource group "resource-group-west"
- Enter a name for your web app—This needs to be a unique name and is unique to Azure as a whole and not just your Azure account. I used "hello-world1234" as my unique name.
- For Publish, select "Code"
- For the "Runtime Stack", select "Python 3.7" or greater.
- For the "Operating System" select "Linux"
- Select a region for your app service
- Create a new App Service Plan. You can keep the default name Azure gives you or you can create your own name.
- For SKU and size, select "F1" (Free).
- Click "Review + Create"
- Click "Create"

## Deploy an App Service from a GitHub repository
- Create a new repo and push the web app code to the repo
- On Azure portal in the Deployment Center.
- Go to Deployment Center
- Choose GitHub
- Choose org and repo
- Go through the prompts; deployment takes a few minutes
- Go to URL of web app and should see the app deployed

## Cleanup
If we no longer need a resource, we can delete them through the portal.

- From the homepage, click on "Resource Group".
- Click on the resource group you want to manage.
- You have two options—"Delete resource group" or if you want to keep the resource group, you can click on the individual or collection of resources you want to delete and click on "Delete".


# Day 10 of #60DaysOfUdacity (Sunday, December 20th, 2020)
D10: I started the Udacity "Version control with Git" course to refresh my knowledge of Git. 
Screenshots: https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day10_Git.PNG 
https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day10_2.PNG


# Day 11 of #60DaysOfUdacity (Monday, December 21th, 2020)
This is an alternative approach to deploy an app service.

## Steps to Create and Deploy an App Service Web App from a Directory using Azure CLI:
- Sign in to Azure ```az login``` using IDE or CMD. 
- cd to web directory ```cd web/```
- Run the following command:
```markdown
    az webapp up -g hello-world-rg -n hello-world-mine-xyz --sku F1 --verbose
```

or 

```markdown
az webapp up \
 --resource-group hello-world-rg \
 --name hello-world-mine-xyz \
 --sku F1 \
 --verbose
 ```
 
 - launch the app using the URL (in this case, http://hello-world-mine-xyz.azurewebsites.net)
 - If you want to update your app, make changes to your code and then run (Note: this may not update new requirements you may have added):
 ```markdown
    az webapp up \
    --name hello-world-mine-xyz \
    --verbose
 ```
 
 ## Cleanup
 If we no longer need a resource, we can delete them through the portal. The quickest way to do this from the CLI is to delete the resource group. This will delete all resources in that group
```markdown
    az group delete -n hello-world-rg
```

Alternatively, if you want to just delete the App Service and App Service plan individually, you can do so with the following commands:

## Delete an App Service
```az group delete --name hello-world-mine-xyz --resource-group hello-world-rg```
or 

```markdown
    az webapp delete \
        --name hello-world-mine-xyz \
        --resource-group hello-world-rg
```

## Delete an App Service plan
```markdown
    az appservice plan delete \
        --name [App Service Plan Name] \
        --resource-group hello-world-rg
```

## Creating an Azure SQL Database in the Portal
To create an Azure SQL Database in the Azure Portal:

1. Find the "SQL databases" service in Azure.
2. Click "Create SQL Database".
3. Select the appropriate subscription and resource group (likely “resource-group-west”).
4. Enter a database name.
5. If you already have a SQL server, you can use it; however, you likely need to click "Create New".
    If creating a new SQL server, enter a server name, and then admin and password("pc-pwd") - make sure you can remember these, or you will not be able to access the server         when necessary. The admin name cannot just be "admin".
6. Set the location to match the resource group.
7. Keep SQL elastic pool on the default of "No".
8. Under Compute+Storage, click on "Configure Database". While General Purpose won't end up charging you anything for the short time the server is live for these exercises, you    might as well press "Looking for basic, standard, premium?", and change it to "Basic".
9. Press the "Next: Networking" button, then select "Public Endpoint", and set both of the Firewall rules that appear to "Yes". This will allow us to more easily access the SQL    database later on within our app.
10.Click "Review + Create" and then "Create" to create the database, then wait for it to deploy.

## Adding Data to Database
To add data to the SQL Database, I performed the following:

- Once the SQL database is deployed, click on its name to access it (you may need to go back to the main "SQL databases" page in Azure).
- Click on the "Query editor" in the left side menu, and then log in with my SQL Server credentials.
- I pasted the query from my ```animals-table-init.sql``` script into the query window, and hit "Run"; you should see ```Query succeeded: Affected rows: 3```.
- On the left side of the query window, I clicked on the "Tables" folder, and double-checked that the ```dbo.POSTS``` table was successfully created with the correct fields.
- I ran a new query with SELECT * FROM animals, to see the three posts listed.

## Create an Azure SQL Database using Azure CLI.

### Create SQL Server
```markdown 
    az sql server create \
    --admin-user udacityadmin \
    --admin-password p@ssword1234 \
    --name hello-world-server \
    --resource-group resource-group-west \
    --location westus2 \
    --enable-public-network true \
    --verbose
 ```

### Create Firewall rule
Next, we have to create two firewall rules. These are the same two rules we checked as yes when we used the portal.

The first one is to allow Allow Azure services and resources to access the server we just created.

```markdown 
    az sql server firewall-rule create \
    -g resource-group-west \
    -s hello-world-server \
    -n azureaccess \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 0.0.0.0 \
    --verbose
 ```

This second rule is to set your computer's public Ip address to the server's firewall. You'll need to find your computer's public ip address for this part.

On macOS, use the command curl ifconfig.me; you can use ipconfig in the command prompt if you are on Windows.

### Create clientIp firewall rule
```markdown
    az sql server firewall-rule create \
    -g resource-group-west \
    -s hello-world-server \
    -n clientip \
    --start-ip-address <PUBLIC-IP-ADDRESS> \
    --end-ip-address <PUBLIC_IP_ADDRESS> \
    --verbose
```
### Create SQL Database
Finally, to create the database itself, I used the below command.

```markdown
    az sql db create \
    --name hello-world-db \
    --resource-group resource-group-west \
    --server hello-world-server \
    --tier Basic \
    --verbose
```

### Adding Data
We'll again add data to the database through the portal, as that's the most straightforward method for now (until we connect to an app).


### Cleanup
You can find the CLI commands for cleaning up the SQL resources below.

### Delete DB
```markdown
    az sql db delete \
    --name hello-world-db \
    --resource-group resource-group-west \
    --server hello-world-server \
    --verbose
```

### Delete SQL Server
```markdown
    az sql server delete \
    --name hello-world-server \
    --resource-group resource-group-west \
    --verbose
```

# Day 12 of #60DaysOfUdacity (Tuesday, December 22th, 2020)
D12: Day 12 of #60daysofudacity

Today, I created a blob storage, blob container via the Azure portal.
- Added images to the container.
- Viewed and downloaded the images. 
- Deleted the storage account.
- I also did the above steps using the Azure CLI.

## Creating Blob Storage in the Portal

To create a blob storage account on Azure Portal, I did the following:

- Click Create a resource
- Search for storage account
- Select the appropriate subscription and resource group (in this case “resource-group-west”).
- Enter a storage account name, note—it can only be lowercase letters and numbers. “helloworld1234mine”
- Set the location to West US 2 to match the resource group "Europe West".
- Leave "Performance" as Standard, while making sure "Account kind" is StorageV2. This could also be BlobStorage, but StorageV2 is preferred.
- We’ll leave replication/redundancy on the default setting.
- Click "Next: "Advance".
- Set "Access tier" to Cool - in a live production app, you may need this to be Hot, but in our case, Cool will work just fine.
- Then set "Blob public access" to "Enabled
- Click "Next: Networking" to confirm that the storage account is using a Public endpoint (all networks)
- Click "Next: Data Protection".
- Click "Review + Create" and then "Create" to create the database, then wait for it to deploy.

## To add a Blob Container called images:

- Once the Storage account is deployed, click on its name to access it (you may need to go back to the main "Storage accounts" page in Azure).
- Click on the "Containers" button in the storage account's "Overview" page.
- Click "+ Container", then add the name of images.
- Set "Public access level" to "Container(anonymous read access for containers and blobs)", and click "Create".
NOTE: I had to refresh my page a few times before I could access the container.

## Adding Images to the Container
To add an image to the Blob Container:

- Click on the container named "images".
- Click "Upload", and add an image of your choosing.
- Once the image appears within the container view, click on it, and copy the "URL" property.
- Paste the URL into your browser to see if the image appropriately loads.
You can also download the file from here as well

## Cleanup
If we no longer need a resource, we can delete them through the portal.

- From the homepage, click on "Resource Group".
- Click on the resource group you want to manage.
- Select the storage account
- Click delete, then confirm.

## Creating Blob Storage from the CLI
This is an alternative way to create an Azure Storage Account and a Storage Container using Azure CLI.

First we create our storage account. We use the following command on cmd:

```markdown
    az storage account create ^
    --name helloworld12345 ^
    --resource-group resource-group-west ^
    --location westus2
```
The storage will default to general purpose V2 and the access tier cannot be set, so it will default to hot. 

### Then we create our container.

```markdown
    az storage container create ^
    --account-name helloworld12345 ^
    --name images ^
    --auth-mode login ^
    --public-access container
```

You can go to the portal to check that the storage account and container have been created. You can then upload an image through the portal the same way as we did using the portal; 

To change the access tier, go to ```settings```, then ```Access tier(default)```, then select ```cool```.
Lastly,to set up a new lifecycle management rule for an alert, go to  ```Blob Service``` within your Storage Account, click ```Lifecycle Management```, then ```+Add rule```.


# Day 13 of #60DaysOfUdacity (Wednesday, December 23th, 2020)
D13: Day 13 of #60daysofudacity
- Today, I connected the app to the storage account and database. 
- I was able to read texts and images saved in it. 

### To connect an app to the storage we've set up, we need a few things from each storage service.

#### From the SQL server and database:
- SQL Server server name (the name of the sql server with .database.windows.net appended to it. In this case, mytest-server.database.windows.net) 
- Admin username: udacityadmin
- Admin password: p@ssword123
- SQL Database name ("test-db)

#### From blob storage:
- Storage account name ("helloworld12345mine")
- A storage account access key (go to ```storage account``` > ```settings``` > ```access keys```).
    (zWkVGXi1CCU+6UgnwQ7ruThRfnxuSKthrg6DLE+ECJdOUhEJ6g3jkwuHISfjPHPRfR2lW1tjdl4mRC76LjlR8A==)
- Container name("images").

#### Summary
- Add the necessary environment variables to connect to the SQL database in ```config.py```.
- Then, add the necessary environment variables to connect to the Blob storage container in ```config.py```.
- Add the necessary code in ```models.py``` to work with the BlobServiceClient to upload new images and delete any images that are replaced.
- Create "Animals" table in the database.
- Run the app on your local machine, and check that the animals are correctly populated from the SQL database.
- Add some images for each animal. You should be able to check back in your blob container and see that new images were added, and they should populate back to the main page.


### Azure Storage Blob Library for Python
In order to interact with our Azure blob storage from within the Python web app, we'll need the Azure Storage Blob Library(https://pypi.org/project/azure-storage-blob/). Note that you can install this with ```pip install azure-storage-blob```, and you'll need to make sure to include the library in your ```requirements.txt``` file in your own apps.

We will largely focus on the BlobServiceClient class. This class has three methods we’ll use:

- get_blob_client - creates a blob client using the filename as the name for the blob
- upload_blob - upload the file to the blob container
- delete_blob - delete a blob from a blob container

#### Uploading a blob
Here is the code I included for uploading a blob in the ```models.py``` file.

```markdown
    from azure.storage.blob import BlobServiceClient

    blob_container = app.config['BLOB_CONTAINER']
    storage_url = "https://{}.blob.core.windows.net/".format(app.config['BLOB_ACCOUNT'])
    blob_service = BlobServiceClient(account_url=storage_url, credential=app.config['BLOB_STORAGE_KEY'])

    blob_client = blob_service.get_blob_client(container=blob_container, blob=filename)
    blob_client.upload_blob(file)
```

Note that I am getting the ```BLOB_CONTAINER``` name from the configuration file, which was attached to the Flask app separately. I do a similar procedure for getting the ```BLOB_ACCOUNT``` AND ```BLOB_STORAGE_KEY``` where needed. I then use the aforementioned ```get_blob_client``` and ```upload_blob``` functions to upload a file.

You might notice that there is a ```filename``` and ```file``` used here - these are not the same things! The ```filename``` is just the name of the ```file```, e.g. ```test_image.png```, while the ```file``` is the actual file object. So, the ```blob client``` is first called to create a blob with the given ```filename```, and then the ```file``` is uploaded into that ```filename``` blob.

#### Deleting a blob
Assuming you've already defined the ```blob_service``` from before, you just need to get a new blob client with ```get_blob_client``` for the related container and ```filename```, then ```delete_blob```.

```markdown
    blob_client = blob_service.get_blob_client(container=blob_container, blob=filename)
    blob_client.delete_blob()
```

It's important to note here you don't need a file to feed to ```delete_blob``` - by specifying the ```filename``` when you ```get_blob_client```, it already knows what blob you are referring to.

### Create "Animals" table in the database. 
- Open the created "SQL database" by clicking on its name to access it from the "Resource group" page.
- Click on the "Query editor" in the left side menu, and then log in with my SQL Server credentials.
- past the query from my animals-table-init.sql script below into the query window, and hit "Run"; you should see Query succeeded: Affected rows: 3.

```markdown
CREATE TABLE ANIMALS(
    id INT NOT NULL IDENTITY(1, 1),
    name VARCHAR(75) NOT NULL,
    scientific_name VARCHAR(75) NOT NULL,
	description VARCHAR(800) NOT NULL,
    image_path VARCHAR(100) NULL,
	PRIMARY KEY (id)
);

INSERT INTO dbo.animals (name, scientific_name, description)
VALUES (
    'Bengal tiger',
    'Panthera tigris tigris',
    'A big orange cat! They like to hunt and usually live alone. Are found largely in India and Bangladesh.'
);

INSERT INTO dbo.animals (name, scientific_name, description)
VALUES (
    'African bush elephant',
    'Loxodonta africana',
    'Huge, incredibly intelligent mammals, with large, distinctive tusks. Found in multiple locations throughout Africa.'
);

INSERT INTO dbo.animals (name, scientific_name, description)
VALUES (
    'Monarch Butterfly',
    'Danaus plexippus',
    'A butterfly typically covered in orange, black and white markings. Can be found throughout the Americas, as well as in many islands in the Pacific and Australia.'
);
```

### Activate virtual environment and run app. 
- cd to app folder.
- Create venv ```python3 -m venv venv```
- Activate the env source ```venv\Scripts\activate```
- Upgrade pip in our virtual environment ```python -m pip install --upgrade pip```
- then Install dependencies ```pip install -r requirements.txt```
- Run the app ```python application.py```
- Go to ```http://localhost:5555/``` in your browser and you should see the application.

# Day 14 of #60DaysOfUdacity (Thursday, December 24th, 2020) - Christmas Eve
D14: Day 14 of #60daysofudacity
Christmas is here, celebration mode has been activated. Almost missed today's challenge, but i encouraged myself to watch the videos and study the notes for atleast 30minutes. So today, 
- I watched the introduction to Security and Monitoring basics of Lesson 4. 
- Also watched topic 2 to 4 videos and the lecture note. 

# Day 15 of #60DaysOfUdacity (Friday, December 25th, 2020) - Christmas day
D15: Day 15 of #60daysofudacity
it's Christmas day, i tried to study new thing today but it didn't work. I ended up revising old lectures/materials. Still in the festive mode. I'm hoping to learn new stuff tomorrow. I will like to encouraging everyone to not get carried away by the merriment of the season. Keep pushing .


# Day 16 of #60DaysOfUdacity (Saturday, December 26th, 2020) - Boxing day
D16: Day 16 of #60daysofudacity
Azure Active Directory is Microsoft’s solution for single sign-on (SSO) and multi-factor authentication (MFA). We'll be using it in combination with the Microsoft Authentication Library (MSAL) to use "Sign in with Microsoft" buttons in an app, although it can be used more broadly for identity management purposes within an organization. The "tenant" in Azure AD is usually equivalent to an organization.

## Using Azure Active Directory in the Portal
- Search for "Active Directory" on the Azure portal. 
- From there, you should already be in a tenant by default, although you can create a new one, if needed, to keep things separate from your main tenant. Again, if you are on an enterprise account that limits your access here, you may need to use another (personal) account.

### To register an app in Azure AD (which does not actually need a deployed app for these steps):
- Click on app registrations on the left panel.
- click on ```+new registration```
- Enter a user-facing display name.
- I allowed the widest set of accounts to access it (Accounts in any organizational directory and personal Microsoft accounts). Chose this because it makes it easier to allow other users to authenticate with the app.
- You can ignore the redirect URI here for now, and revisit that when we get to implementing OAuth 2.0. 
- Once the Application has been registered, you need to copy the Application (client) ID, as it’ll be used later on.
- Next, under "manage" on the left here, click on ```certificates and secrets``` seen on the left side.
- Click on "+ New client secret", then enter a description (you can decide on your own desired expiration time, I chose one year). Copy down the string under "Value", and make sure you store it somewhere safe - you won't be able to see it again, and would otherwise have to create a new client secret once again. We’ll use this value and the application client ID when implementing OAuth 2.0.

```markdown
	Application(client) ID: c43fefe9-85e6-4635-be29-6b398cf53cbf
	Directory (tenant)ID: a60d5df0-1322-4a1f-bd98-b2fef3ad851f
	Object ID: 77569788-4ce5-4bd6-aa97-42952b14f21a

	Client secrets
	hello world desc - (Value) UgzSP5556B7W-9_qbAB~I923F-sDZudZ1a (ID) 1a7c635e-5758-443c-80e5-25ec7c9e12dd
```

# Day 17 of #60DaysOfUdacity (Sunday, December 27th, 2020)
D17: Day 17 of #60daysofudacity
Today,  
- Watched videos 8 to 11 in Lesson 4.  
- implemented and integrated the authorization process with MSAL
into my existing application. 
- course completion at 91% viewed.

## Add necessary variables in config.py

- Fill out ```CLIENT_SECRET``` and ```CLIENT_ID``` by getting the relevant values from the registered app in Azure Active Directory (see previous exercise).
- Add a ```REDIRECT_PATH``` - I used "/getAToken".
- Note that if we were using a single tenant app, ```AUTHORITY``` would switch from https://login.microsoftonline.com/common to ending instead with the tenant name (in place of common).

## Add the redirect and logout URIs in Azure AD
- Within your registered app, under "Manage", click on "Authentication", then "+Add a platform".
- Select "Web" under "Web applications" in the new window.
- Enter ```https://localhost:5555/getAToken``` in the redirect URI (replace ```/getAToken``` with your own ```REDIRECT_PATH```).
- Enter ```https://localhost:5555/login``` in the logout URI - we want the user to be redirected back to the login page of this app when they logout. Other apps could potentially just redirect back to a homepage (our homepage is hidden behind the login process).
Click Configure.

## Adding MSAL functionality
### Implement "Sign in with Microsoft" with MSAL

- In ```_build_msal_app```, you'll want to use a ```ConfidentialClientApplication``` (see documentation here https://msal-python.readthedocs.io/en/latest/#confidentialclientapplication):
```markdown
 	return msal.ConfidentialClientApplication(
     		Config.CLIENT_ID, authority=authority or Config.AUTHORITY,
     		client_credential=Config.CLIENT_SECRET, token_cache=cache)
```

- In ```_build_auth_url```, you can use the previous msal app to get an authorization request url (see documentation here https://msal-python.readthedocs.io/en/latest/#msal.ClientApplication.get_authorization_request_url):
```markdown
	return _build_msal_app(authority=authority).get_authorization_request_url(
    		scopes or [],
    		state=state or str(uuid.uuid4()),
    		redirect_uri=url_for('authorized', _external=True, _scheme='https'))
```

- If we go back to our ```authorized``` function, we'll see a place where we can use our ```_build_msal_app``` function again, this time to acquire a token (see documentation here https://msal-python.readthedocs.io/en/latest/#msal.ClientApplication.acquire_token_by_authorization_code):
```markdown
 	result = _build_msal_app(cache=cache).acquire_token_by_authorization_code(
     		request.args['code'],
     		scopes=Config.SCOPE,
     		redirect_uri=url_for('authorized', _external=True, _scheme='https'))
```

- At this point, logging a user in with Microsoft should work just fine, but you should also make sure they are able to log out. So, along with making sure you have the correct logout URI in Azure AD, you also need to return the correct redirect in ```logout```:
```markdown
 	return redirect(
     		Config.AUTHORITY + '/oauth2/v2.0/logout' +
     		'?post_logout_redirect_uri=' + url_for('login', _external=True))
```

### Using HTTPS with Your App
You may have noticed the use of ```_scheme='https'``` and ```_external=True``` in the ```url_for()``` functions used in this exercise.

Setting the ```_scheme``` to "https" allows it to be served to the browser, as you may guess, through "https". Now, we don't have a fully secure app, as you may note when you try to open it in your browser; however, in this basic app, it's not super concerning just yet. However, Azure Active Directory will not allow you to use a non-HTTPS website for a live app's redirect URI (localhost can still use HTTP).

In order for this ```_scheme``` setting to work, ```_external``` must also be set to True, which just means an absolute URL will be created, as opposed to a relative URL such as which works with localhost.


# D18: Day 18 of #60daysofudacity (Monday, December 28th, 2020)
Today,
- Watched videos 12 to 14 in Lesson 4.
- Attempted the exercise in 13 and 14 but encountered some challenges, couldn't finish.
- Current course completion at 96% viewed.

# D19: Day 19 of #60daysofudacity (Tuesday, December 29th, 2020)
Today,
- Revised videos 12 to 14 in Lesson 4.
- Attempted the exercise in 13 and 14 and fixed the problems i encountered earlier.
- Added monitoring and logging into my Azure applications, including storing logs and activating alerts
- Completed the course. 

## Monitoring and Logging in Azure. 
- Login to Azure CLI ```az login```
- navigate to the app directory. 

### Adding Logging in the Flask App
1. Flask apps actually have this logger by default, and it uses the ```logging``` library from the Python standard library. As such, since we want to set the logging level to ```warning```, it can be done as follows in ```__init__.py```:
```markdown
	app.logger.setLevel(logging.WARNING)
```
We also want to update the stream handler for the logger to only pay attention to warnings and above:
```markdown
	streamHandler = logging.StreamHandler()
 	streamHandler.setLevel(logging.WARNING)
 	app.logger.addHandler(streamHandler)
```

2. There's quite a bit of room for exactly what messages you want to log for each log level in the app, but I did this in the basic fashion below, just stating back which level occurred:
```markdown
	if log:
     		if log == 'info':
         		app.logger.info('No issue.')
     		elif log == 'warning':
         		app.logger.warning('Warning occurred.')
     		elif log == 'error':
         		app.logger.error('Error occurred.')
     		elif log == 'critical':
         		app.logger.critical('Critical error occurred.')
```

3. From there, I first confirmed that the logs appeared to be working through the terminal by running on localhost, then I created a resource group and deployed the app to azure. 
```markdown
	az webapp up -g hello-world-forreal-dec -n flaskexercisedecember --location westeurope --sku F1 --verbose
```

### Sending Logs to Storage
Note: I should be using console logs when setting up my alert, not app logs.

1. To prepare for sending logs to storage, I first went and created a new storage account in the portal. This can just be standard performance, StorageV2, with cool access tier (you would likely be better served with hot access in an app with substantial logging needs). I used the defaults for everything else.

2. If the app is deployed, head to the app URL and press a few buttons. Back in the App Service page in the portal, find the "Log stream" under "Monitoring", and confirm that your button presses are in fact showing up in the Log stream.

3.Next, click on "Diagnostic settings", also under "Monitoring", then "Add diagnostic setting". Give it a name, then under "log", click "AppServiceConsoleLogs", then under "Destination details", click "Archive to a storage account". You can change the "Retention (days)" that has appeared on the left if you want; the default of "0" will be indefinite retention. Then click "Save". It will take about ten minutes for this to begin populating.

### Adding Alerts
1. Go back to your App Service, and click on "Alerts" under "Monitoring", then "+ New alert rule". The scope should just be your app.

2. Under "Condition", click "Select condition", then find the "Signal name" ```Requests```, and click on it. Scroll down to "Alert logic", and change the "Aggregation Type" to ```Count```, then put ```20``` in the "count" box (this is set low on purpose). Finally, set the "Aggregation granularity" to 15 minutes to make sure you will activate the alert, and click "Done".

3. Under "Action group", click "Select action group", and then "+ Create action group". Give it an "Action group name", "Short name", then make sure to select the same Resource group as your app is in for easier deletion later on. Give the "Action name" something descriptive, such as ```20 Requests in 15 minutes```. Then, for "Action Type", select "Email/SMS message/Push/Voice". In the new window, click on "Email" and enter your own email, then click "OK" at the bottom of this side window, then "OK" at the bottom of the main window for adding the action group.

4. Lastly, add an alert rule name and description. You can change the severity of the alert if you wish. Make sure the final box for "Enable alert rule upon creation" is checked. Finally, click the "Create alert rule" button. Once again, this will take about 10 minutes to activate.
Quotas & Checking on Logs and Alerts

### Considering quotas:

1. While waiting for the previous two stages to be ready, navigate back to your App Service, and find the "App Service plan" header, then click on "Quotas". On mine, under the free tier, I notice I have 60 minutes of CPU time for the day, and 330 MB (I accidentally say 165 MB in the video) of data out (along with one for shorter CPU time, and another for memory usage).

2. While not required to add the actual alerts for these, it's important to consider how you might approach doing so. If I go back to Alerts and check out the different conditions, I notice that CPU Time and Data Out are both two other Metrics I could make an alert based on. For CPU Time, perhaps I could consider setting an alert for 15 minutes total used (900 seconds) within a six hour aggregation period. If this is triggered, maintained activity at that level would cause the CPU time quota to be exceeded, leading to the app being stopped.

3. There are plenty of more ways to address these quotas through alerts, but that is just one example.

### Checking that log storage and alerts were appropriately created:

1.If it's been 10 minutes, first navigate back to your app URL and click the buttons each a handful of times, to make sure you have some new logging information, as well as hitting a decent number of requests to trigger the alert email. You can check the "Metrics" page under "Monitoring" for your App Service, and select the "Requests" metric (it updates once every five minutes) to confirm you are actually sending enough requests, or you could also manually count from the Log stream.

2. To check log storage is appropriately configured, go back to the storage account you created earlier, and look at its containers. If it hasn't been ten minutes yet, the logs may not have appeared yet. If a container was created, click on it, then dive down into the directories until you get to the json logs. Download the log, and confirm it shows some of your various logging from the app.

3. To check that the alert has appropriately occurred (make sure you have actually met the trigger criteria), just check your email. Note that you will have received a first email just for joining the action group.


# D20: Day 20 of #60daysofudacity (Wednesday, December 30th, 2020)
- In other to be able to take on the optional project challenge, I started studying "Python Flask Tutorial: Full-Featured Web App " by Corey Schafer https://www.youtube.com/watch?v=UIJKdCIEXUQ&list=PL-osiE80TeTs4UjLw5MM6OjgkjFeUxCYH&index=3. 
- Completed part 1 "Getting Started" and Part 2 "Templates" in the series. 
- Since I'm going to be using virtual environment alot for this project, i studies how on Creating Virtual Environments using Python’s built-in venv module on Windows and how to use it in project. I documented the steps here https://peteroj.medium.com/creating-virtual-environments-using-pythons-built-in-venv-module-on-windows-916dbdec7f0e.


# D21: Day 21 of #60daysofudacity - New year Eve (Thursday, December 31st, 2020)
- I continued studying "Python Flask Tutorial: Full-Featured Web App " by Corey Schafer https://www.youtube.com/watch?v=UIJKdCIEXUQ&list=PL-osiE80TeTs4UjLw5MM6OjgkjFeUxCYH&index=3.
- I watched and practiced the part 3 "Forms and User Input" in the series. Faced some challenges, couldn't complete it. I will continue tomorrow.

# D22: Day 22 of #60daysofudacity - New year Day (Friday, January 1st, 2021)
- I continued studying "Python Flask Tutorial: Full-Featured Web App " by Corey Schafer https://www.youtube.com/watch?v=44PvX0Yv368&list=PL-osiE80TeTs4UjLw5MM6OjgkjFeUxCYH&index=5
- I watched and practiced parts 3, 4 and 5 of 15 in the series. 
- Resolved the challenges i faced earlier with "Forms and User Input" .
- Created a database using Flask SQLalchemy.
- Structured the project package. 

# D23: Day 23 of #60daysofudacity (Saturday, January 2nd, 2021)
- I continued studying "Python Flask Tutorial: Full-Featured Web App " by Corey Schafer 
- I watched and practiced parts 6 of 15 in the series. 
- Implemented User authentication. 

# D24: Day 24 of #60daysofudacity (Sunday, January 3rd, 2021)
- I continued studying "Python Flask Tutorial: Full-Featured Web App " by Corey Schafer 
- I watched and practiced parts 7 of 15 "User Account and Profile Picture" in the series. 
- Implemented the feature for update the user's account and its profile picture

# D25: Day 25 of #60daysofudacity (Monday, January 4th, 2021)
- I continued studying "Python Flask Tutorial: Full-Featured Web App " by Corey Schafer 
- I watched and practiced parts 8 of 15 "Creating, reading, updating and deleting user posts" in the series. 
- I started the course "Data Structures and Algorithm" in Python. https://classroom.udacity.com/courses/ud513/lessons/7117335401/concepts/71182844640923


# D26: Day 26 of #60daysofudacity (Tuesday, January 5th, 2021)
- I continued studying "Python Flask Tutorial: Full-Featured Web App " by Corey Schafer
- I watched and practiced parts 9 of 15 "Pagination" in the series.
- I continued the course "Data Structures and Algorithm" in Python. https://classroom.udacity.com/courses/ud513/lessons/7117335401/concepts/71182844640923
- Learnt about LinkedList today.

# D27: Day 27 of #60daysofudacity (Wednesday, January 6th, 2021)
- I continued studying "Python Flask Tutorial: Full-Featured Web App " by Corey Schafer
- I watched and practiced parts 10 of 15 "Email and Password" in the series.
- I continued the course "Data Structures and Algorithm" in Python. https://classroom.udacity.com/courses/ud513/lessons/7117335401/concepts/71182844640923
- Learnt about Stacks and Queues today.

# D28: Day 28 of #60daysofudacity (Thursday, January 7th, 2021)
- I revised the code from the tutorial series "Python Flask Tutorial: Full-Featured Web App " by Corey Schafer up to part 10 of 15. 


# D27: Day 27 of #60daysofudacity (Wednesday, January 6th, 2021)
- I continued studying "Python Flask Tutorial: Full-Featured Web App " by Corey Schafer
- I watched and practiced parts 11 of 15 "Blueprints and Configuration" in the series.

