# CyberbullyingDetectionModel
This repository contains a dataset of tweets categorized by cyberbullying_type, of which there are 6, all with equal distribution ([You can find the dataset here](https://www.kaggle.com/datasets/andrewmvd/cyberbullying-classification)). This repository also contains the code for analyzing the aforementioned dataset using Apache Spark. There is also the option to run a version of the project through Databricks Community Edition. Instructions for running both versions can be found below. This repository also contains presentations created throughout the span of this project, representing different stages of development.
## Setting Up Spark on Azure VM
### 1. Create an Azure VM
- Log in to the [Azure portal](https://azure.microsoft.com/en-us/get-started/azure-portal).
- Click on "Virtual machines" then click "Create".
- Select desired options for your VM then click "Review + create" to provision the VM.
### 2. Connect to the Azure VM
- Once the VM is created, connect to it using SSH.
### 3. Update the System Packages
```
sudo apt update
```
### 4. Install Java Development Kit
```
sudo apt install default-jdk -y
```
### 5. Download and Extract Spark
```
wget https://dlcdn.apache.org/spark/spark-3.5.1/spark-3.5.1-bin-hadoop3.tgz
tar -xzvf spark-3.5.1-bin-hadoop3.tgz
```
### 6. Move Spark Directory to /opt
```
sudo mv spark-3.5.1-bin-hadoop3 /opt/spark
```
### 7. Set Environment Variables
- Open profile settings:
```
sudo nano ~/.bashrc
```
- Add the following lines to the end of the file:
```
export SPARK_HOME=/opt/spark
export PATH=$PATH:$SPARK_HOME/bin
```
- Source your profile to apply the changes:
```
source ~/.bashrc
```
### 8. Install Python Dependencies
```
sudo apt-get install python3-pip -y
pip3 install pyspark
```
## Downloading and Running the Script
- You will need TextBlob installed to run part of the script:
```
pip install textblob
```
- You also need numpy installed:
```
pip install numpy
```
### 1. Download the files from this repository and transfer them to the VM using FileZilla:
- Open FileZilla > File > Site Manager
- Click new site
- For protocol select SFTP - SSH ...
- Port: 22
- Host: paste the Public IP address of your VM here
- Logon type: However you sign into your VM (mine was Key)
- User: Username of your VM
- If you are using Key for Logon type, in the Key file section browse to where the key is located
- Click connect
- Move cyberbullying_tweets.csv dataset over
- Move files from the folder titled "Spark_scripts"
- Make sure all files are in the same root directory in the VM
### 2. Run the Spark script
> [!NOTE]  
> Running this script may take a **significant** amount of time (it took my virtual machine over an hour).
> It includes all steps from preprocessing to model training and evaluation.
```
spark-submit main_script.py
```
- After the above script fully executes, you will be able to see the evaluation metrics for the model.
- To simply view the final results without having to run the entire script, please refer to the FinalResults.pdf file.
- You can also run an older version of this project from when I was still using Databricks Community Edition, before I moved over to a VM (recommended).
## Running Databricks Community Edition Version
### 1. Create a Databricks Community Edition account
- Visit [this](https://www.databricks.com/) link to create a Databricks Community Edition account
- Fill out the inital fields then click Continue.
- When it asks "How will you be using Databricks?" select "Get started with Community Edition", which is a free edition for personal use.
- Complete email validation and sign in to your account. After signing in, you should be met with the dashboard.
### 2. Access the notebook
- Access the notebook for this version of the project by clicking [here](https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/1941027640709137/4153980120042452/1023779770062107/latest.html).
### 3. Import the notebook
- When you visit the link above, there will be an import button in the top right. Click that and copy the URL.
- Go back to your Databricks dashboard. Hover over the left side of the screen and go to Workspace > Users > Your User (should be your email address)
- Under your user right click and select import.
- Select Import from URL.
- Paste the previously mentioned link and click Import.
### 4. Create compute
- Once you have imported the notebook, you must create a compute.
- Hover over the left side of the screen once again and this time go to Compute.
- Click Create Compute on the right side of the screen.
- Give the compute a name.
- Click Create compute.
- Cluster may take a few minutes to start runnning.
### 5. Configure settings and add dataset
- Once your cluster is up and running, you must add the dataset to the Databricks File Transfer System.
- Download cyberbullying_tweets.csv from this repository.
- Click your email on the top right side of the screen and go to User Settings.
- Navigate to the Advanced tab found under Workspace-admin.
- Scroll down to Other and turn on DBFS File Browser, then refresh page.
- Hover over the left side of the Databricks Community Edition dashboard and select Catalog.
- Click DBFS, found next to the Database Tables button.
- Click FileStore > tables > right click inside the new folder that has just expanded
- Select upload here and then upload the cyberbullying_tweets.csv file.
> [!IMPORTANT]  
> Make sure you upload the .csv file to the correct folder. If the path is not correct the notebook will not run.
### 6. Run the notebook
- Go to Workspace > Users > Your User > notebook that we previously imported
- On the top right side of the screen select Connect then the cluster that we created previously.
- Click Run all.
- Once all cells have finished running, scroll to the bottom of the notebook to see the evaluation of the model.
