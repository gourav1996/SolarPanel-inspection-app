# SolarPanel Inspection App
Photovoltaic energy is one of most promising among renewable energy sources.
To assure optimal continuous solar power production, thermography scans should be performed at regular intervals to assess preventive maintenance needs.
Panels get overheated due to shade, defective cells, or substrings consuming instead of producing power, the module efficiency can drop by 0.5% per Kelvin. A panel temperature rise of 18 °F (10 °C) as compared with an average temperature of other panels can lower the power yield by as much as 5%.
Thermal imaging helps to identify mismatched panels where high performing modules are impeded by lower performing modules and overheated connections.

The solar panel hotspots create two
issues:

 • Fall in overall power production
  since cells consume power
  instead of producing.

 • Power consumption continues
 to heat up cells and affect the
 production of neighboring cells.
## 
Panels might be non-functioning due to miswired panels or worn/defective cables. This condition is indicated when the entire panel is hotter
when compared to others.

![Common defects](resources/solarPanelDefects.png)

To do the preventive maintenance SolarPanel-inspection-app can help in detection of defected panels.
![Solar Panel Thermal Image](resources/solarpanelThermalImage.png)


## Index

1. [Introduction](#Introduction)
2. [Deepstream Setup](#Deepstream-Setup)
    1. [Install System Dependencies](#Install-System-Dependencies)
    2. [Install Deepstream](#Install-Deepstream)
3. [Running the Application](#Running-the-Application)
    1. [Clone the repository](#Cloning-the-repository)
    2. [Run with different input sources](#Run-with-different-input-sources)
    
## Introduction

Hermes Application consists of two parts. An Intelligent Video Analytics Pipeline powered by Deepstream and NVIDIA Jetson Xavier NX and a reconnaissance drone, for which I have used a Ryze Tello.

![Jetson Nx](resources/processed.jpeg)

This project is a proof-of-concept, trying to show that surveillance and mapping of wildfires can be done with a drone and an onboard Jetson platform.

## Deepstream Setup

This post assumes you have a fully functional Jetson device. If not, you can refer the documentation [here](https://docs.nvidia.com/jetson/jetpack/install-jetpack/index.html).

### 1. Install System Dependencies

```sh
sudo apt install \
libssl1.0.0 \
libgstreamer1.0-0 \
gstreamer1.0-tools \
gstreamer1.0-plugins-good \
gstreamer1.0-plugins-bad \
gstreamer1.0-plugins-ugly \
gstreamer1.0-libav \
libgstrtspserver-1.0-0 \
libjansson4=2.11-1
```

### 2. Install Deepstream

Download the DeepStream 5.0.1 Jetson Debian package `deepstream-5.0_5.0.1-1_arm64.deb`, to the Jetson device from [here](https://developer.nvidia.com/assets/Deepstream/5.0/ga/secure/deepstream_sdk_5.0.1_amd64.deb). Then enter the command:

```sh
sudo apt-get install ./deepstream-5.0_5.0.1-1_arm64.deb
```

## Running the Application

### 1. Clone the repository

This is a straightforward step, however, if you are new to git or git-lfs, I recommend glancing threw the steps.

First, install git and git-lfs

```sh
sudo apt install git git-lfs
```

Next, clone the repository

```sh
# Using HTTPS
git clone https://github.com/aj-ames/Hermes-Deepstream.git

#```

Finally, enable lfs and pull the yolo weights

```sh
git lfs install
git lfs pull
```

### 2. Run with different input sources

The computer vision part of the solution can be run on one or many input sources of multiple types, all powered using NVIDIA Deepstream.

First, build the application by running the following command:

```sh
make clean && make -j$(nproc)
```

This will generate the binary called `SolarPanel-inspection-app`. This is a one-time step and you need to do this only when you make source-code changes.

Next, create a file called `inputsources.txt` and paste the path of videos or rtsp url.

```sh
file:///home/gourav/Videos/v1.mp4
rtsp://admin:admin%40123@192.168.1.1:554/stream
```

Now, run the application by running the following command:

```sh
./SolarPanel-inspection-app
```

Finally, add the url in `inputsources.txt` and start `./SolarPanel-inspection-app`.


## Citations

* [AlexeyAB/darknet](https://github.com/AlexeyAB/darknet)
* [Solar panel Thermography](http://www.murcal.com/pdf%20folder/15.testo_thermography_guide.pdf)
* [HermesApp](https://github.com/aj-ames/Hermes-Deepstream)
