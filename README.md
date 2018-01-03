# IoT Hub Trigger Task
Use this task to trigger your instance of Azure IoT Hub to send messages to devices.

## What you have to specify
1. Connections string
2. The rest api to query the devices.
3. The SAS Token (auth key) to access IoT Hub.
4. An Id for the message.
5. The message.

### SAS Token
A SAS Token look like this *SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501*. It can be generated with the **Device Explorer Tool** (https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer), that can be downloaded <a href="https://github.com/Azure/azure-iot-sdk-csharp/releases">here</a>.
### Base64 Encoding
The generated SAS Token from the Device Explorer needs to be Encoded, as it contains characters that will be further encoded, which would make the token invalid.
You can use PowerShell to encode the token.

    $sasToken = "<Paste your Token>"
    $b = [System.Text.Encoding]::UTF8.GetBytes($sasToken)
    [System.Convert]::ToBase64String($b)
The commands will display the encoded string.

## Known issues with G_VERSION
- Auth key has to be Base 64 encoded. (I experienced some troubles in passing in an un-encoded string so this is a temporary workaround)
- Your message should be plain text without fancy characters. (Not sure yet what exactly fancy means, you can do some experiments if you want, but be warned. This will be addressed in future versions )

You can find all the necessary keys in Azure portal.

This is an open source project which can be found [here](https://github.com/DanielMeixner/vsts-task-iothub). (https://github.com/DanielMeixner/vsts-task-iothub) 

The idea behind is to use Visual Studio Team Services in "DevOps for IoT" or "DevOps for Devices" scenarios as described in my blogpost [here](https://blogs.msdn.microsoft.com/dmx/2017/01/26/devops-for-iot-part-1/). 
(https://blogs.msdn.microsoft.com/dmx/2017/01/26/devops-for-iot-part-1/)
