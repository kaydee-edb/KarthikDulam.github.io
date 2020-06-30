---
layout: post
title: "Installing XGBoost GPU for R on windows 10"
date: 2019-10-12
---

For the last couple of days, i have been trying to install the XGBoost GPU for R on my windows 10 device. I faced numerous issues during the installation. Most of the issues i faced were because of the order in which i installed the required software. I had to painfully uninstall them and then install back in the required order. So without further ado, lets delve into the subject matter at hand.
First things first, Here is my device information for comparison:
Alienware m15
RTX 2080
Windows 10
Here are the steps for the installation of required software in the order needed for the process to work.
1. Install Visual Studio 2017 Community Edition. Make sure you install the visual studio first.
https://visualstudio.microsoft.com/vs/older-downloads/
2. Install CUDA from Nvidia: I have installed CUDA 10.0.0 and i was able to compile Xgboost GPU without any issues. You are free to choose any CUDA version after 9.0. However, i would not try taking chances with latest Cuda version :)
https://developer.nvidia.com/cuda-toolkit-archive
3. Install Git for windows OS
https://git-scm.com/download/win
4. Install Cmake for windows
https://cmake.org/download/
5. Install R Studio
https://rstudio.com/products/rstudio/download/
After Succesfully installing R studio, install the below packages
Devtools
6. Install Rtools for windows
https://cran.r-project.org/bin/windows/Rtools/

You need to install Rtools version based on the version of your R installed above.
Once we are done with the installations above, we are ready for actual XGBoost installation. But before we dig in, verify that the below parameters are added to your path variables in the environment variables.
Add/verify that the below environment variables are added to the list of system variables on your device.
Add/Verify R.exe to the path.
Verify if CUDA_PATH_Vx_0 has been added to system variables. (x being the version you chose to install)
Add C:\Rtools\bin to Path
Add C:\Rtools\mingw_64\bin to Path
Add C:\Program Files\CMake\bin to Path
Add/Verify if C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0\bin is added to path
Add/Verify if C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0\lib\x64 is added to path
Add/Verify if C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0\include is added to path
Once all the above required software have been installed and system path updated then follow the below steps for actual installation:
1. Open Git Bash in Administrator mode
Naviagate to the local git folder on your system.
2. Clone the xgboost library and Install the GPU version to the system
>git clone — recursive https://github.com/dmlc/xgboost
cd xgboost
git submodule init
git submodule update
3. Close out of the Git bash and open a windows command prompt in Admin mode. Navigate to the xgboost directory created above and run the below commands
mkdir build
cd build
Run the below command to build the Visual studio solution. Update the parameter after -G to point to your version of visual studio and update the value of the -DLIBR_EXECUTABLE based on the location of the R.exe on your system
cmake .. -G”Visual Studio 15 2017 Win64" -DUSE_CUDA=ON -DLIBR_EXECUTABLE=”C:/Users/kdulam/OneDrive/Documents/R/R-3.6.0/bin/R.exe” -DR_LIB=ON -DGPU_COMPUTE_VER=75
Change the parameter DGPU_compute_ver based on the GPU that your device hosts. My device has RTX2080 which has a computer version of 7.5.
Verify that the job is completed sucessfully. You will see the below msgs on your console
— Configuring done
— Generating done
— Build files have been written to: C:/Users/kdulam/OneDrive/Documents/MachineLearning/xgboost/build
Once the above job is successful, run the below install statement
cmake — build . — target install — config Release
It will take a while for the install job to be completed. If it is successful then it will write the installed Xgboost package to the library folder in the R installation folder. Generally, its added to C:\Program Files\R\R-3.6.0\library
Now that you see the package in the folder successfully, pat yourself on the back for a job well done. Lets try and run a demo program from the xgboost package with GPU acceleration.
you can find the demo file at the location where you cloned the Xgboost from github on your system.
Navigate to C:\your xgboost location\build\R-package\demo\gpu_accelerated.R
If you are unable to find it, don’t stress about it. Here is the github link to the demo file — https://github.com/dmlc/xgboost/blob/master/R-package/demo/gpu_accelerated.R
Run the above file in your R studio and if the job runs sucessfully then congratulations, you have successfully installed the GPU version of XGBoost.

Here are the process times for the job above on my system:
Xgboost with GPU:
> proc.time() — pt
user system elapsed
8.21 1.61 5.69

Xgboost without GPU:
> proc.time() — pt
user system elapsed
42.70 7.34 17.29
Let me know if you had any other errors during installation process. Happy to help. I would like to mention that the installation process in the official xgboost documentation is very clear. The documentation also has install instructions for other operation systems.
