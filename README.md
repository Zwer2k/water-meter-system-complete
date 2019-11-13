# water-meter-system-complete

This repository is the sum of different projects to read out an analog water meter with the help of a camera and image processing, including neural network processing to extract the values.
The result is a HTTP-server, that takes an image as input, processes it and gives as an output the water meter number, including the subdigits.

**This is a dedicated Version and installation instruction for Raspberry PI3.**

The information about the usage can be found in the [main branch](https://github.com/jomjol/water-meter-system-complete)(Version 3.0.0). This is for sure not the most lean installation procedure as most probably way much less packages are needed as installed. But in order to remove error messages I followed the suggestions from different blogs to quickly make progress.

## Changelog
##### 2.0 Correction / detailed
* Base is a Raspberian Buster Lite (instead of Stretch Lite)
* Correction of minor changes in code (#keras)
##### 1.0 Initial Version

## Installation

This installation has been tested on a Raspberry Pi 3B.

Starting point is an installed **Raspberian Buster Lite**. It should also work with the desktop version.

#### Update and Install PIP3

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install python3-pip git
```

#### Install Tensorflow

```
pip3 install tensorflow 
```

#### Install  OpenCV, Pillow and Requests

```
sudo apt-get install python-opencv libqtgui4  libgstreamer1.0-0 libjasper1 libqt4-test libjpeg-dev zlib1g-dev  libfreetype6-dev liblcms1-dev libopenjp2-7  libtiff5 libatlas-base-dev python-setuptools libilmbase-dev libopenexr-dev libavformat-dev libavformat-dev libswscale-dev libv4l-dev
pip3 install opencv-python pillow requests
```

## Usage

After the installation of the environment and the dependencies you need to copy the code in a dedicated directory.
**Attention use the code in this branch, as there are some minor changes needed**

This can be done by a git-clone command:

```
git clone -b Raspberry-V3 https://github.com/jomjol/water-meter-system-complete
``` 

Then you can run the server. **Due to a problem with OpenCV a library needs to be loaded in advance. Start the code with the following command:**


```
cd water-meter-system-complete/code
LD_PRELOAD=/usr/lib/arm-linux-gnueabihf/libatomic.so.1 python3 wasseruhr.py
```


## Running in background

In order to run the server as a service in the background parallel to other applications and also have an automated restart in case of failures, I use the pm2 Process manager. To install it you need nodejs and npm:

```
sudo apt-get install nodejs npm
sudo npm install pm2 -g
```

After this you can use ```pm2 start 'LD_PRELOAD=/usr/lib/arm-linux-gnueabihf/libatomic.so.1 python3 wasseruhr.py'``` to have it running as a service. Be patient, it takes about 30 seconds to start and respond on the http request.

In order to have it persistent also after a restart or breakdown of the server do the following after the server has started:
``` 
pm2 save
pm2 startup
```

and follow the instruction followed the last prompt.





