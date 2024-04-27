# CyberbullyingDetectionModel
This repository contains a dataset of tweets categorized by cyberbullying_type, of which there are 6, all with equal distribution ([You can find the dataset here](https://www.kaggle.com/datasets/andrewmvd/cyberbullying-classification)). This repository also contains the code for analyzing the aforementioned dataset using Apache Spark, and relevant presentations created along the course of the project.
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
%pip install textblob
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
> Running this script may take a **sigificant** amount of time (it took my virtual machine over an hour on average).
> It includes all steps from preprocessing to model training and evaluation.
```
spark-submit main_script.py
```
- After the above script fully executes, you will be able to see the evaluation metrics for the model.
- To simply view the final results, please refer to the final_results.ppt file.
