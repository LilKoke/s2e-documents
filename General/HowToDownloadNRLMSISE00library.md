# How to download and make NRLMSISE00 Library

## 1.  Overview

- [NRLMSISE00](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2002JA009430) is an atmosphere model to calculate an air density, considering the solar activity
- [C language version of NRLMSISE00](https://ccmc.gsfc.nasa.gov/pub/modelweb/atmospheric/msis/nrlmsise00/nrlmsis00_c_version/) is mandatory library for S2E. 
- How to use NRLMSISE00 is written in [Specification of Atomosphere model](../Specifications/Environment/Spec_Atmosphere.md)

## 2. How to set up NRLMSISE00 for S2E
  
1. In any environment, run `scripts/Common/download_nrlmsise00_src_and_table.sh`.
  + Source codes of NRLMISE00 and SpaceWeather.txt will be downloaded, and libnrlmsise00.a will be made for Linux and OSX.
    + Users have to compile the codes using same compiler with S2E. You can directly compile them by using makefile in the ExtLibraries\nrlmsise00\src after these codes are donwloaded.
  + If you use Windows, bash terminal for Windows (e.g. Git bash, WSL, MSYS) is needed to run this script.
  + If you use Windows, you need to run an additional script. Proceed to Step 2.

2. If you use Windows, run `scripts/VisualStudio/make_nrlmsise00_VS32bit.bat` after 1.
  + VS command prompt will be launched, then run `scripts/VisualStudio/make_libnrlmsise.bat` in VS command prompt.
  + libnrlmise.lib which is the library for Windows will be made.
  + At the end of the procedure, you may see "指定されたバッチ ラベルが見つかりません - END". If there is `libnrlmsise00.lib` in the right place and all the files are in the right place, you may ignore this message.

3. Check your directories are as follows.
<pre>   
  ├─ExtLibraries  
  │  └─nrlmsise00
  │      ├─table 
  |      |  └─SpaceWeather.txt
  │      ├─lib
  |      |  |─libnrlmsise00.a
  |      |  └─libnrlmsise00.lib
  │      └─src
  |         └─nrlmsise-00.h
  └─s2e_core  
</pre>  

