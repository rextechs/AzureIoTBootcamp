---
title: Secure OPC UA client and OPC UA server application using OPC Vault - Azure | Microsoft Docs
description: Secure OPC UA client and OPC UA server application with a new key pair and certificate using OPC Vault.
author: dominicbetts
ms.author: dobett
ms.date: 11/26/2018
ms.topic: conceptual
ms.service: iot-industrialiot
services: iot-industrialiot
manager: philmea
---

# Secure OPC UA client and OPC UA server application 
OPC Vault is a microservice that can configure, register, and manage certificate lifecycle for OPC UA server and client applications in the cloud. This article shows you how to secure an OPC UA client and an OPC UA server application with a new key pair and certificate using OPC Vault.

In the following setup, the OPC client is testing the connectivity to the OPC PLC. By default, the connectivity is not possible because both components have not yet been provisioned with the right certificates. In this workflow, we do not use the OPC UA components self-signed certificates and sign them via OPC Vault. See the previous [testbed](howto-opc-vault-deploy-existing-client-plc-communication.md). Instead, this testbed provisions the components with a new certificate as well as with a new private key that are both generated by OPC Vault. Some background information on OPC UA security can be found in this [whitepaper](https://opcfoundation.org/wp-content/uploads/2014/05/OPC-UA_Security_Model_for_Administrators_V1.00.pdf). The complete information can be found in the OPC UA specification.

Testbed: The following environment is configured for testing.

OPC Vault scripts:
- Secure OPC UA client and OPC UA server applications with a new key pair and certificate using OPC Vault.

> [!NOTE]
> For more information, see the GitHub [repository](https://github.com/Azure-Samples/iot-edge-industrial-configs#testbeds).

## Generate a new certificate and private key 
**Preparation**
- Ensure that the environment variables `$env:_PLC_OPT` and `$env:_CLIENT_OPT` are undefined. For example, `$env:_PLC_OPT=""` in your PowerShell
- Set the environment variable `$env:_OPCVAULTID` to a string that allows you to find your data again in OPC Vault. We recommend setting it to a 6-digit number. For our example, "123456" was used as value for the variable.
- Ensure there is no docker volume `opcclient` or `opcplc`. Check with `docker volume ls` and remove them with `docker volume rm <volumename>`. You may need to remove also containers with `docker rm <containerid>` if the volumes are still used by a container.

**Quickstart**
1. Go to the [OPC Vault website](https://opcvault.azurewebsites.net/)

1. Select `Register New`

1. Enter the OPC PLC information as it was shown in the previous testbed's log output `CreateSigningRequest information` area into the input fields on the `Register New OPC UA Application` page, select `Server` as ApplicationType.

1. Select `Register`

1. On the next page, `Request New Certificate for OPC UA Application` select `Request new KeyPair and Certificate`

1. On the next page, `Generate a new Certificate with a Signing Request` paste in the `CSR (base64 encoded)` string from the log output into the `CreateRequest` input field. Ensure you copy the full string.

1. On the next page, `Request New Certificate for OPC UA Application` select `Request new Certificate with Signing Request`

1. On the next page `Generate a new KeyPair and for an OPC UA Application` enter `CN=OpcPlc` as SubjectName, `opcplc-<_OPCVAULTID>` (replace `<_OPCVAULTID>` with yours) as DomainName, select `PEM` as PrivateKeyFormat and enter a password (we refer later to it as `<certpassword-string>`)

1. Select `Generate New KeyPair`

1. You are now moving forward to `View Certificate Request Details`. On this page, you can download all required information to provision the certificate stores of `opc-plc`.

1. On this page:  
    - Select `Certificate` in `Download as Base64` and copy the text string presented in the `EncodedBase64` field and store it for later use. We refer to it as `<applicationcertbase64-string>` later on. Select `Back`.
    - Select `PrivateKey` in `Download as Base64` and copy the text string presented in the `EncodedBase64` field and store it for later use. We refer to it as `<privatekeybase64-string>` later on. Select `Back`.
    - Select `Issuer` in `Download as Base64` and copy the text string presented in the `EncodedBase64` field and store it for later use. We refer to it as `<addissuercertbase64-string>` later on. Select `Back`.
    - Select `Crl` in `Download as Base64` and copy the text string presented in the `EncodedBase64` field and store it for later use. We refer to it as `<updatecrlbase64-string>` later on. Select `Back`.

1. Now set in your PowerShell a variable named `$env:_PLC_OPT`:

   `$env:_PLC_OPT="--applicationcertbase64 <applicationcertbase64-string> --privatekeybase64 <privatekeybase64-string> --certpassword <certpassword-string> --addtrustedcertbase64 <addissuercertbase64-string> --addissuercertbase64 <addissuercertbase64-string> --updatecrlbase64 <updatecrlbase64-string>"`  

    Replace the strings passed in as option values Base64 strings you fetched from the website.  

1. Repeat the complete process starting with `Register New` for the OPC client. There are only the following differences you need to be aware of:
    - Use the log output from the `opcclient`.
    - Select `Client` as ApplicationType during registration.
    - Use `$env:_CLIENT_OPT` as name of the PowerShell variable.

    > [!NOTE] 
    > While working with this scenario, you may have recognized that the `<addissuercertbase64-string>` and `<updatecrlbase64-string>` values are identical for `opcplc` and `opcclient`. This is true for our use case and can save you some time while doing the steps.

**Quickstart**

Run the following PowerShell command in the root of the repository:

```
docker-compose -f connecttest.yml up
```

**Verification**

Verify that the two components have not had an existing application certificate. Check the log output. Below is the output of OPC PLC, and OPC client has a similar log output.

```
opcplc-123456 | [13:40:08 INF] There is no existing application certificate.
```
If there is an application certificate, remove the docker volumes as explained in the preparation steps.

Verify in the log that the OPC Vault CA certificate was installed in the issuer certificate store as well as in the trusted peer certificate store. Below is the log output of OPC PLC, and OPC Client has a similar log output. 

```
opcplc-123456 | [13:40:09 INF] Trusted issuer store contains 1 certs
opcplc-123456 | [13:40:09 INF] 01: Subject 'CN=Azure IoT OPC Vault CA, O=Microsoft Corp.' (thumbprint: BC78F1DDC3BB5D2D8795F3D4FF0C430AD7D68E83)
opcplc-123456 | [13:40:09 INF] Trusted issuer store has 1 CRLs.
opcplc-123456 | [13:40:09 INF] 01: Issuer 'CN=Azure IoT OPC Vault CA, O=Microsoft Corp.', Next update time '10/19/2019 22:06:46'
opcplc-123456 | [13:40:09 INF] Trusted peer store contains 1 certs
opcplc-123456 | [13:40:09 INF] 01: Subject 'CN=Azure IoT OPC Vault CA, O=Microsoft Corp.' (thumbprint: BC78F1DDC3BB5D2D8795F3D4FF0C430AD7D68E83)
opcplc-123456 | [13:40:09 INF] Trusted peer store has 1 CRLs.
opcplc-123456 | [13:40:09 INF] 01: Issuer 'CN=Azure IoT OPC Vault CA, O=Microsoft Corp.', Next update time '10/19/2019 22:06:46'
opcplc-123456 | [13:40:09 INF] Rejected certificate store contains 0 certs
```
The OPC PLC does now trust all OPC UA clients with certificates signed by OPC Vault.

Verify in the log that the private key format is recognized as PEM and that the new application certificate is installed. Below is the log output of OPC PLC, and OPC client has a similar log output. 

```
opcplc-123456 | [13:40:09 INF] The private key for the new certificate was passed in using PEM format.
opcplc-123456 | [13:40:09 INF] Remove the existing application certificate.
opcplc-123456 | [13:40:09 INF] The new application certificate 'CN=OpcPlc' and thumbprint 'A3CB288FC1D2B7A5C08AACF531CF4A85E44A6C4C' was added to the application certificate store.
opcplc-123456 | [13:40:09 INF] Activating the new application certificate with thumbprint 'A3CB288FC1D2B7A5C08AACF531CF4A85E44A6C4C'.
```

The application certificate and the private key are now installed in the application certificate store and used by the OPC UA application.

Verify that the connection between the OPC client and OPC PLC can be established successfully and the OPC client can successfully read data from OPC PLC. You should see the following output in the OPC client log output:
```
opcclient-123456 | [13:40:12 INF] Create secured session for endpoint URI 'opc.tcp://opcplc-123456:50000/' with timeout of 10000 ms.
opcclient-123456 | [13:40:12 INF] Session successfully created with Id ns=3;i=941910499.
opcclient-123456 | [13:40:12 INF] The session to endpoint 'opc.tcp://opcplc-123456:50000/' has 4 entries in its namespace array:
opcclient-123456 | [13:40:12 INF] Namespace index 0: http://opcfoundation.org/UA/
opcclient-123456 | [13:40:12 INF] Namespace index 1: urn:OpcPlc:opcplc-123456
opcclient-123456 | [13:40:12 INF] Namespace index 2: http://microsoft.com/Opc/OpcPlc/
opcclient-123456 | [13:40:12 INF] Namespace index 3: http://opcfoundation.org/UA/Diagnostics
opcclient-123456 | [13:40:12 INF] The server on endpoint 'opc.tcp://opcplc-123456:50000/' supports a minimal sampling interval of 0 ms.
opcclient-123456 | [13:40:12 INF] Execute 'OpcClient.OpcTestAction' action on node 'i=2258' on endpoint 'opc.tcp://opcplc-123456:50000/' with security.
opcclient-123456 | [13:40:12 INF] Action (ActionId: 000 ActionType: 'OpcTestAction', Endpoint: 'opc.tcp://opcplc-123456:50000/' Node 'i=2258') completed successfully
opcclient-123456 | [13:40:12 INF] Value (ActionId: 000 ActionType: 'OpcTestAction', Endpoint: 'opc.tcp://opcplc-123456:50000/' Node 'i=2258'): 10/21/2018 13:40:12
```
If you see this output, then the OPC PLC is now trusting the OPC client and vice versa, since both have now certificates signed by a CA and both trust certificates that were signed by this CA.

### A testbed for OPC Publisher ###

**Quickstart**

Run the following PowerShell command in the root of the repository:
```
docker-compose -f testbed.yml up
```

**Verification**
- Verify that data is sent to the IoTHub you configured by setting `_HUB_CS` using [Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) or [iothub-explorer](https://github.com/Azure/iothub-explorer).
- OPC test client is going to use IoTHub direct method calls and OPC method calls to configure OPC Publisher to publish/unpublish nodes from the OPC test server.
- Watch the output for error messages.

## Next steps

Now that you have learned how to deploy OPC Vault to an existing project, here is the suggested next step:

> [!div class="nextstepaction"]
> [Deploy OPC Twin to an existing project](howto-opc-twin-deploy-existing.md)