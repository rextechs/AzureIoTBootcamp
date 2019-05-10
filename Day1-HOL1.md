# Windows Server IoT 2019 + Azure IoT Edge (45 Min)

In this Hands on Lab (HOL), we are going to install Azure IoT Edge Runtime and IoT Edge Module to Windows Server IoT 2019.  
We will use virtual machines, however, the same steps described in this article apply to physical machine installation.  

## Prerequisites

- Instance of IoT Hub
- IoT Edge device in the IoT Hub
- Windows Server IoT 2019  
  Can be physical machine or virtual machine

## Key Components

- IoT Hub
- IoT Edge Module  
  We are going to install "Simulated Temperature Sensor" from Azure IoT Edge Marketplace.  This module generates temperature and humidity data.  
- Container  
  IoT Edge Runtime as well as IoT Edge Module(s) are containerized

## Step 1 : Create an instance of IoT Hub

[Create an IoT hub using the Azure portal](articles/iot-hub/iot-hub-create-through-portal.md)  
  
## Step 2 : Register a new Azure IoT Edge device

[Register a new Azure IoT Edge device from the Azure portal](articles/iot-edge/how-to-register-device-portal.md)

## Step 3 : Install IoT Edge Runtime on Windows

[Install the Azure IoT Edge runtime on Windows](articles/iot-edge/how-to-install-iot-edge-windows.md)

## Step 4 : Deploy Simulated Temperature Sensor from Marketplace

<Run docker commands, display logs, etc>

## Step 5 : Confirm D2C Message

<Use Device Explorer to see D2C messages>

## Step 6 : Clean up

<Remove Simulated Temperature Sensor>