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

- Typed  "az login" on the terminal to login to the Azure CLI.
- Used "az account list-locations -o table" to see the list of all locations which was listed in a table format. 
- Used the Azure CLI command "az group create" and passed in two flags:
    resource group --name
    --location which is the same as the "region" field on the Azure portal.
- Therefore, created my resource group in the West US 2 region with the name "resource-group-west-using-cli":
- The command "az group create --name resource-group-west-using-cli --location westus2"
- Viewed all created resource groups using both portal and cli via https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups. See screen via https://github.com/PeterO2309/Bertelsmann-Scholarship-2020-2021-Cloud-Track/blob/main/Images/day04_1.PNG
