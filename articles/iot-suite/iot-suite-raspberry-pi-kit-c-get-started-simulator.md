---
title: Connect a Raspberry Pi to Azure IoT Suite using C with simulated telemetry | Microsoft Docs
description: Use the Microsoft Azure IoT Starter Kit for the Raspberry Pi 3 and Azure IoT Suite. Use C to connect your Raspberry Pi to the remote monitoring solution, send simulated telemetry to the cloud, and respond to methods invoked from the solution dashboard.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''

ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/24/2017
ms.author: dobett

---
# Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud. The tutorial uses:

- Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.
- The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> The remote monitoring solution provisions a set of Azure services in your Azure subscription. The deployment reflects a real enterprise architecture. To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it. If you need the preconfigured solution again, you can easily recreate it. For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## Download and configure the sample

You can now download and configure the remote monitoring client application on your Raspberry Pi.

### Clone the repositories

If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:

`cd ~`

`git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git`

### Update the device connection string

Open the sample source file in the **nano** editor using the following command:

`nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c`

Locate the following lines:

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial. Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).

## Build the sample

Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:

`sudo apt-get update`

`sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev`

You can now build the updated sample solution on the Raspberry Pi:

`chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh`

`~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh`

You can now run the sample program on the Raspberry Pi. Enter the command:

  `sudo ~/cmake/remote_monitoring/remote_monitoring`

The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:

![Output from Raspberry Pi app][img-raspberry-output]

Press **Ctrl-C** to exit the program at any time.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## Next steps

Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
