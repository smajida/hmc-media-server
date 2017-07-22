HMC Media Server
================
[![Join the chat at https://gitter.im/hmcmediaserver/lobby](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/hmcmediaserver/lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

[HMC Media Server] is trying to solve a very fundamental problem most of us are facing.

> How do I organize my own media files using a software that offers similiar features as these provided by the cloud based services? 

We keep our media files created using various devices and upload some of them to the cloud based services usch as Flickr, Google Photos, Facebook or Amazon Prime Photo. The media files are usually locked away stored in the storage devices that rarely get accessed.

[HMC Media Server] will unlock these media files (photos, audios and videos) so that you can enjoy the media files inside you home with high speed network. The application also supports Apple TV and Chromecast that you can stream your media files to your big screens.

## Download Links
**[HMC Media Server]** is a Java based web application to help manage your media libraries.

* HMC Media Server for Unix/Linux/OSX: [hmc-1.3.0-BETA1.tar.gz](https://drive.google.com/file/d/0B3yQIDinGlTfcFN4MmhKVHFlX2c/view?usp=sharing)
* HMC Media Server for Windows: [hmc-1.3.0-BETA1.zip](https://drive.google.com/file/d/0B3yQIDinGlTfTXYxaGZ2cGwwZ00/view?usp=sharing)
* [FaceNet Plug-in (Linux/OSX)](#facenet): [tf_serving-1.0.0-BETA1.tar.gz](https://drive.google.com/file/d/0B3yQIDinGlTfcFZsU2dTTUdhenM/view?usp=sharing)). This package has been tested under Ubuntu 16.04, Ubuntu 14.04, CentOS 7 and Mac/OSX. The Windows platform is not supported natively. Alternatively, you can install the FaceNet Plug-in as a remote service hosted by a supported OS natively or as a VM.

## Install Native Software Dependencies

### Windows (64bit)
The native software dependencies for Windows (64bit) are included as part of the software distributions. **FFmpeg** is an optional software dependency that allows **HMC Media Server** to transcode video clips into streaming friendly x264 format using web browsers.

1. Download the 64bit static linked FFmpeg from the link below:
> http://ffmpeg.zeranoe.com/builds/win64/static/ffmpeg-3.3.2-win64-static.zip  

1. Open the package and copy **ffmpeg.exe** to the **bin/windows_x86_64** sub-directory.

### OS X (64bit)

1. Install **HomeBrew**
> /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  

1. Use **brew** to install software dependencies
> brew cask install java  
> brew install ImageMagick  
> brew install dcraw  
> brew install ffmpeg  
> brew install exiftool  
> brew install jhead  

1. Verify the dependencies are installed correctly
> which java  
> which convert  
> which ffmpeg  
> which jpegtran  
> which exiftool  
> which dcraw  
> which jhead  

### Ubuntu 16.04 (64bit)
1. Use **apt-get** to install software dependencies
> sudo apt-get install openjdk-8-jdk
> sudo apt-get install imagemagick
> sudo apt-get install ffmpeg
> sudo apt-get install libjpeg-progs
> sudo apt-get install dcraw
> sudo apt-get install libimage-exiftool-perl
> sudo apt-get install jhead

1. Verify the dependencies are installed correctly
> which java  
> which convert  
> which ffmpeg  
> which jpegtran  
> which exiftool  
> which dcraw  
> which jhead  

### Ubuntu 14.04 (64bit)
1. Use **apt-get** to install software dependencies
> sudo apt-get install openjdk-8-jdk
> sudo apt-get install imagemagick
> sudo apt-get install libjpeg-progs
> sudo apt-get install dcraw
> sudo apt-get install libimage-exiftool-perl
> sudo apt-get install jhead
> sudo apt-get install libav-tools  

1. Create a symbolic link from **avconv** to **ffmpeg**
> sudo ln -s /usr/bin/avconv /usr/bin/ffmpeg  

1. Verify the dependencies are installed correctly
> which java  
> which convert  
> which ffmpeg  
> which jpegtran  
> which exiftool  
> which dcraw  
> which jhead  

### CentOS 7 (64bit)

1. Use **yum** to install software dependencies
> sudo yum install java-1.8.0-openjdk  
> sudo yum install ImageMagick  
> sudo yum install libjpeg*  
> sudo yum install dcraw  
> sudo yum install perl-Image-ExifTool  
> sudo yum install jhead  

1. Verify the dependencies are installed correctly
> which java  
> which convert  
> which ffmpeg  
> which jpegtran  
> which exiftool  
> which dcraw  
> which jhead  

1. Install libjpeg.so.8
> wget https://github.com/maciej-c/libjpeg8x64/raw/master/libjpeg8-x64.tar.gz  
> sudo tar xzf libjpeg8-x64.tar.gz -C /usr/lib64  

1. Install FFmpeg (Optional)
Please refer to [How to Install FFmpeg on CentOS](https://www.vultr.com/docs/how-to-install-ffmpeg-on-centos) detail instructions.
    * Update the system
    > sudo yum install epel-release -y  
    > sudo yum update -y  
    > sudo shutdown -r now

    * Install the Nux Dextop YUM repo
    > sudo rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro  
    > sudo rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm  
 
    * Install FFmpeg and FFmpeg development packages
    > sudo yum install ffmpeg ffmpeg-devel -y  

## Optional Plug-in

### <a name="facenet"></a>FaceNet Plug-in


1. Download [FaceNet Plug-in (Linux/OSX)](#facenet): [tf_serving-1.0.0-BETA1.tar.gz](https://drive.google.com/file/d/0B3yQIDinGlTfcFZsU2dTTUdhenM/view?usp=sharing).

1. Unpack **tf_serving-1.0.0-BETA1.tar.gz** to the target directory. For example **/opt/tf_serving**

1. Start **FaceNet** service
> cd /opt/tf_serving
> ./run_facenet.sh  

#### FaceNet Model

This is a pre-trained inception resnet_v1 TensorFlow model based on the face recognizer as described in the paper. This model can be used to generate face embedding for face recognition and clustering.

  [FaceNet: A Unified Embedding for Face Recognition and Clustering](https://arxiv.org/abs/1503.03832)

This model is trained using the [open source TensorFlow implementation](https://github.com/davidsandberg/facenet) of the paper. This model is validated using the LFW dataset and the best result is provided below.

| Report Link                                |    Accuracy    |         Validation Rate        |  AUC   |  EER   |
|--------------------------------------------|----------------|--------------------------------|--------|--------|
| [LFW Validation Report][lfw_report_01]     | 0.9968+-0.0027 | 0.99333+-0.00667 @ FAR=0.00100 | 0.9997 | 0.0039 |

## Using HMC Media Server

### Start HMC Media Server

1. Open a console and change to the **hmc** directory where the **[HMC Media Server]** is installed. For example **/opt/hmc**
> cd /opt/hmc
> ./hmc.sh  

1. Start FaceNet Plug-in (Optional)
> cd tf_serving  
> ./run_facenet.sh  

![labeled_faces_01.jpg](https://github.com/scotthong/hmc-media-server/blob/master/images/labeled_faces_01.jpg)
![imageEditor_with_facechips_01.jpg](https://github.com/scotthong/hmc-media-server/blob/master/images/imageEditor_with_facechips_01.jpg)

### Quick Start Guide
Please refer to the [HMC Media Server Quick Start Guide] page for the guides on previous releases.

Updated guides to be completed...

## License

```
  Copyright 2015-2017 HMC Technologies LLC

  Licensed under the Creative Commons Attribution-ShareAlike 3.0 
  Unported License (the "License"); you may not use this application except
  in compliance with the License. You may obtain a copy of the License at

  http://creativecommons.org/licenses/by-nc-sa/3.0/legalcode  

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
```


[HMC Media Server]: http://homemediacenter.org
[HMC Media Server Quick Start Guide]: http://homemediacenter.org/#/support/quickStart#top