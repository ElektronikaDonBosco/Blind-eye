
# Jetson Nano Object detection alarm

Procedure to make inference in Jetson Nano.

## Set up Jetson Nano
First of all you should set up Jetson Nano, so a good way to get acquainted is to  
Go to [this](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#intro) step by step tutorial.

## Install dependecies and download packages

The next step will be to install python dependecies. For that open a terminal an execute the following commands.

```bash
sudo apt-get update
sudo apt-get install python3-pip -y
sudo apt-get install dialog -y # Download the model
sudo apt-get install v4l2loopback-dkms # To display the image
sudo modprobe v4l2loopback
sudo apt-get install nano 
```

## Prepare the docker container

To prepare the docker we need to clone the repository of jetson inference and enter the jetson_inference folder.
```bash
git clone https://github.com/mikelalda/Blind-eye.git

```

Clone jetson-inference repository

```bash
git clone https://github.com/dusty-nv/jetson-inference.git


```

Each time to run the container follow the next steps:

```bash
cd jetson-inference
docker/run.sh --volume path_to/Blind-eye/:/Blind-eye #You must use your own computer path.
```

## Run inference

In the file Alarm-Yolo/main.py we need to change the line 10 with ESP8266 IP address.

![](assets/2023-05-03_101412.png)

Also the change the wifi of the ESP8266 in line 13 of Arduino code.

![](assets/2023-05-03_101304.png)

Once having done all the steps, run this in the docker terminal.
 
```bash
cd /Blind-eye
python3 main.py
```
