---
title: Linux安装CUDA时输出的内容
tags:
  - Linux
  - Tensorflow
  - CUDA
categories: Linux
abbrlink: 2248321871
date: 2017-09-05 18:20:00
---

<!-- toc -->
<!-- more -->

# 安装cuda的命令

使用wget下载好deb文件后，
```bash
mark@mashangxue123.com:~$ wget  https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
.....

在命令行中依次输入下面的命令后，等待安装完成

```bash
sudo dpkg -i cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda
```

# Linux安装CUDA时输出的内容
```bash
mark@mashangxue123.com:~$ wget  https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
--2017-09-04 20:07:02--  https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
Resolving developer.download.nvidia.com (developer.download.nvidia.com)... 180.97.172.35, 180.97.172.36, 180.97.172.34, ...
Connecting to developer.download.nvidia.com (developer.download.nvidia.com)|180.97.172.35|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2690 (2.6K) [application/x-deb]
Saving to: ‘cuda-repo-ubuntu1604_8.0.61-1_amd64.deb’

cuda-repo-ubuntu1604_8.0.61-1_amd64.deb            100%[==============================================================================================================>]   2.63

2017-09-04 20:07:05 (418 MB/s) - ‘cuda-repo-ubuntu1604_8.0.61-1_amd64.deb’ saved [2690/2690]

mark@mashangxue123.com:~$ sudo dpkg -i cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
[sudo] password for mark: 
Sorry, try again.
[sudo] password for mark: 
Sorry, try again.
[sudo] password for mark: 
(Reading database ... 466087 files and directories currently installed.)
Preparing to unpack cuda-repo-ubuntu1604_8.0.61-1_amd64.deb ...
Unpacking cuda-repo-ubuntu1604 (8.0.61-1) over (8.0.61-1) ...
Setting up cuda-repo-ubuntu1604 (8.0.61-1) ...

OK




mark@mashangxue123.com:~$ 

mark@mashangxue123.com:~$ sudo apt-get update




Hit:1 http://cn.archive.ubuntu.com/ubuntu xenial InRelease
Get:2 http://cn.archive.ubuntu.com/ubuntu xenial-updates InRelease [102 kB]                                                                                                  
Get:3 http://packages.microsoft.com/repos/vscode stable InRelease [2,802 B]                                                                                                  
Get:4 http://packages.microsoft.com/repos/vscode stable/main amd64 Packages [24.4 kB]                                                                                        
Get:5 http://ppa.launchpad.net/x2go/stable/ubuntu xenial InRelease [17.5 kB]                                                                                                 
Get:6 http://cn.archive.ubuntu.com/ubuntu xenial-backports InRelease [102 kB]                                                                                                
Get:7 http://download.virtualbox.org/virtualbox/debian raring InRelease [7,152 B]                                                                                            
Ign:7 http://download.virtualbox.org/virtualbox/debian raring InRelease                                                                                                      
Get:8 http://cn.archive.ubuntu.com/ubuntu xenial-updates/main amd64 Packages [632 kB]                                                                                        
Get:9 http://ppa.launchpad.net/x2go/stable/ubuntu xenial/main amd64 Packages [15.7 kB]                                                                                     
Get:10 http://security.ubuntu.com/ubuntu xenial-security InRelease [102 kB]                                                                                                  
Get:11 http://download.virtualbox.org/virtualbox/debian raring/contrib amd64 Packages [1,337 B]                                                                        
Get:12 http://download.virtualbox.org/virtualbox/debian raring/contrib i386 Packages [1,322 B]                                                                               
Get:13 http://ppa.launchpad.net/x2go/stable/ubuntu xenial/main i386 Packages [15.7 kB]                                                                                       
Get:14 http://cn.archive.ubuntu.com/ubuntu xenial-updates/main i386 Packages [606 kB]                                                                              
Get:15 http://cn.archive.ubuntu.com/ubuntu xenial-updates/main Translation-en [261 kB]                                                                                       
Get:16 http://security.ubuntu.com/ubuntu xenial-security/main amd64 Packages [353 kB]                                                                                        
Get:17 http://cn.archive.ubuntu.com/ubuntu xenial-updates/main amd64 DEP-11 Metadata [305 kB]                                                                                
Get:18 http://cn.archive.ubuntu.com/ubuntu xenial-updates/main DEP-11 64x64 Icons [205 kB]                                                                                   
Ign:19 https://get.docker.io/ubuntu docker InRelease                                                                                                                         
Get:20 http://cn.archive.ubuntu.com/ubuntu xenial-updates/restricted amd64 Packages [8,048 B]                                                                                
Get:21 http://cn.archive.ubuntu.com/ubuntu xenial-updates/restricted i386 Packages [8,044 B]                                                                                 
Get:22 http://cn.archive.ubuntu.com/ubuntu xenial-updates/restricted Translation-en [2,688 B]                                                                                
Get:23 http://cn.archive.ubuntu.com/ubuntu xenial-updates/universe amd64 Packages [529 kB]                                                                                   
Hit:24 https://get.docker.io/ubuntu docker Release                                                                                                                           
Get:26 http://cn.archive.ubuntu.com/ubuntu xenial-updates/universe i386 Packages [506 kB]                                                                                    
Get:27 http://cn.archive.ubuntu.com/ubuntu xenial-updates/universe Translation-en [209 kB]                                                                                   
Get:28 http://cn.archive.ubuntu.com/ubuntu xenial-updates/universe amd64 DEP-11 Metadata [171 kB]                                                                            
Get:29 http://cn.archive.ubuntu.com/ubuntu xenial-updates/universe DEP-11 64x64 Icons [226 kB]                                                                               
Get:30 http://cn.archive.ubuntu.com/ubuntu xenial-updates/multiverse amd64 Packages [15.5 kB]                                                                                
Get:31 http://cn.archive.ubuntu.com/ubuntu xenial-updates/multiverse i386 Packages [14.6 kB]                                                                                 
Get:32 http://cn.archive.ubuntu.com/ubuntu xenial-updates/multiverse amd64 DEP-11 Metadata [5,892 B]                                                                         
Get:33 http://cn.archive.ubuntu.com/ubuntu xenial-backports/main amd64 Packages [4,884 B]                                                                                    
Get:34 http://cn.archive.ubuntu.com/ubuntu xenial-backports/main i386 Packages [4,880 B]                                                                                     
Get:35 http://cn.archive.ubuntu.com/ubuntu xenial-backports/main amd64 DEP-11 Metadata [3,324 B]                                                                             
Get:36 http://cn.archive.ubuntu.com/ubuntu xenial-backports/universe amd64 DEP-11 Metadata [5,132 B]                                                                         
Get:37 http://cn.archive.ubuntu.com/ubuntu xenial-backports/universe DEP-11 64x64 Icons [2,716 B]                                                                            
Get:38 http://security.ubuntu.com/ubuntu xenial-security/main i386 Packages [330 kB]                                                                                         
Get:39 http://security.ubuntu.com/ubuntu xenial-security/main Translation-en [154 kB]                                                                                        
Get:40 http://security.ubuntu.com/ubuntu xenial-security/main amd64 DEP-11 Metadata [59.9 kB]                                                                                
Get:41 http://security.ubuntu.com/ubuntu xenial-security/main DEP-11 64x64 Icons [52.0 kB]                                                                                   
Get:42 http://security.ubuntu.com/ubuntu xenial-security/universe amd64 Packages [166 kB]                                                                                    
Get:43 http://security.ubuntu.com/ubuntu xenial-security/universe i386 Packages [145 kB]                                                                                     
Get:44 http://security.ubuntu.com/ubuntu xenial-security/universe Translation-en [86.8 kB]                                                                                   
Get:45 http://security.ubuntu.com/ubuntu xenial-security/universe amd64 DEP-11 Metadata [48.8 kB]                                                                            
Get:46 http://security.ubuntu.com/ubuntu xenial-security/universe DEP-11 64x64 Icons [69.1 kB]                                                                               
Get:47 http://security.ubuntu.com/ubuntu xenial-security/multiverse amd64 Packages [2,752 B]                                                                                 
Get:48 http://security.ubuntu.com/ubuntu xenial-security/multiverse i386 Packages [2,908 B]                                                                                  
Ign:49 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  InRelease                                                                                  
Ign:50 http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64  InRelease
Get:51 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  Release [564 B]
Get:52 http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64  Release [564 B]
Get:53 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  Release.gpg [801 B]
Get:54 http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64  Release.gpg [801 B]
Get:55 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  Packages [66.0 kB]
Get:56 http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64  Packages [8,408 B]                                                             
Fetched 5,666 kB in 1min 15s (75.5 kB/s)                                                                                                                                     
Reading package lists... Done
W: GPG error: http://download.virtualbox.org/virtualbox/debian raring InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 54422A4B98AB5139
W: The repository 'http://download.virtualbox.org/virtualbox/debian raring InRelease' is not signed.
N: Data from such a repository can't be authenticated and is therefore potentially dangerous to use.
N: See apt-secure(8) manpage for repository creation and user configuration details.
W: https://get.docker.io/ubuntu/dists/docker/Release.gpg: Signature by key 36A1D7869245C8950F966E92D8576A8BA88D21E9 uses weak digest algorithm (SHA1)
mark@mashangxue123.com:~$ sudo apt-get install cuda
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  linux-headers-4.10.0-27 linux-headers-4.10.0-27-generic linux-headers-4.8.0-36 linux-headers-4.8.0-36-generic linux-headers-4.8.0-51 linux-headers-4.8.0-51-generic
  linux-headers-4.8.0-56 linux-headers-4.8.0-56-generic linux-headers-4.8.0-58 linux-headers-4.8.0-58-generic linux-image-4.10.0-27-generic linux-image-4.8.0-36-generic
  linux-image-4.8.0-51-generic linux-image-4.8.0-56-generic linux-image-4.8.0-58-generic linux-image-extra-4.10.0-27-generic linux-image-extra-4.8.0-36-generic
  linux-image-extra-4.8.0-51-generic linux-image-extra-4.8.0-56-generic linux-image-extra-4.8.0-58-generic linux-signed-image-4.10.0-27-generic
  linux-signed-image-4.8.0-51-generic linux-signed-image-4.8.0-56-generic linux-signed-image-4.8.0-58-generic
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  bbswitch-dkms ca-certificates-java cuda-8-0 cuda-command-line-tools-8-0 cuda-core-8-0 cuda-cublas-8-0 cuda-cublas-dev-8-0 cuda-cudart-dev-8-0 cuda-cufft-8-0
  cuda-cufft-dev-8-0 cuda-curand-dev-8-0 cuda-cusolver-8-0 cuda-cusolver-dev-8-0 cuda-cusparse-dev-8-0 cuda-demo-suite-8-0 cuda-documentation-8-0 cuda-driver-dev-8-0
  cuda-drivers cuda-misc-headers-8-0 cuda-npp-8-0 cuda-npp-dev-8-0 cuda-nvgraph-8-0 cuda-nvgraph-dev-8-0 cuda-nvml-dev-8-0 cuda-nvrtc-8-0 cuda-nvrtc-dev-8-0
  cuda-runtime-8-0 cuda-samples-8-0 cuda-toolkit-8-0 cuda-visual-tools-8-0 default-jre default-jre-headless fonts-dejavu-extra java-common lib32gcc1 libc6-i386 libcuda1-384
  libgif7 libjansson4 libxnvctrl0 nvidia-384 nvidia-384-dev nvidia-modprobe nvidia-opencl-icd-384 nvidia-prime nvidia-settings openjdk-8-jre openjdk-8-jre-headless
  screen-resolution-extra xserver-xorg-legacy
Suggested packages:
  bumblebee default-java-plugin icedtea-8-plugin openjdk-8-jre-jamvm fonts-ipafont-gothic fonts-ipafont-mincho fonts-wqy-microhei fonts-wqy-zenhei fonts-indic
The following NEW packages will be installed:
  bbswitch-dkms ca-certificates-java cuda cuda-8-0 cuda-command-line-tools-8-0 cuda-core-8-0 cuda-cublas-dev-8-0 cuda-cudart-dev-8-0 cuda-cufft-8-0 cuda-cufft-dev-8-0
  cuda-curand-dev-8-0 cuda-cusolver-8-0 cuda-cusolver-dev-8-0 cuda-cusparse-dev-8-0 cuda-demo-suite-8-0 cuda-documentation-8-0 cuda-driver-dev-8-0 cuda-drivers
  cuda-misc-headers-8-0 cuda-npp-8-0 cuda-npp-dev-8-0 cuda-nvgraph-8-0 cuda-nvgraph-dev-8-0 cuda-nvml-dev-8-0 cuda-nvrtc-8-0 cuda-nvrtc-dev-8-0 cuda-runtime-8-0
  cuda-samples-8-0 cuda-toolkit-8-0 cuda-visual-tools-8-0 default-jre default-jre-headless fonts-dejavu-extra java-common lib32gcc1 libc6-i386 libcuda1-384 libgif7
  libjansson4 libxnvctrl0 nvidia-384 nvidia-384-dev nvidia-modprobe nvidia-opencl-icd-384 nvidia-prime nvidia-settings openjdk-8-jre openjdk-8-jre-headless
  screen-resolution-extra xserver-xorg-legacy
The following packages will be upgraded:
  cuda-cublas-8-0
1 upgraded, 50 newly installed, 0 to remove and 228 not upgraded.
Need to get 1,391 MB of archives.
After this operation, 2,427 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://cn.archive.ubuntu.com/ubuntu xenial/main amd64 java-common all 0.56ubuntu2 [7,742 B]
Get:2 http://cn.archive.ubuntu.com/ubuntu xenial/main amd64 default-jre-headless amd64 2:1.8-56ubuntu2 [4,380 B]
Get:3 http://cn.archive.ubuntu.com/ubuntu xenial/main amd64 ca-certificates-java all 20160321 [12.9 kB]
Get:4 http://cn.archive.ubuntu.com/ubuntu xenial-updates/main amd64 openjdk-8-jre-headless amd64 8u131-b11-2ubuntu1.16.04.3 [27.0 MB]
Get:5 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-misc-headers-8-0 8.0.61-1 [1,077 kB]                                                   
Get:6 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-core-8-0 8.0.61-1 [20.0 MB]                                                            
Get:7 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-driver-dev-8-0 8.0.61-1 [14.1 kB]                                                      
Get:8 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-cudart-dev-8-0 8.0.61-1 [1,071 kB]                                                     
Get:9 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-command-line-tools-8-0 8.0.61-1 [26.1 MB]                                              
Get:10 http://cn.archive.ubuntu.com/ubuntu xenial-updates/main amd64 libgif7 amd64 5.1.4-0.3~16.04 [30.5 kB]                                                                 
Get:11 http://cn.archive.ubuntu.com/ubuntu xenial-updates/main amd64 openjdk-8-jre amd64 8u131-b11-2ubuntu1.16.04.3 [69.5 kB]                                                
Get:12 http://cn.archive.ubuntu.com/ubuntu xenial/main amd64 default-jre amd64 2:1.8-56ubuntu2 [980 B]                                                                       
Get:13 http://cn.archive.ubuntu.com/ubuntu xenial-updates/main amd64 libc6-i386 amd64 2.23-0ubuntu9 [2,333 kB]                                                               
Get:14 http://cn.archive.ubuntu.com/ubuntu xenial/main amd64 lib32gcc1 amd64 1:6.0.1-0ubuntu1 [46.6 kB]                                                                      
Get:15 http://cn.archive.ubuntu.com/ubuntu xenial-updates/main amd64 xserver-xorg-legacy amd64 2:1.18.4-0ubuntu0.3 [36.0 kB]                                                 
Get:16 http://cn.archive.ubuntu.com/ubuntu xenial/main amd64 screen-resolution-extra all 0.17.1 [11.4 kB]                                                                    
Get:17 http://cn.archive.ubuntu.com/ubuntu xenial/main amd64 libjansson4 amd64 2.7-3 [26.9 kB]                                                                               
Get:18 http://cn.archive.ubuntu.com/ubuntu xenial/main amd64 fonts-dejavu-extra all 2.35-1 [1,749 kB]                                                                        
Get:19 http://cn.archive.ubuntu.com/ubuntu xenial/main amd64 bbswitch-dkms amd64 0.8-3ubuntu1 [11.6 kB]                                                                      
Get:20 http://cn.archive.ubuntu.com/ubuntu xenial/main amd64 nvidia-prime amd64 0.8.2 [11.1 kB]                                                                              
Get:21 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-nvrtc-8-0 8.0.61-1 [9,585 kB]                                                         
Get:22 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-nvrtc-dev-8-0 8.0.61-1 [10.8 kB]                                                      
Get:23 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-cusolver-8-0 8.0.61-1 [29.3 MB]                                                       
Get:24 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-cusolver-dev-8-0 8.0.61-1 [6,816 kB]                                                  
Get:25 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-cublas-8-0 8.0.61.2-1 [58.1 MB]                                                       
Get:26 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-cublas-dev-8-0 8.0.61.2-1 [66.6 MB]                                                   
Get:27 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-cufft-8-0 8.0.61-1 [117 MB]                                                           
Get:28 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-cufft-dev-8-0 8.0.61-1 [94.8 MB]                                                      
Get:29 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-curand-dev-8-0 8.0.61-1 [67.7 MB]                                                     
Get:30 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-cusparse-dev-8-0 8.0.61-1 [29.6 MB]                                                   
Get:31 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-npp-8-0 8.0.61-1 [157 MB]                                                             
Get:32 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-npp-dev-8-0 8.0.61-1 [82.3 MB]                                                        
Get:33 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-samples-8-0 8.0.61-1 [101 MB]                                                         
Get:34 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-documentation-8-0 8.0.61-1 [113 MB]                                                   
Get:35 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-nvml-dev-8-0 8.0.61-1 [48.4 kB]                                                       
Get:36 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-nvgraph-8-0 8.0.61-1 [2,948 kB]                                                       
Get:37 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-nvgraph-dev-8-0 8.0.61-1 [3,028 kB]                                                   
Get:38 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-visual-tools-8-0 8.0.61-1 [286 MB]                                                    
Get:39 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-toolkit-8-0 8.0.61-1 [2,892 B]                                                        
Get:40 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  nvidia-384 384.66-0ubuntu1 [72.9 MB]                                                       
Get:41 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  nvidia-384-dev 384.66-0ubuntu1 [82.4 kB]                                                   
Get:42 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  libcuda1-384 384.66-0ubuntu1 [3,666 kB]                                                    
Get:43 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  nvidia-modprobe 384.66-0ubuntu1 [17.1 kB]                                                  
Get:44 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  libxnvctrl0 384.66-0ubuntu1 [19.1 kB]                                                      
Get:45 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  nvidia-settings 384.66-0ubuntu1 [889 kB]                                                   
Get:46 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  nvidia-opencl-icd-384 384.66-0ubuntu1 [3,355 kB]                                           
Get:47 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-drivers 384.66-1 [2,402 B]                                                            
Get:48 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-runtime-8-0 8.0.61-1 [2,574 B]                                                        
Get:49 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-demo-suite-8-0 8.0.61-1 [4,988 kB]                                                    
Get:50 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda-8-0 8.0.61-1 [2,556 B]                                                                
Get:51 http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64  cuda 8.0.61-1 [2,510 B]                                                                    
Fetched 1,391 MB in 2h 3min 1s (188 kB/s)                                                                                                                                    
Extracting templates from packages: 100%
Preconfiguring packages ...
Selecting previously unselected package java-common.
(Reading database ... 466087 files and directories currently installed.)
Preparing to unpack .../java-common_0.56ubuntu2_all.deb ...
Unpacking java-common (0.56ubuntu2) ...
Selecting previously unselected package default-jre-headless.
Preparing to unpack .../default-jre-headless_2%3a1.8-56ubuntu2_amd64.deb ...
Unpacking default-jre-headless (2:1.8-56ubuntu2) ...
Selecting previously unselected package ca-certificates-java.
Preparing to unpack .../ca-certificates-java_20160321_all.deb ...
Unpacking ca-certificates-java (20160321) ...
Selecting previously unselected package openjdk-8-jre-headless:amd64.
Preparing to unpack .../openjdk-8-jre-headless_8u131-b11-2ubuntu1.16.04.3_amd64.deb ...
Unpacking openjdk-8-jre-headless:amd64 (8u131-b11-2ubuntu1.16.04.3) ...
Selecting previously unselected package cuda-misc-headers-8-0.
Preparing to unpack .../cuda-misc-headers-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-misc-headers-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-core-8-0.
Preparing to unpack .../cuda-core-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-core-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-driver-dev-8-0.
Preparing to unpack .../cuda-driver-dev-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-driver-dev-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-cudart-dev-8-0.
Preparing to unpack .../cuda-cudart-dev-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-cudart-dev-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-command-line-tools-8-0.
Preparing to unpack .../cuda-command-line-tools-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-command-line-tools-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-nvrtc-8-0.
Preparing to unpack .../cuda-nvrtc-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-nvrtc-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-nvrtc-dev-8-0.
Preparing to unpack .../cuda-nvrtc-dev-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-nvrtc-dev-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-cusolver-8-0.
Preparing to unpack .../cuda-cusolver-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-cusolver-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-cusolver-dev-8-0.
Preparing to unpack .../cuda-cusolver-dev-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-cusolver-dev-8-0 (8.0.61-1) ...
Preparing to unpack .../cuda-cublas-8-0_8.0.61.2-1_amd64.deb ...
Unpacking cuda-cublas-8-0 (8.0.61.2-1) over (8.0.61.1-1) ...
Selecting previously unselected package cuda-cublas-dev-8-0.
Preparing to unpack .../cuda-cublas-dev-8-0_8.0.61.2-1_amd64.deb ...
Unpacking cuda-cublas-dev-8-0 (8.0.61.2-1) ...
Selecting previously unselected package cuda-cufft-8-0.
Preparing to unpack .../cuda-cufft-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-cufft-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-cufft-dev-8-0.
Preparing to unpack .../cuda-cufft-dev-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-cufft-dev-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-curand-dev-8-0.
Preparing to unpack .../cuda-curand-dev-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-curand-dev-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-cusparse-dev-8-0.
Preparing to unpack .../cuda-cusparse-dev-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-cusparse-dev-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-npp-8-0.
Preparing to unpack .../cuda-npp-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-npp-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-npp-dev-8-0.
Preparing to unpack .../cuda-npp-dev-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-npp-dev-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-samples-8-0.
Preparing to unpack .../cuda-samples-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-samples-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-documentation-8-0.
Preparing to unpack .../cuda-documentation-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-documentation-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-nvml-dev-8-0.
Preparing to unpack .../cuda-nvml-dev-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-nvml-dev-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-nvgraph-8-0.
Preparing to unpack .../cuda-nvgraph-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-nvgraph-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-nvgraph-dev-8-0.
Preparing to unpack .../cuda-nvgraph-dev-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-nvgraph-dev-8-0 (8.0.61-1) ...
Selecting previously unselected package libgif7:amd64.
Preparing to unpack .../libgif7_5.1.4-0.3~16.04_amd64.deb ...
Unpacking libgif7:amd64 (5.1.4-0.3~16.04) ...
Selecting previously unselected package openjdk-8-jre:amd64.
Preparing to unpack .../openjdk-8-jre_8u131-b11-2ubuntu1.16.04.3_amd64.deb ...
Unpacking openjdk-8-jre:amd64 (8u131-b11-2ubuntu1.16.04.3) ...
Selecting previously unselected package default-jre.
Preparing to unpack .../default-jre_2%3a1.8-56ubuntu2_amd64.deb ...
Unpacking default-jre (2:1.8-56ubuntu2) ...
Selecting previously unselected package cuda-visual-tools-8-0.
Preparing to unpack .../cuda-visual-tools-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-visual-tools-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-toolkit-8-0.
Preparing to unpack .../cuda-toolkit-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-toolkit-8-0 (8.0.61-1) ...
Selecting previously unselected package libc6-i386.
Preparing to unpack .../libc6-i386_2.23-0ubuntu9_amd64.deb ...
Unpacking libc6-i386 (2.23-0ubuntu9) ...
Selecting previously unselected package lib32gcc1.
Preparing to unpack .../lib32gcc1_1%3a6.0.1-0ubuntu1_amd64.deb ...
Unpacking lib32gcc1 (1:6.0.1-0ubuntu1) ...
Selecting previously unselected package xserver-xorg-legacy.
Preparing to unpack .../xserver-xorg-legacy_2%3a1.18.4-0ubuntu0.3_amd64.deb ...
Unpacking xserver-xorg-legacy (2:1.18.4-0ubuntu0.3) ...
Selecting previously unselected package nvidia-384.
Preparing to unpack .../nvidia-384_384.66-0ubuntu1_amd64.deb ...
Unpacking nvidia-384 (384.66-0ubuntu1) ...
Selecting previously unselected package nvidia-384-dev.
Preparing to unpack .../nvidia-384-dev_384.66-0ubuntu1_amd64.deb ...
Unpacking nvidia-384-dev (384.66-0ubuntu1) ...
Selecting previously unselected package libcuda1-384.
Preparing to unpack .../libcuda1-384_384.66-0ubuntu1_amd64.deb ...
Unpacking libcuda1-384 (384.66-0ubuntu1) ...
Selecting previously unselected package nvidia-modprobe.
Preparing to unpack .../nvidia-modprobe_384.66-0ubuntu1_amd64.deb ...
Unpacking nvidia-modprobe (384.66-0ubuntu1) ...
Selecting previously unselected package screen-resolution-extra.
Preparing to unpack .../screen-resolution-extra_0.17.1_all.deb ...
Unpacking screen-resolution-extra (0.17.1) ...
Selecting previously unselected package libjansson4:amd64.
Preparing to unpack .../libjansson4_2.7-3_amd64.deb ...
Unpacking libjansson4:amd64 (2.7-3) ...
Selecting previously unselected package libxnvctrl0.
Preparing to unpack .../libxnvctrl0_384.66-0ubuntu1_amd64.deb ...
Unpacking libxnvctrl0 (384.66-0ubuntu1) ...
Selecting previously unselected package nvidia-settings.
Preparing to unpack .../nvidia-settings_384.66-0ubuntu1_amd64.deb ...
Unpacking nvidia-settings (384.66-0ubuntu1) ...
Selecting previously unselected package nvidia-opencl-icd-384.
Preparing to unpack .../nvidia-opencl-icd-384_384.66-0ubuntu1_amd64.deb ...
Unpacking nvidia-opencl-icd-384 (384.66-0ubuntu1) ...
Selecting previously unselected package cuda-drivers.
Preparing to unpack .../cuda-drivers_384.66-1_amd64.deb ...
Unpacking cuda-drivers (384.66-1) ...
Selecting previously unselected package cuda-runtime-8-0.
Preparing to unpack .../cuda-runtime-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-runtime-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-demo-suite-8-0.
Preparing to unpack .../cuda-demo-suite-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-demo-suite-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda-8-0.
Preparing to unpack .../cuda-8-0_8.0.61-1_amd64.deb ...
Unpacking cuda-8-0 (8.0.61-1) ...
Selecting previously unselected package cuda.
Preparing to unpack .../cuda_8.0.61-1_amd64.deb ...
Unpacking cuda (8.0.61-1) ...
Selecting previously unselected package fonts-dejavu-extra.
Preparing to unpack .../fonts-dejavu-extra_2.35-1_all.deb ...
Unpacking fonts-dejavu-extra (2.35-1) ...
Selecting previously unselected package bbswitch-dkms.
Preparing to unpack .../bbswitch-dkms_0.8-3ubuntu1_amd64.deb ...
Unpacking bbswitch-dkms (0.8-3ubuntu1) ...
Selecting previously unselected package nvidia-prime.
Preparing to unpack .../nvidia-prime_0.8.2_amd64.deb ...
Unpacking nvidia-prime (0.8.2) ...
Processing triggers for man-db (2.7.5-1) ...
Processing triggers for ca-certificates (20160104ubuntu1) ...
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...
done.
Processing triggers for libc-bin (2.23-0ubuntu9) ...
Processing triggers for gnome-menus (3.13.3-6ubuntu3.1) ...
Processing triggers for desktop-file-utils (0.22-1ubuntu5) ...
Processing triggers for bamfdaemon (0.5.3~bzr0+16.04.20160824-0ubuntu1) ...
Rebuilding /usr/share/applications/bamf-2.index...
Processing triggers for mime-support (3.59ubuntu1) ...
Processing triggers for hicolor-icon-theme (0.15-0ubuntu1) ...
Processing triggers for ureadahead (0.100.0-19) ...
Processing triggers for dbus (1.10.6-1ubuntu3.3) ...
Processing triggers for fontconfig (2.11.94-0ubuntu1.1) ...
Setting up java-common (0.56ubuntu2) ...
Setting up cuda-misc-headers-8-0 (8.0.61-1) ...
Setting up cuda-core-8-0 (8.0.61-1) ...
Setting up cuda-driver-dev-8-0 (8.0.61-1) ...
Setting up cuda-cudart-dev-8-0 (8.0.61-1) ...
Setting up cuda-command-line-tools-8-0 (8.0.61-1) ...
Setting up cuda-nvrtc-8-0 (8.0.61-1) ...
Setting up cuda-nvrtc-dev-8-0 (8.0.61-1) ...
Setting up cuda-cusolver-8-0 (8.0.61-1) ...
Setting up cuda-cusolver-dev-8-0 (8.0.61-1) ...
Setting up cuda-cublas-8-0 (8.0.61.2-1) ...
Setting up cuda-cublas-dev-8-0 (8.0.61.2-1) ...
Setting up cuda-cufft-8-0 (8.0.61-1) ...
Setting up cuda-cufft-dev-8-0 (8.0.61-1) ...
Setting up cuda-curand-dev-8-0 (8.0.61-1) ...
Setting up cuda-cusparse-dev-8-0 (8.0.61-1) ...
Setting up cuda-npp-8-0 (8.0.61-1) ...
Setting up cuda-npp-dev-8-0 (8.0.61-1) ...
Setting up cuda-samples-8-0 (8.0.61-1) ...
Setting up cuda-documentation-8-0 (8.0.61-1) ...
Setting up cuda-nvml-dev-8-0 (8.0.61-1) ...
Setting up cuda-nvgraph-8-0 (8.0.61-1) ...
Setting up cuda-nvgraph-dev-8-0 (8.0.61-1) ...
Setting up libgif7:amd64 (5.1.4-0.3~16.04) ...
Setting up libc6-i386 (2.23-0ubuntu9) ...
Setting up lib32gcc1 (1:6.0.1-0ubuntu1) ...
Setting up xserver-xorg-legacy (2:1.18.4-0ubuntu0.3) ...
Setting up nvidia-384 (384.66-0ubuntu1) ...
update-alternatives: using /usr/lib/nvidia-384/ld.so.conf to provide /etc/ld.so.conf.d/x86_64-linux-gnu_GL.conf (x86_64-linux-gnu_gl_conf) in auto mode
update-alternatives: warning: skip creation of /usr/share/grub-gfxpayload-lists/blacklist/10_proprietary-graphics-drivers because associated file /usr/share/nvidia-384/nvidia-384.grub-gfxpayload (of link group x86_64-linux-gnu_gl_conf) doesn't exist
update-alternatives: using /usr/lib/nvidia-384/ld.so.conf to provide /etc/ld.so.conf.d/x86_64-linux-gnu_EGL.conf (x86_64-linux-gnu_egl_conf) in auto mode
update-alternatives: using /usr/lib/nvidia-384/alt_ld.so.conf to provide /etc/ld.so.conf.d/i386-linux-gnu_GL.conf (i386-linux-gnu_gl_conf) in auto mode
update-alternatives: using /usr/lib/nvidia-384/alt_ld.so.conf to provide /etc/ld.so.conf.d/i386-linux-gnu_EGL.conf (i386-linux-gnu_egl_conf) in auto mode
update-alternatives: using /usr/share/nvidia-384/glamor.conf to provide /usr/share/X11/xorg.conf.d/glamoregl.conf (glamor_conf) in auto mode
update-initramfs: deferring update (trigger activated)

A modprobe blacklist file has been created at /etc/modprobe.d to prevent Nouveau from loading. This can be reverted by deleting /etc/modprobe.d/nvidia-graphics-drivers.conf.
A new initrd image has also been created. To revert, please replace /boot/initrd-4.10.0-30-generic with /boot/initrd-$(uname -r)-backup.

*****************************************************************************
*** Reboot your computer and verify that the NVIDIA graphics driver can   ***
*** be loaded.                                                            ***
*****************************************************************************

INFO:Enable nvidia-384
DEBUG:Parsing /usr/share/ubuntu-drivers-common/quirks/dell_latitude
DEBUG:Parsing /usr/share/ubuntu-drivers-common/quirks/lenovo_thinkpad
DEBUG:Parsing /usr/share/ubuntu-drivers-common/quirks/put_your_quirks_here
Adding system user `nvidia-persistenced' (UID 123) ...
Adding new group `nvidia-persistenced' (GID 132) ...
Adding new user `nvidia-persistenced' (UID 123) with group `nvidia-persistenced' ...
Not creating home directory `/'.
Loading new nvidia-384-384.66 DKMS files...
First Installation: checking all kernels...
Building only for 4.10.0-30-generic
Building for architecture x86_64
Building initial module for 4.10.0-30-generic
Done.

nvidia_384:
Running module version sanity check.
 - Original module
   - No original module exists within this kernel
 - Installation
   - Installing to /lib/modules/4.10.0-30-generic/updates/dkms/

nvidia_384_modeset.ko:
Running module version sanity check.
 - Original module
   - No original module exists within this kernel
 - Installation
   - Installing to /lib/modules/4.10.0-30-generic/updates/dkms/

nvidia_384_drm.ko:
Running module version sanity check.
 - Original module
   - No original module exists within this kernel
 - Installation
   - Installing to /lib/modules/4.10.0-30-generic/updates/dkms/

nvidia_384_uvm.ko:
Running module version sanity check.
 - Original module
   - No original module exists within this kernel
 - Installation
   - Installing to /lib/modules/4.10.0-30-generic/updates/dkms/

depmod....

DKMS: install completed.
Setting up nvidia-384-dev (384.66-0ubuntu1) ...
Setting up libcuda1-384 (384.66-0ubuntu1) ...
Setting up nvidia-modprobe (384.66-0ubuntu1) ...
Setting up screen-resolution-extra (0.17.1) ...
Setting up libjansson4:amd64 (2.7-3) ...
Setting up libxnvctrl0 (384.66-0ubuntu1) ...
Setting up nvidia-settings (384.66-0ubuntu1) ...
Setting up nvidia-opencl-icd-384 (384.66-0ubuntu1) ...
Setting up cuda-drivers (384.66-1) ...
Setting up cuda-runtime-8-0 (8.0.61-1) ...
Setting up cuda-demo-suite-8-0 (8.0.61-1) ...
Setting up fonts-dejavu-extra (2.35-1) ...
Setting up bbswitch-dkms (0.8-3ubuntu1) ...
Loading new bbswitch-0.8 DKMS files...
First Installation: checking all kernels...
Building only for 4.10.0-30-generic
Building initial module for 4.10.0-30-generic
Done.

bbswitch:
Running module version sanity check.
 - Original module
   - No original module exists within this kernel
 - Installation
   - Installing to /lib/modules/4.10.0-30-generic/updates/dkms/

depmod....

DKMS: install completed.
Setting up nvidia-prime (0.8.2) ...
Setting up ca-certificates-java (20160321) ...
Adding debian:VeriSign_Universal_Root_Certification_Authority.pem
Adding debian:DigiCert_Assured_ID_Root_CA.pem
Adding debian:Staat_der_Nederlanden_Root_CA.pem
Adding debian:Sonera_Class_1_Root_CA.pem
Adding debian:CFCA_EV_ROOT.pem
Adding debian:TÜRKTRUST_Elektronik_Sertifika_Hizmet_Sağlayıcısı_H6.pem
Adding debian:DST_ACES_CA_X6.pem
Adding debian:Verisign_Class_3_Public_Primary_Certification_Authority_-_G3.pem
Adding debian:NetLock_Business_=Class_B=_Root.pem
Adding debian:CA_Disig.pem
Adding debian:EC-ACC.pem
Adding debian:Comodo_AAA_Services_root.pem
Adding debian:DigiCert_High_Assurance_EV_Root_CA.pem
Adding debian:WellsSecure_Public_Root_Certificate_Authority.pem
Adding debian:Security_Communication_RootCA2.pem
Adding debian:thawte_Primary_Root_CA_-_G3.pem
Adding debian:Go_Daddy_Class_2_CA.pem
Adding debian:Comodo_Trusted_Services_root.pem
Adding debian:E-Tugra_Certification_Authority.pem
Adding debian:Chambers_of_Commerce_Root_-_2008.pem
Adding debian:Certigna.pem
Adding debian:T-TeleSec_GlobalRoot_Class_3.pem
Adding debian:StartCom_Certification_Authority.pem
Adding debian:Verisign_Class_1_Public_Primary_Certification_Authority_-_G3.pem
Adding debian:Deutsche_Telekom_Root_CA_2.pem
Adding debian:Entrust_Root_Certification_Authority.pem
Adding debian:Swisscom_Root_EV_CA_2.pem
Adding debian:Atos_TrustedRoot_2011.pem
Adding debian:Microsec_e-Szigno_Root_CA_2009.pem
Adding debian:VeriSign_Class_3_Public_Primary_Certification_Authority_-_G5.pem
Adding debian:CNNIC_ROOT.pem
Adding debian:Equifax_Secure_eBusiness_CA_1.pem
Adding debian:IdenTrust_Public_Sector_Root_CA_1.pem
Adding debian:Buypass_Class_2_Root_CA.pem
Adding debian:thawte_Primary_Root_CA_-_G2.pem
Adding debian:USERTrust_ECC_Certification_Authority.pem
Adding debian:AffirmTrust_Premium_ECC.pem
Adding debian:Certplus_Class_2_Primary_CA.pem
Adding debian:IGC_A.pem
Adding debian:Comodo_Secure_Services_root.pem
Adding debian:AddTrust_External_Root.pem
Adding debian:ApplicationCA_-_Japanese_Government.pem
Adding debian:TÜBİTAK_UEKAE_Kök_Sertifika_Hizmet_Sağlayıcısı_-_Sürüm_3.pem
Adding debian:TÜRKTRUST_Elektronik_Sertifika_Hizmet_Sağlayıcısı_H5.pem
Adding debian:Entrust_Root_Certification_Authority_-_G2.pem
Adding debian:SwissSign_Silver_CA_-_G2.pem
Adding debian:Cybertrust_Global_Root.pem
Adding debian:Microsec_e-Szigno_Root_CA.pem
Adding debian:USERTrust_RSA_Certification_Authority.pem
Adding debian:Staat_der_Nederlanden_EV_Root_CA.pem
Adding debian:Starfield_Root_Certificate_Authority_-_G2.pem
Adding debian:QuoVadis_Root_CA_3_G3.pem
Adding debian:GlobalSign_Root_CA_-_R2.pem
Adding debian:Network_Solutions_Certificate_Authority.pem
Adding debian:NetLock_Express_=Class_C=_Root.pem
Adding debian:AddTrust_Qualified_Certificates_Root.pem
Adding debian:GeoTrust_Primary_Certification_Authority.pem
Adding debian:Verisign_Class_3_Public_Primary_Certification_Authority_2.pem
Adding debian:TC_TrustCenter_Class_3_CA_II.pem
Adding debian:Taiwan_GRCA.pem
Adding debian:Staat_der_Nederlanden_Root_CA_-_G2.pem
Adding debian:Actalis_Authentication_Root_CA.pem
Adding debian:Trustis_FPS_Root_CA.pem
Adding debian:NetLock_Qualified_=Class_QA=_Root.pem
Adding debian:COMODO_ECC_Certification_Authority.pem
Adding debian:SecureSign_RootCA11.pem
Adding debian:Security_Communication_Root_CA.pem
Adding debian:Verisign_Class_2_Public_Primary_Certification_Authority_-_G3.pem
Adding debian:Entrust_Root_Certification_Authority_-_EC1.pem
Adding debian:ssl-cert-snakeoil.pem
Adding debian:TWCA_Root_Certification_Authority.pem
Adding debian:AffirmTrust_Networking.pem
Adding debian:Swisscom_Root_CA_1.pem
Adding debian:DigiCert_Assured_ID_Root_G3.pem
Adding debian:ACCVRAIZ1.pem
Adding debian:GeoTrust_Universal_CA.pem
Adding debian:GeoTrust_Global_CA_2.pem
Adding debian:ComSign_CA.pem
Adding debian:Camerfirma_Chambers_of_Commerce_Root.pem
Adding debian:Juur-SK.pem
Adding debian:Camerfirma_Global_Chambersign_Root.pem
Adding debian:SecureTrust_CA.pem
Adding debian:EBG_Elektronik_Sertifika_Hizmet_Sağlayıcısı.pem
Adding debian:DigiCert_Assured_ID_Root_G2.pem
Adding debian:SwissSign_Platinum_CA_-_G2.pem
Adding debian:RSA_Security_2048_v3.pem
Adding debian:GeoTrust_Primary_Certification_Authority_-_G2.pem
Adding debian:Sonera_Class_2_Root_CA.pem
Adding debian:GlobalSign_ECC_Root_CA_-_R4.pem
Adding debian:COMODO_RSA_Certification_Authority.pem
Adding debian:WoSign.pem
Adding debian:DST_Root_CA_X3.pem
Adding debian:Equifax_Secure_CA.pem
Adding debian:EE_Certification_Centre_Root_CA.pem
Adding debian:StartCom_Certification_Authority_G2.pem
Adding debian:Buypass_Class_2_CA_1.pem
Adding debian:Starfield_Services_Root_Certificate_Authority_-_G2.pem
Adding debian:CA_Disig_Root_R2.pem
Adding debian:Global_Chambersign_Root_-_2008.pem
Adding debian:Entrust.net_Premium_2048_Secure_Server_CA.pem
Adding debian:WoSign_China.pem
Adding debian:QuoVadis_Root_CA_3.pem
Adding debian:Certinomis_-_Root_CA.pem
Adding debian:Secure_Global_CA.pem
Adding debian:NetLock_Arany_=Class_Gold=_Főtanúsítvány.pem
Adding debian:Hellenic_Academic_and_Research_Institutions_RootCA_2011.pem
Adding debian:VeriSign_Class_3_Public_Primary_Certification_Authority_-_G4.pem
Adding debian:OISTE_WISeKey_Global_Root_GA_CA.pem
Adding debian:NetLock_Notary_=Class_A=_Root.pem
Adding debian:StartCom_Certification_Authority_2.pem
Adding debian:Root_CA_Generalitat_Valenciana.pem
Adding debian:ePKI_Root_Certification_Authority.pem
Adding debian:D-TRUST_Root_Class_3_CA_2_2009.pem
Adding debian:Staat_der_Nederlanden_Root_CA_-_G3.pem
Adding debian:T-TeleSec_GlobalRoot_Class_2.pem
Adding debian:Hongkong_Post_Root_CA_1.pem
Adding debian:TURKTRUST_Certificate_Services_Provider_Root_2007.pem
Adding debian:GeoTrust_Primary_Certification_Authority_-_G3.pem
Adding debian:Certum_Root_CA.pem
Adding debian:thawte_Primary_Root_CA.pem
Adding debian:DigiCert_Global_Root_G3.pem
Adding debian:Certification_Authority_of_WoSign_G2.pem
Adding debian:Visa_eCommerce_Root.pem
Adding debian:GeoTrust_Universal_CA_2.pem
Adding debian:Verisign_Class_3_Public_Primary_Certification_Authority.pem
Adding debian:Izenpe.com.pem
Adding debian:CA_WoSign_ECC_Root.pem
Adding debian:XRamp_Global_CA_Root.pem
Adding debian:OISTE_WISeKey_Global_Root_GB_CA.pem
Adding debian:QuoVadis_Root_CA_2_G3.pem
Adding debian:DigiCert_Global_Root_CA.pem
Adding debian:UTN_USERFirst_Hardware_Root_CA.pem
Adding debian:Verisign_Class_3_Public_Primary_Certification_Authority_-_G2.pem
Adding debian:Certum_Trusted_Network_CA.pem
Adding debian:COMODO_Certification_Authority.pem
Adding debian:TWCA_Global_Root_CA.pem
Adding debian:AddTrust_Low-Value_Services_Root.pem
Adding debian:QuoVadis_Root_CA.pem
Adding debian:AddTrust_Public_Services_Root.pem
Adding debian:Equifax_Secure_Global_eBusiness_CA.pem
Adding debian:Starfield_Class_2_CA.pem
Adding debian:Go_Daddy_Root_Certificate_Authority_-_G2.pem
Adding debian:Certinomis_-_Autorité_Racine.pem
Adding debian:PSCProcert.pem
Adding debian:S-TRUST_Authentication_and_Encryption_Root_CA_2005_PN.pem
Adding debian:DigiCert_Global_Root_G2.pem
Adding debian:China_Internet_Network_Information_Center_EV_Certificates_Root.pem
Adding debian:ACEDICOM_Root.pem
Adding debian:Verisign_Class_1_Public_Primary_Certification_Authority_-_G2.pem
Adding debian:UTN_USERFirst_Email_Root_CA.pem
Adding debian:Security_Communication_EV_RootCA1.pem
Adding debian:GlobalSign_ECC_Root_CA_-_R5.pem
Adding debian:Verisign_Class_2_Public_Primary_Certification_Authority_-_G2.pem
Adding debian:GeoTrust_Global_CA.pem
Adding debian:Buypass_Class_3_Root_CA.pem
Adding debian:Swisscom_Root_CA_2.pem
Adding debian:SwissSign_Gold_CA_-_G2.pem
Adding debian:D-TRUST_Root_Class_3_CA_2_EV_2009.pem
Adding debian:AC_Raíz_Certicámara_S.A..pem
Adding debian:DigiCert_Trusted_Root_G4.pem
Adding debian:Baltimore_CyberTrust_Root.pem
Adding debian:CA_Disig_Root_R1.pem
Adding debian:Verisign_Class_1_Public_Primary_Certification_Authority.pem
Adding debian:GlobalSign_Root_CA_-_R3.pem
Adding debian:Autoridad_de_Certificacion_Firmaprofesional_CIF_A62634068.pem
Adding debian:AffirmTrust_Commercial.pem
Adding debian:AffirmTrust_Premium.pem
Adding debian:QuoVadis_Root_CA_2.pem
Adding debian:TeliaSonera_Root_CA_v1.pem
Adding debian:certSIGN_ROOT_CA.pem
Adding debian:S-TRUST_Universal_Root_CA.pem
Adding debian:QuoVadis_Root_CA_1_G3.pem
Adding debian:IdenTrust_Commercial_Root_CA_1.pem
Adding debian:GlobalSign_Root_CA.pem
done.
Processing triggers for ca-certificates (20160104ubuntu1) ...
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...

done.
done.
Setting up openjdk-8-jre-headless:amd64 (8u131-b11-2ubuntu1.16.04.3) ...
update-alternatives: using /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/rmid to provide /usr/bin/rmid (rmid) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java to provide /usr/bin/java (java) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/keytool to provide /usr/bin/keytool (keytool) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/jjs to provide /usr/bin/jjs (jjs) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/pack200 to provide /usr/bin/pack200 (pack200) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/rmiregistry to provide /usr/bin/rmiregistry (rmiregistry) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/unpack200 to provide /usr/bin/unpack200 (unpack200) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/orbd to provide /usr/bin/orbd (orbd) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/servertool to provide /usr/bin/servertool (servertool) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/tnameserv to provide /usr/bin/tnameserv (tnameserv) in auto mode
update-alternatives: using /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/jexec to provide /usr/bin/jexec (jexec) in auto mode
Setting up default-jre-headless (2:1.8-56ubuntu2) ...
Setting up openjdk-8-jre:amd64 (8u131-b11-2ubuntu1.16.04.3) ...
update-alternatives: using /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/policytool to provide /usr/bin/policytool (policytool) in auto mode
Setting up default-jre (2:1.8-56ubuntu2) ...
Setting up cuda-visual-tools-8-0 (8.0.61-1) ...
Setting up cuda-toolkit-8-0 (8.0.61-1) ...
Setting up cuda-8-0 (8.0.61-1) ...
Setting up cuda (8.0.61-1) ...
Processing triggers for libc-bin (2.23-0ubuntu9) ...
Processing triggers for initramfs-tools (0.122ubuntu8.8) ...
update-initramfs: Generating /boot/initrd.img-4.10.0-30-generic
W: Possible missing firmware /lib/firmware/ast_dp501_fw.bin for module ast
Processing triggers for shim-signed (1.27~16.04.1+0.9+1474479173.6c180c6-1ubuntu1) ...
Secure Boot not enabled on this system.
Processing triggers for dbus (1.10.6-1ubuntu3.3) ...
Processing triggers for ureadahead (0.100.0-19) ...

mark@mashangxue123.com:~$ 

```