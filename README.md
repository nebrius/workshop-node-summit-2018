# Node Summit 2017 NodeBots Workshop

In this workshop, we will be programming a Raspberry Pi using Node.js, [Johnny-Five](http://johnny-five.io/), and [Raspi IO](https://github.com/nebrius/raspi-io) to make Johnny-Five work on the Raspberry Pi. When using Raspi-IO, be sure to pay attention to the [pin naming scheme](https://github.com/nebrius/raspi-io/wiki/Pin-Information) as it can be a little confusing.

## First run

Connect to your Raspberry Pi using password `raspi`. If you're running Windows, you'll need to install an SSH client if you haven't already. You can use [Git BASH](https://git-scm.com/downloads), [PuTTY](https://putty.org/), or [Windows Subsystems for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10).

```
ssh pi@rpi##.local
cd nodebot && npm install johnny-five raspi-io
```

Replace `##` with the number printed on top of the Ethernet port on your Raspberry Pi.

## Introduction

The Raspberry Pi's provided come with Linux and Node.js preinstalled.

1. Navigate to the `/home/pi/nodebot` folder.
2. Create an empty Node.js project with `npm init`. You can leave all values as their defaults.
3. Install Johnny-Five and Raspi IO with `npm install johnny-five raspi-io`
4. Mount the source folder from your Raspberry Pi on your laptop by connecting over SMB.
    1. If you're on Windows, enter `\\rpi##.local\nodebot` in the address bar in Windows Explorer.
    2. If you're in macOS, open Finder, hit cmd+k, and enter `smb://rpi##.local/nodebot` in the `Server Address` field and click `Conenct`
    3. If you're on Linux, you'll need to check the documentation for your distro.
5. Open the mounted folder using VS Code.
6. Let's get to editing!

If this all looks intimidating to you, don't worry! We will go through these steps together.

## Hello Raspi-IO

For the this part of the workshop, we will build the "Hello World" of hardware: getting an LED to blink! For this part of the workshop we will build hello world together using the following schematic:

![Hello Raspi-IO Schematic](https://nebri.us/static/node-summit-2017-workshop-1.png)

The objective is to make the LED blink once per second. Take a look at the [Led](http://johnny-five.io/api/led/) class in Johnny-Five. Remember to check the [pin naming scheme](https://github.com/nebrius/raspi-io/wiki/Pin-Information) to see what the pin number should be!

## Distributed Environmental Sensing System

For this part of the workshop, we will build a distributed environmental sensing system. For this part of the workshop, use the following schematic:

![HDistributed Temperature Sensor Schematic](https://nebri.us/static/node-summit-2017-workshop-2.png)

For this part of the workshop, we will build two parts: the client and a server.

### Client

In this case, the "client" is the Raspberry Pi itself. The client needs to do the following:

1. Read the temperature, pressure, and humidity from the [BME280 sensor](http://johnny-five.io/examples/multi-BME280/) provided in the kit.
2. If the temperature gets too high or too low, then trigger an alarm
    1. Set the low threshold to 3 degrees below room temperature, and the high threshold to 3 degrees above room temperature. This way, you can make it warmer or cooler by blowing on it.
    2. When an alarm is triggered, flash the LED four times per second
    3. Write some code so that it turns the alarm off when the [button](http://johnny-five.io/api/button/) is pressed.
3. Send the sensor data and the alarm status to the server

### Server

In this case, the "server" will be a Node.js process running on your local laptop. The server needs to do the following:

1. Listen for clients that send sensor data to it and store it in memory
1. Serve a basic web page that displays the current sensor data from all connected Raspberry Pis to the user
1. Shows when a temperature alarm is triggered
1. Provides a button in the web page for a user to turn the alarm off

I recommend using [socket.io](https://socket.io/) to handle the connection to make it easier for the server to tell the client to turn an alarm off. This can, however, be done with REST calls if you prefer.

For bonus points, team up with a neighbor and make sure that connecting two or more Raspberry Pi's to the same server works.

# License

MIT License

Copyright (c) 2018 Bryan Hughes <bryan@nebri.us>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
