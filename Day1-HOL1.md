# Windows Server IoT 2019 + Azure IoT Edge (45 Min)

In many use cases, a Windows Server IoT 2019 can be used an IoT edge gateway that connects local devices and sensors to the cloud services and apps. In this lab, we're going to walk you through how to turn a Windows Server IoT 2019 server into an IoT edge gateway. We will use virtual machines for this lab, however, the same steps described in this article can be applied to a Windows Server IoT 2019 on a physical machine.  

In this lab you learn how to:

1. Create an IoT Hub.
2. Register an IoT Edge device to your IoT hub.
3. Install and start the IoT Edge runtime on a Windows Server IoT 2019.
4. Remotely deploy a module (device simulator) to a Windows Server IoT 2019 to send telemetry to IoT Hub.
   Note: We are going to install a "Simulated Temperature Sensor"module from Azure IoT Edge Marketplace. This module generates temperature and humidity data.  

## Prerequisites
1. IoT Hub
2. Azure Account. If you don't have an active Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.
3. Windows Server 2019, which can be a physical or virtual machine  

## Step 1 : Create an instance of IoT Hub

### 1: Login to http://portal.azure.com

### 2. Select **All service** -> **Internet of Things** -> **IoT Hub** 

![create-iot-hub](images/WinServer-Lab/Create-IoTHub.png)
### 3: Click **Add** to add a new IotHub instance
    Select a subscription
    Select an existing Resource Group, or create a new one by clicking Create new link
    Select Region
    Provide a IoT Hub Name
![add-iot-hub](images/WinServer-Lab/add-iothub.png)

### 4: Click **Next: Size and scale>> **

    Select F1: Free tier for Pricing and scale tier

![select-tier](images/WinServer-Lab/IoTHub-FreeTier.png)
    
### 5: Click **Review + create**, to create the IoTHub instance

## Step 2 : Register the Windows Server IoT 2019 as a new Azure IoT Edge device

### 1: Navigate to the IoTHub that was created, select **IoT Edge** -> **Add an Edge device**

### 2: Provide a name of the device, then click **Save** to create the device

![add-edge-device](images/WinServer-Lab/create-edge-device.png)

### 3: View all devices

All the edge-enabled devices that connect to your IoT hub are listed on the **IoT Edge** page.

### Retrieve the connection string

INFO: When you're ready to set up your physical device, you'll need a connection string which links your physical device with its identity in IoT hub. 

1. From the **IoT Edge** page in the portal, click on the device ID from the list of Edge devices.
2. Copy the value of either **Connection string (primary key)** or **Connection string (secondary key)**. Save the connection string to a file for later part of the lab.

![save-connection-string](images/WinServer-Lab/save-connection-string.png)

## Step 3: Connect to your Windows Server on a virtual machine.

### 1. open a Remote Desktop Connection from your machine

INFO: you can type RDP from Window's search, then select then Remote Desktop Connection app

### 2. Type in the IP address to your server and click **connect**

### 3. Login to your server

## Step 4 : Install IoT Edge Runtime on Windows

### 1. Open a Powershell window as an Administrator

### 2. Run the **Deploy-IoTEdge** command, which checks whether your Windows machine is on a supported version, turns on the containers feature, and then downloads the moby runtime and the IoT Edge runtime. 

```powershell
. {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
Deploy-IoTEdge
```

### 3 Run the  Initialize-IoTEdge command to initialize the finish the IoT Edge installation

```powershell
. {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
Initialize-IoTEdge
```

### 4. Provide the device connection string (saved from prior step). 

![IoTEdge-Installation](images/WinServer-Lab/IotEdge-Installation.png)

### 6. Run the Get-Service command to confirm IoT Edge runtime is installed and running

```powershell
Get-Service iotedge
```

![edge-running](images/WinServer-Lab/EdgeRunning.png)

## Step 4 : Deploy Simulated Temperature Sensor from Marketplace to Windows Server

IoT Edge is used to connect devices and sensors to cloud. In this lab, we're going to use an existing simulator from Azure Marketplace. 

Azure Marketplace is an online applications and services marketplace where you can browse through a wide range of enterprise applications and solutions that are certified and optimized to run on Azure, including [IoT Edge modules](https://azuremarketplace.microsoft.com/marketplace/apps/category/internet-of-things?page=1&subcategories=iot-edge-modules).

### 1. From Azure portal, navigate to Marketplace or type Marketplace at the Search bar and select Marketplace

### 2. Within Marketplace, select **Get Started**, type in *simulated* at the search bar, then select Simulated Temperature Sensor 

### 3. Click **Create**
     
### 4. Fill out the information on the Target Devices for IoT Edge Module

1. Choose your subscription and the IoT Hub to which the target device is attached.

2. Choose **Deploy to a device**.

3. Enter the name of the device or select **Find Device** to browse among the devices registered with the hub and select the one you created earlier, which links to the Windows Server IoT 2019. 

4. Click **Create** to continue the standard process of configuring a deployment manifest, including adding other modules if desired. Details for the new module such as image URI, create options, and desired properties are predefined but can be changed. 

5. Click Next for the following steps, and finally click Submit to deploy the module to the Windows Server. 

## Step 5 : Confirm Deployment, and Watch Data Being Sent 

The module that you pushed creates sample data that you can use for testing. The simulated temperature sensor module generates environment data that you can use for testing later. The simulated sensor is monitoring both a machine and the environment around the machine. For example, this sensor might be in a server room, on a factory floor, or on a wind turbine. The message includes ambient temperature and humidity, machine temperature and pressure, and a timestamp. The IoT Edge tutorials use the data created by this module as test data for analytics.

Confirm that the module deployed from the cloud is running on your IoT Edge device.

```powershell
iotedge list
```

   ![View three modules on your device](./images/WinServer-Lab/iotedge-list-2.png)

View the messages being sent from the temperature sensor module to the cloud.

```powershell
iotedge logs SimulatedTemperatureSensor -f
```

   ![View the data from your module](./images/WinServer-Lab/iotedge-logs.png)

DONE!  