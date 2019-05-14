
# Building Intelligent Edge Device

In this Hands on Lab, we will create following scenarios

- Setup Azure IoT Edge Runtime Environment
- Clone, edit, and compile Azure IoT Edge Module
- Deploy the Azure IoT Edge Module
- Control the Azure IoT Ede Module from Cloud

## Prerequisites

## Development Environment (DevEnv)

### Software 

- Windows 10 IoT  
  For the development machine
- Visual Studio Code
- Git tools  
  Git command line tool as well as Github Desktop are pre-installed in DevEnv
- Docker for Desktop  
  Need to build containers

### Software : Target Device

- Ubuntu 18.04  
  A target OS that will run IoT Edge Module
- Moby Engine and CLI
- Auzre IoT Edge Runtime

### Hardware

- Windows 10 Development PC
- A Server Machine running Ubuntu VM

## Step 1 : Prepare Azure IoT Hub  

Create an IoT Hub if you do not have one.  
Choose your favorite tool to create a new IoT Hub.

|Tool     |Link     |
|---------|---------|
|Portal   |[Create an IoT hub using the Azure portal](articles/iot-hub/iot-hub-create-through-portal.md)           |
|AZ CLI   |[Create an IoT hub using the Azure CLI](articles/iot-hub/iot-hub-create-using-cli.md)         |
|VSCode   |[Create an IoT hub using the Azure IoT Tools for Visual Studio Code](articles/iot-hub/iot-hub-create-use-iot-toolkit.md)         |

## Step 2 : Prepare Azure IoT Edge Device

Create an IoT Edge Device in the IoT Hub you just created.  
Choose your favorite tool to create a new IoT Edge Device.

|Tool     |Link     |
|---------|---------|
|Portal   |[Register a new Azure IoT Edge device from the Azure portal](articles/iot-edge/how-to-register-device-portal.md)         |
|AZ CLI   |[Register a new Azure IoT Edge device with Azure CLI](articles/iot-edge/how-to-register-device-cli.md)         |
|VSCode   |[Register a new Azure IoT Edge device from Visual Studio Code](articles/iot-edge/how-to-register-device-vscode.md)         |

## Step 3 : Install Azure IoT Edge Runtime Environment



## Step 4 : Clone Source Code

```bash

git clone https://cdsiotbootcamp.visualstudio.com/bootcamp2019/_git/IntelligentEdgeHOL

```

## Step 5 : Prepare Azure Container Registry

- [Create a private container registry using the Azure portal](articles/container-registry/container-registry-get-started-portal.md)
- [Quickstart: Create a private container registry using the Azure CLI](articles/container-registry/container-registry-get-started-azure-cli.md)
- [Create a private container registry using Azure PowerShell](articles/container-registry/container-registry-get-started-powershell.md)

## Step 6 : Modify Sample Code

1. ACR
1. 

## Step 7 : Build and Push Container Image


## Step 8 : Deploy Module

```
sudo apt-get install -y openssh-server
sudo apt-get install -y curl git
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/

sudo apt-get update
sudo apt-get install moby-engine
sudo apt-get install moby-cli

https://www.youtube.com/watch?v=H2oonkOZkzY