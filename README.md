# demo-function-chain
This is a simple function chaining example that can be deployed with xOpera on Azure platform.
## Table of contents
- [Purpose](#Purpose)
- [Functionality](#Functionality)
- [Quick deployment](#Quick-deployment)
## Purpose
The repository implements an image processing demo, which includes three different functions for style transfermation, channel filter and printing text on the image. These three functions are chainging with a sequential pattern supported by Azure Durable Functions and Azure Functions. 
## Functionality
The main functionality of this example is to sequentially execute three image processing function. This function in chain is triggered by an uploading event in the Azure Blob container. The AzureBlobTriggerContainer node creates two containers, including one for uploading and another one for output result. The durable orchestrator then calls for three Azure functions in the order. The process is shown in the following figure.
![Image of function chain](https://github.com/radon-h2020/demo-function-chain/blob/main/function-chain.png)

## Quick deployment
To be able to deployment with xOpera, it requires to install Azure CLI and the following prerequisites.

```
# install Azure CLI and try to login in your account
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
az login

# install prerequisites
cd demo-function-chain
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install ansible
pip install opera
```
Before deployment, you need to set the variables in the inputs.yaml to configure the user parameters. For example:
```
# set the storage account name you want to create on Azure
storage_account_name: myexamplestorage
```
Now, you can deploy this image processing example with xOpera as follows: 
```
# run xOpera service
opera deploy -i inputs.yaml service.yaml
```
