Ubitrack Installation Tutorial
------------------------------


Ubuntu Linux 18.04
++++++++++++++++++


- Install Desktop Version X64

- Install system packages
  $ sudo apt-get update
  $ sudo apt-get upgrade
  $ sudo apt-get install build-essential

  $ sudo apt-get install libv4l-dev qv4l2
  $ sudo apt-get install opencl-headers
  $ sudo apt-get install ocl-icd-opencl-dev
  $ sudo apt-get install libusb-1.0-0-dev


- Install Graphics Drivers (Nvidia Howto: https://linuxconfig.org/how-to-install-the-nvidia-drivers-on-ubuntu-18-04-bionic-beaver-linux)
  $ sudo add-apt-repository ppa:graphics-drivers/ppa
  $ sudo apt update
  $ ubuntu-drivers devices
  $ sudo ubuntu-drivers autoinstall

- Install CUDA
  $ wget https://developer.nvidia.com/compute/cuda/10.0/Prod/local_installers/cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64
  $ mv cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64 cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb

  $ sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb
  $ sudo apt-key add /var/cuda-repo-10-0-local-10.0.130-410.48/7fa2af80.pub
  $ sudo apt-get update
  $ sudo apt-get install cuda

  carefully read the "UEFI" related dialogs and register the MOK in bios if asked
  make sure your installation works (glxinfo / nvidia-settings, cuda examples)
  maybe you need to blacklist some nvidia related modules (https://linuxconfig.org/how-to-disable-nouveau-nvidia-driver-on-ubuntu-18-04-bionic-beaver-linux)

  $ cd /usr/local/cuda/samples/1_Utilities/deviceQuery
  $ sudo make
  $ ./deviceQuery

- ZED Stereo Camera SDK
  $ wget https://download.stereolabs.com/zedsdk/2.7/ubuntu18
  $ mv ubuntu18 ZED_SDK_Ubuntu18_v2.7.1.run
  $ chmod +x ./ZED_SDK_Ubuntu18_v2.7.1.run
  $ ./ZED_SDK_Ubuntu18_v2.7.1.run
  

- Install developer Tools
  $ sudo apt-get install git cmake
  $ sudo apt-get install python3-pip python3-dev

- Install conan package manager
  $ sudo pip3 install --upgrade conan
  $ conan remote add bincrafters "https://api.bintray.com/conan/bincrafters/public-conan"
  $ conan remote add camposs "https://conan.campar.in.tum.de/api/conan/conan-camposs"
  $ conan remote add ubitrack "https://conan.campar.in.tum.de/api/conan/conan-ubitrack"

  change c++ default for stdlib in ~/.conan/profiles/default:
  compiler.libcxx=libstdc++11


- To build an Ubuntu 1.3 release:
  $ sudo pip3 install doit
  $ git clone https://github.com/ubitrack/ubitrack_release_tools.git
  $ cp custom_options_example.yml local_options.yml
  adjust your configuration
  $ doit custom_options=local_options.yml

  maybe needs fix: only python3 executable is installed but python is missing
  should be corrected in python_dev-config package; temporary fix:
  $ sudo ln -s /usr/bin/python3 /usr/local/bin/python


