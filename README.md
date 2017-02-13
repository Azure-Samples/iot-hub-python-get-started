---
services: iot-hub
platforms: python
author: msonecode
---

# How to get started for using IoT Hub REST API in Python

## About this sample
The sample project demonstrates how to get started for using IoT Hub REST API in Python.

The REST APIs for IoT Hub offer programmatic access to the device and messaging services, as well as the resource provider, in IoT Hub. You can access messaging services within an IoT service running in Azure, or you can directly over the Internet from any application that can send an HTTP/HTTPS request and receive an HTTP/HTTPS response. You can visit the [IoT Hub REST API references](https://msdn.microsoft.com/en-us/library/azure/mt548492.aspx) on Microsoft Azure official site to learn more about these APIs, requirements, parameters, request and response via HTTP methods.

In the sample project, steps at below will be proivded for us to get started.

1. Create an IoT Hub through Azure Portal.
2. Get the connection information from the settings on Azure portal.
3. A simple Python script shows how to create a device identity at the IoT Hub, list all registered device identities from IoT Hub.
4. A simple Python script shows how to send messages from the simulated device application to IoT Hub.


## Create an IoT Hub through Azure Portal

To do this, refer to the article [Create an IoT Hub through Azure Portal](https://azure.microsoft.com/documentation/articles/iot-hub-csharp-csharp-getstarted/#create-an-iot-hub).



## Get the connection information
- Getting the IoT Hub **Hostname**

    Copy the IoT Hub **Hostname** at the dashboard.

    ![Copy the IoT Hub Hostname at the dashboard](./Images/4.png)

- Getting the **Shared access key** and **Connection string** of the policy

    Click the **Key** button to show the **Shared access policies**, then select one policy, then copy the **Shared access key** and **Connection string**.

    ![Click the Key button to show the Shared access policies](./Images/5.png)

    ![Copy the Shared access key and Connection string](./Images/6.png)

## Building the sample
You can use Eclipse with PyDev Plugin to import the sample project.
### Preparation
- Install the Python package **requests** via command pip install requests
- Download [Eclipse](https://eclipse.org/downloads/)
- Install PyDev plugin via Eclipse Marketplace, click **Help** -> **Eclipse Marketplace**, then input **PyDev** in the search box and enter, then click the **install** button and follow the tips to install until **Finish** and restart Eclipse.

    ![Install PyDev plugin via Eclipse Marketplace](./Images/7.png)

    ![Input PyDev in the search box and enter](./Images/8.png)

### Import the sample project
1. Open the Eclipse.
2. Click **File** -> **Import**.

    ![Click File -> Import](./Images/9.png)

3. Select **General** -> **Existing Projects into Workspace**, then click **Next**.

    ![Select General -> Existing Projects into Workspace](./Images/10.png)

4. Select the sample project path via **Browse**, then click **Finish**.

    ![Select the sample project path via Browse](./Images/11.png)

5. See the **PyDev Package Explorer**.

    ![See the PyDev Package Explorer](./Images/12.png)

## Running the sample
There are two scripts separately at the **service** and **device** directories:

- service/deviceManager.py: Using [Device Indentities REST APIs](https://msdn.microsoft.com/en-us/library/azure/mt548489.aspx) to create a new device identity, retrieve a device identity, and list device identities.

- device/d2cMsgSender.py: Using [Send device-to-cloud message](https://msdn.microsoft.com/en-US/library/azure/mt590784.aspx) API to send device-to-cloud message from the simulated device application to IoT Hub.

You can open the Python script on Eclipse, and click the right mouse button at the script window, then click the **Run As** -> **2 Python Run** to run the script, then see the result at the **Console** Window.

![Click the Run As -> 2 Python Run to run the script](./Images/13.png)

## Code sample running result
The results for running `service/deviceManager.py`:


1. The result for calling the function `createDeviceId(deviceId)`

    - Creating an non-existed device identity, the result as below.
    ```
    (u'{"deviceId":"iotdevice3","generationId":"635937464376399955","etag":"MA==","connectionState":"Disconnected","status":"enabled","statusReason":null,"connectionStateUpdatedTime":"0001-01-01T00:00:00","statusUpdatedTime":"0001-01-01T00:00:00","lastActivityTime":"0001-01-01T00:00:00","cloudToDeviceMessageCount":0,"authentication":{"symmetricKey":{"primaryKey":"PqZ70GzRIOv8Mfap31nzDjwqsRwt8X6VTLDUM48qDGk=","secondaryKey":"gZfLMBuwgNDOuYbJZNK8ZXLGCm5WJba4CVGvXBV/0qM="}}}', 200)
    ```
    - If trying to create an existed device identity, an error information will be shown.

    ```
    (u'{"Message":"ErrorCode:DeviceAlreadyExists;A device with ID \'iotdevice1\' is already registered.\r\nTracking Id:218b497e330b41119036553381cc63de-G:GatewayWorkerRole.11-B:1-P:8a500395-cf20-45f1-831b-e0a49c9bd5fa-TimeStamp:03/16/2016 17:26:37\r\nErrorCode:DeviceAlreadyExists"}', 409)
    ```

2. The result for calling the function `retrieveDeviceId(deviceId)`
    ```
    (u'{"deviceId":"iotdevice1","generationId":"635928930091746067","etag":"MA==","connectionState":"Disconnected","status":"enabled","statusReason":null,"connectionStateUpdatedTime":"2016-03-16T09:46:02.5862088","statusUpdatedTime":"0001-01-01T00:00:00","lastActivityTime":"2016-03-16T09:46:02.5862088","cloudToDeviceMessageCount":0,"authentication":{"symmetricKey":{"primaryKey":"F+x9Sg9zVZC+TWnrQ1vXm0sYH/SAtvv6Wa5WhWnHdQo=","secondaryKey":"vZaSU6/8Mah4Chu28Vzx07/Feqe1a2EeDeUNEo9EY10="}}}', 200)
    ```

3. The result for calling the function `listDeviceId()` lists all the registered device identities.
    ```
    (u'[{"deviceId":"iotdevice1","generationId":"635928930091746067","etag":"MA==","connectionState":"Disconnected","status":"enabled","statusReason":null,"connectionStateUpdatedTime":"2016-03-16T09:46:02.5862088","statusUpdatedTime":"0001-01-01T00:00:00","lastActivityTime":"2016-03-16T09:46:02.5862088","cloudToDeviceMessageCount":0,"authentication":{"symmetricKey":{"primaryKey":"F+x9Sg9zVZC+TWnrQ1vXm0sYH/SAtvv6Wa5WhWnHdQo=","secondaryKey":"vZaSU6/8Mah4Chu28Vzx07/Feqe1a2EeDeUNEo9EY10="}}}]', 200)
    ```

The result for running `device/d2cMsgSender.py` includes the empty content and status code 204 from the response if message is sent successfully:
```
(u'', 204)
```
