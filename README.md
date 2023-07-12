Before starting with the description of the project, we would like to thanks MikelAlda for the help given during the project development.

# Jetson Nano Object detection sensor

The main objetive of this project is to gain the ability to distinguish different object and living beings with the use of a webcam. So thanks to the development of the technology we are able to do such things and once we are able to detect what each thing is this aplication could be very helpful for visually-impaired people.
The software will be able to analyze the different things he sees and then he would be able to transmit the information to the user.
There will be 3 vibrators (left, center, right) conected to a NodeMCU device. When the jetson nano detects one element the vibrator asociated to that side will vibrate.
The communication between the jetson nano and the NodeMCU is done trought Wi-Fi.

## Material used in the project
-Jetson Nano

-Webcam

-Vibrators

-Leds

-ESP826MOD Sensor module (NodeMCU)

## -ESP826MOD (NodeMCU) Sensor Module Schematic Pinout
<img src="https://github.com/ElektronikaDonBosco/Blind-eye/blob/master/60893535def1e6e04c6f55b835bcd917.jpg" width=50% height=50%>

## Jetson Nano set up
In the following lines, you will see the procedure to make inference in the Jetson Nano code we have used.

First of all, you have to set up your Jetson Nano, so a good way is to  
go to [this](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#intro) step by step tutorial.

## Install dependecies and download packages

The next step is to install the python dependecies. In order to do that, open a terminal an execute the following commands.

```bash
sudo apt-get update
sudo apt-get install python3-pip -y
sudo apt-get install dialog -y # Download the model
sudo apt-get install v4l2loopback-dkms # To display the image
sudo modprobe v4l2loopback
sudo apt-get install nano 
```

## Prepare the docker container

To prepare the docker, we need to clone the repository of jetson inference and enter the jetson_inference folder.
```bash
git clone https://github.com/ElektronikaDonBosco/Blind-eye.git

```

To clone the jetson-inference repository, use the next command:

```bash
git clone https://github.com/dusty-nv/jetson-inference.git


```

Each time you want to run the container, follow the next code:

```bash
cd jetson-inference
docker/run.sh --volume /home/donbosco/jetson-inference/Blind-eye/:/Blind-eye #Beware that you must use your own computer path.
```

## Run inference

1 - The NodeMCU must connect to the Wi-Fi to get information from the jetson nano. We must set the Wi-Fi network and the password of the network in the NodeMCU code. It will be necessary to change the Wi-Fi of the ESP8266 (NodeMCU) in line 13 of the code. You have that code inside the folder "Arduino". When you transfer the program to the NodeMCU device it will send the IP in the serie port, if you open the SerialMonitor you will see the IP. It is neccessary to know the IP in the next point.

![](assets/2023-05-03_101304.png)

2 - In the file "Blind-Eye/main.py", we need to set the ESP8266 (NodeMCU) IP address in line 10. The jetson nano must know the IP address of the NodeMCU, and it is set here. You can see the Blind-Eye instalation process by clicking [this](https://github.com/ElektronikaDonBosco/Blind-Eye) guide.

![](assets/2023-05-03_101412.png)

3 - Open a Terminal window and run docker
```bash
cd jetson-inference
docker/run.sh --volume home/donbosco/Blind-Eye:/Blind-Eye
```
It will ask for the password you created in the Operating System: "donbosco" in our case

4 - Run the python code
```bash
cd /Blind-eye/
python3 main.py
```

NOTE: if the jetson nano can not connect to the NodeMCU the jetson nano code will stop.
