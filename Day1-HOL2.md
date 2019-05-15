# Windows 10 IoT + Azure IoT Edge - Advance Lab (90 Min)

## Prerequisites

- An instance of IoT Hub from the previous HOL

## Key Components

## Step 1 : Register a new Azure IoT Edge device

## Sign in to access your IoT hub

You can use the Azure IoT extensions for Visual Studio Code to perform operations with your IoT hub. For these operations to work, you need to sign in to your Azure account and select the IoT hub that you are working on.

1. In Visual Studio Code, open the **Explorer** view.

1. At the bottom of the Explorer, expand the **Azure IoT Hub Devices** section.

   ![Expand Azure IoT Hub Devices section](./images/Register-device-vscode/azure-iot-hub-devices.png)

1. Click on the **...** in the **Azure IoT Hub Devices** section header. If you don't see the ellipsis, click on or hover over the header.

1. Choose **Select IoT Hub**.

2. If you are not signed in to your Azure account, follow the prompts and sign in to your Azure account.

3. Select your Azure subscription.

4. Select your IoT hub.

## Create a device

1. In the VS Code Explorer, expand the **Azure IoT Hub Devices** section.

1. Click on the **...** in the **Azure IoT Hub Devices** section header. If you don't see the ellipsis, click on or hover over the header.

1. Select **Create IoT Edge Device**.

1. In the text box that opens, give your device an ID.

In the output screen, you see the result of the command. The device info is printed, which includes the **deviceId** that you provided and the **connectionString** that you can use to connect your physical device to your IoT hub.

## View all devices

All the devices that connect to your IoT hub are listed in the **Azure IoT Hub Devices** section of the Visual Studio Code Explorer. IoT Edge devices are distinguishable from non-Edge devices with a different icon, and the fact that they can be expanded to show the modules deployed to each device.

   ![View all IoT Edge devices in your IoT hub](./images/Register-device-vscode/view-devices.png)

## Retrieve the connection string

When you're ready to set up your device, you need the connection string that links your physical device with its identity in the IoT hub.

1. Right-click on the ID of your device in the **Azure IoT Hub Devices** section.

1. Select **Copy Device Connection String**.

   The connection string is copied to your clipboard.

You can also select **Get Device Info** from the right-click menu to see all the device info, including the connection string, in the output window.

## Step 2 : Install and configure IoT Edge Runtime on Windows 10

[Install the Azure IoT Edge runtime on Windows](articles/iot-edge/how-to-install-iot-edge-windows.md)


### 1. Open a Powershell window as an Administrator:

### 2. The **Deploy-IoTEdge** command checks that your Windows machine is on a supported version, turns on the containers feature, and then downloads the moby runtime and the IoT Edge runtime. The command defaults to using Windows containers.

```powershell
. {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
Deploy-IoTEdge
```

### 3. Follow the prompted steps, you can just select the default options. The machine will restart. 

### 4. Once the machine is restarted, open a Powershell window as Administrator and run the following command tocomplete the installation process

```powershell
. {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
Initialize-IoTEdge
```

### 5. Provide the device connection string copied before. 



## Step 3 : Confirm IoT Edge runtime is installed and running

You can check the status of the IoT Edge service by: 

```powershell
Get-Service iotedge
```

## Step 4 : Create Azure Container Registry

[Quickstart: Deploy a container instance in Azure using the Azure portal](articles/container-instances/container-instances-quickstart-portal.md)

## Step 5 : Clone Sample Code from Github

Clone this repo 
https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/EdgeModules/SqueezeNetObjectDetection/cs

## Step 6 : Open in Visual Studio Code

## Step 7 : Edit Source Code

<Set parameters, ACR>

## Step 8 : Compile, build container, and push to ACR

<Change Container from Linux to Windows?>

## Step 9 : Deploy Module

<Deployment Manifest -> Deploy >

## Step 10 : Run AI

## Step 11 : Clean up

# <span style="color:red"> Reference Content Below (to be deleted) </span>
[SqueezeNetObjectDetection:](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/EdgeModules/SqueezeNetObjectDetection/cs)


