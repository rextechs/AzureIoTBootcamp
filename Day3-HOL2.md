
# Intelligent Edge

In this Hands on Lab, we will create following scenarios

- Setup Azure IoT Edge Runtime Environment
- Clone, edit, and compile Azure IoT Edge Module
- Deploy the Azure IoT Edge Module
- Control the Azure IoT Ede Module from Cloud

## Prerequisites

## Step 1 : Azure IoT Hub  

Create an IoT Hub if you do not have one.  Please follow one of 3 methods to create an IoT Hub

- [Create an IoT hub using the Azure portal](articles/iot-hub/iot-hub-create-through-portal.md)  
- [Create an IoT hub using the Azure CLI](articles/iot-hub/iot-hub-create-using-cli.md)
- [Create an IoT hub using the Azure IoT Tools for Visual Studio Code](articles/iot-hub/iot-hub-create-use-iot-toolkit.md)

## Step 2 : Azure IoT Edge Device

Create an IoT Edge device in the IoT Hub from the previous step

[Register a new Azure IoT Edge device from the Azure portal](articles/iot-edge/how-to-register-device-portal.md)

## Step 3 : Azure Container Registry

[Quickstart: Deploy a container instance in Azure using the Azure portal](articles/container-instances/container-instances-quickstart-portal.md)

## Step 4 : Clone Source Code

```bash

git clone https://cdsiotbootcamp.visualstudio.com/bootcamp2019/_git/IntelligentEdgeHOL

```

```
sudo apt-get install -y openssh-server
sudo apt-get install -y curl git

https://www.youtube.com/watch?v=H2oonkOZkzY