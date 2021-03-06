# Equipment Activity Monitor in Python\*

## Introduction

This Equipment Activity Monitor application is part of a series of how-to Intel® Internet of Things (IoT) code sample exercises using the Intel® IoT Developer Kit, Intel® Edison board, Intel® IoT Gateway, cloud platforms, APIs, and other technologies.

From this exercise, developers will learn how to:<br>

- Connect the Intel® Edison board or Intel® IoT Gateway, computing platforms designed for prototyping and producing IoT and wearable computing products.<br>
- Interface with the Intel® Edison board or Arduino 101\* (branded Genuino 101\* outside the U.S.) board IO and sensor repository using MRAA and UPM from the Intel® IoT Developer Kit, a complete hardware and software solution to help developers explore the IoT and implement innovative projects.<br>
- Set up a web application server to let users store alarm data using Azure Redis Cache\* from Microsoft Azure\*, Redis Store\* from IBM Bluemix\*, or ElastiCache\* using Redis\* from Amazon Web Services (AWS)\*, different cloud services for connecting IoT solutions including data analysis, machine learning, and a variety of productivity tools to simplify the process of connecting your sensors to the cloud and getting your IoT project up and running quickly.
- Set up a MQTT-based server using IoT Hub from Microsoft Azure\*, IoT from IBM Bluemix\*, or IoT from Amazon Web Services (AWS)\*, different cloud machine to machine messaging services based on the industry standard MQTT protocol.

## What it is

Using an Intel® Edison board or Intel® IoT Gateway, this project lets you create a shop-floor equipment activity monitor that:<br>
- tracks equipment usage by monitoring sound and vibration sensors.<br>
- issues a visual notification whenever the equipment is in use.<br>
- logs equipment usage using cloud-based data storage.

## How it works

This equipment activity monitor watches for sound and vibration.

If both exceed a defined threshold, it lights up the display to indicate the equipment is in use.

Once the equipment is no longer used, it clears the display.

Optionally, equipment usage start/stop events can also be stored using the Intel® IoT Examples Datastore or an MQTT server running in your own Microsoft Azure\*, IBM Bluemix\*, or AWS\* account.

## Hardware requirements

This sample can be used with either the Grove\* Transportation and Safety Kit from Seeed Studio\*, or else the Starter Kit for Intel® Edison/Galileo from DFRobot\*.

Grove\* Starter Kit Plus, containing:

1. Intel® Edison board with an Arduino-compatible breakout board or Intel® IoT Gateway with Arduino 101
2. [Grove\* Sound Sensor](http://www.seeedstudio.com/depot/Grove-Sound-Sensor-p-752.html)
3. [Grove\* Piezo Vibration Sensor](http://www.seeedstudio.com/depot/Grove-Piezo-Vibration-Sensor-p-1411.html)
4. [Grove\* RGB LCD](http://iotdk.intel.com/docs/master/upm/node/classes/jhd1313m1.html)

DFRobot\* Starter Kit for Intel® Edison, containing:

1. Intel® Edison baord with an Arduino-compatible breakout board or Intel® IoT Gateway with Arduino 101
2. [Analog Sound Sensor](http://www.dfrobot.com/index.php?route=product/product&product_id=83).
3. [Digital Vibration Sensor](http://www.dfrobot.com/index.php?route=product/product&product_id=79)
4. [LCD Keypad Shield](http://iotdk.intel.com/docs/master/upm/node/classes/sainsmartks.html)

## Software requirements

1. Microsoft Azure\*, IBM Bluemix\*, or AWS\* account (optional)

### How to set up

To begin, clone the **How-To Intel IoT Code Samples** repository with Git\* on your computer as follows:

    $ git clone https://github.com/intel-iot-devkit/how-to-code-samples.git

To download a .zip file, in your web browser go to <a href="https://github.com/intel-iot-devkit/how-to-code-samples">https://github.com/intel-iot-devkit/how-to-code-samples</a> and click the **Download ZIP** button at the lower right. Once the .zip file is downloaded, uncompress it, and then use the files in the directory for this example.

### Installing the program manually on the Intel® Edison board

You can set up the code manually on the Intel® Edison board.

Clone the **How-To Intel IoT Code Samples** repository to your Intel® Edison board after you establish an SSH connection to it, as follows:

    $ git clone https://github.com/intel-iot-devkit/how-to-code-samples.git

Then, navigate to the directory with this example.

To install Git\* on the Intel® Edison board (if you don’t have it yet), establish an SSH connection to the board and run the following command:

    $ opkg install git

### Connecting the Grove\* sensors

![](./../../images/js/equipment-activity.jpg)

You need to have a Grove\* Shield connected to an Arduino\*-compatible breakout board to plug all the Grove\* devices into the Grove\* Shield. Make sure you have the tiny VCC switch on the Grove\* Shield set to **5V**.

1. Plug one end of a Grove\* cable into the Grove\* Sound Sensor, and connect the other end to the A0 port on the Grove\* Shield.

2. Plug one end of a Grove\* cable into the Grove\* Piezo Vibration Sensor, and connect the other end to the A2 port on the Grove\* Shield.

3. Plug one end of a Grove\* cable into the Grove\* RGB LCD, and connect the other end to any of the I2C ports on the Grove\* Shield.

### Connecting the DFRobot\* sensors

![](./../../images/js/equipment-activity-dfrobot.jpg)

You need to have a LCD Keypad Shield connected to an Arduino\* compatible breakout board to plug all the DFRobot\* devices into the LCD Keypad Shield.

1. Plug one end of a DFRobot\* cable into Analog Sound Sensor, then connect the other end to the A2 port on the LCD Keypad Shield.

2. Plug one end of a DFRobot\* cable into the Digital Vibration Sensor, then connect the other end to the A1 port on the LCD Keypad Shield.

### Intel® Edison board setup

If you're running this code on your Intel® Edison board, you need to install some dependencies by establishing an SSH session to the Edison and run the commands in the sections below.

#### Update the opkg repo

To add the opkg repository:

    $ echo "src mraa-upm http://iotdk.intel.com/repos/3.5/intelgalactic/opkg/i586" > /etc/opkg/mraa-upm.conf
    $ opkg update

You'll only need to perform this step once.

#### Git\*

To install Git\* on the Intel® Edison board (if you don’t have it yet):

    $ opkg update
    $ opkg install git

#### MRAA and UPM Dependencies

To install the latest versions of the MRAA and UPM libraries:

    $ opkg update
    $ opkg install mraa
    $ opkg install upm

#### Python\* Package Manager (pip)

To install the Python\* package manager needed to install and run the example:

    $ pip install --upgrade pip setuptools


#### Install the example

Once all dependencies are installed you can install the example itself with the following command:

    $ pip install --src ~/python/examples/ -e "git+https://github.com/intel-iot-devkit/how-to-code-samples.git#egg=iot_equipment_activity_monitor&subdirectory=equipment-activity-monitor/python"

The `pip` command will install required Python dependencies, save the source code for the example in `~/python/examples/iot_equipment_activity_monitor/` and link the package to the global Python `site-packages` folder.

### Intel® IoT Gateway setup

You can run this example using an Intel® IoT Gateway connected to an Arduino 101\* (branded Genuino 101\* outside the U.S.).

Make sure your Intel® IoT Gateway is setup, by following the directions on the web site here:

https://software.intel.com/en-us/node/633284

You must install the Intel® XDK on the Intel® IoT Gateway, by following the directions on the above link, under the section "Connecting to the Intel® XDK".

The Arduino 101 needs to have the Firmata\* firmware installed. If you have IMRAA installed on your gateway, this will be done automatically. Otherwise, install the StandardFirmata or ConfigurableFirmata sketch manually on to your Arduino 101.

You will also need to configure the `config.json` in the example to use the Arduino 101. See the section "Configuring the example" below.

### Data store server setup

Optionally, you can store the data generated by this sample program in a back-end database deployed using Microsoft Azure\*, IBM Bluemix\*, or AWS\*, along with Node.js\*, and a Redis\* data store.

For information on how to set up your own cloud data server, go to:

[https://github.com/intel-iot-devkit/intel-iot-examples-datastore](https://github.com/intel-iot-devkit/intel-iot-examples-datastore)

### MQTT server setup

You can also optionally store the data generated by this sample program using MQTT, a machine-to-machine messaging server. You can use MQTT to connect to Microsoft Azure\*, IBM Bluemix\*, or AWS\*.

For information on how to connect to your own cloud MQTT messaging server, go to:

[https://github.com/intel-iot-devkit/intel-iot-examples-mqtt](https://github.com/intel-iot-devkit/intel-iot-examples-mqtt)

## Configuring the example

When the example is installed through `pip` the `config.json` file that holds the configuration for the example lives in `~/python/examples/iot_equipment_activity_monitor/equipment-activity-monitor/python/iot_equipment_activity_monitor/config.json`.

To configure the example for the Grove\* kit, just leave the `kit` key in the `config.json` set to `grove`. To configure the example for the DFRobot\* kit, change the `kit` key in the `config.json` to `dfrobot` as follows:

```JSON
{
  "kit": "dfrobot",
  "VIBRATION_THRESHOLD": 100,
  "NOISE_THRESHOLD": 0
}
```

To configure the example for the Arduino 101, add a `PLATFORM` key with the value `firmata` to the `config.json`, as follows:

```JSON
{
  "kit": "grove",
  "PLATFORM": "firmata",
  "VIBRATION_THRESHOLD": 100,
  "NOISE_THRESHOLD": 0
}

To configure the example for the optional Microsoft Azure\*, IBM Bluemix\*, or AWS\* data store, add the `SERVER` and `AUTH_TOKEN` keys in the `config.json` file below as follows:

```JSON
{
  "kit": "grove",
  "VIBRATION_THRESHOLD": 100,
  "NOISE_THRESHOLD": 0,
  "SERVER": "http://intel-examples.azurewebsites.net/logger/access-control",
  "AUTH_TOKEN": "s3cr3t"
}
```

For information on how to configure the example for the optional Microsoft Azure\*, IBM Bluemix\*, or AWS\* MQTT messaging server, go to:

[https://github.com/intel-iot-devkit/intel-iot-examples-mqtt/](https://github.com/intel-iot-devkit/intel-iot-examples-mqtt/)

## Running the program manually

Once the example is installed through `pip` you can run the program by running the following command in an SSH session to the board:

    $ python -m iot_equipment_activity_monitor

### Determining the Intel® Edison board's IP address

You can determine what IP address the Intel® Edison board is connected to by running the following command:

    ip addr show | grep wlan

You will see the output similar to the following:

    3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast qlen 1000
        inet 192.168.1.13/24 brd 192.168.1.255 scope global wlan0

The IP address is shown next to `inet`. In the example above, the IP address is `192.168.1.13`.

IMPORTANT NOTICE: This software is sample software. It is not designed or intended for use in any medical, life-saving or life-sustaining systems, transportation systems, nuclear systems, or for any other mission-critical application in which the failure of the system could lead to critical injury or death. The software may not be fully tested and may contain bugs or errors; it may not be intended or suitable for commercial release. No regulatory approvals for the software have been obtained, and therefore software may not be certified for use in certain countries or environments.
