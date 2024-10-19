# Custom-Pynq-OS-develpment-with-Petalinux
| T | A | S | K | : The project is to run the TVM deploy_classification.py inference on the custom development board: TE0802 Zynq Ultrascale+ developed by Trenz Electronics

TVM works on the Pynq Driver. Since there is no Operating System for the TE0802 board, an Operating System has to be created from scratch with the source files from Trenz Electronics based on a Pynq Linux driver.

Project Instructor : @eamicheal

## Why TE0802 Zynq Ultrascale+ Board ?
<div>
  <img align="left" width="25%" src="https://github.com/arunbasilpaul/Custom-Pynq-OS-develpment-with-Petalinux/assets/171144888/3d4663f8-d005-4819-b758-57084f5d0e54">
</div>

- 1Gb DDR memory for future projects
- Software resource availability
- Cost around 335€
- Capability to run deep-learning models of considerable size
- Availability of multitude of external ports for connecting external peripherals

## Softwares and their versions:
<div>
  <img align="right" width="30%" src="https://github.com/arunbasilpaul/Custom-Pynq-OS-develpment-with-Petalinux/assets/171144888/5f4f845a-527d-4dc0-a92e-9b99d4fd696c">
</div>

- Ubuntu 18.04.5
- Vivado with Vitis 2019.2
- PetaLinux 2019.2 (It is better to have the same version as Vivado)
- TVM
- Python with Anaconda 3.8
- Balena Etcher (To format the SD card and clone the new OS)

## Design Flow:
The steps involved are dependent on the previous step and provide insights or and source files for the next step:

<div>
  <img align="right" width="100%" src="https://github.com/arunbasilpaul/Custom-Pynq-OS-develpment-with-Petalinux/assets/171144888/ff7f2bb6-3422-481e-b4f1-174b4e3b1d1d">
</div>

## Overview of the Pynq Linux:
<div>
  <img align="left" width="30%" src="https://github.com/arunbasilpaul/Custom-Pynq-OS-develpment-with-Petalinux/assets/171144888/e717fd5b-d380-4b36-9723-42907f0b2af7">
</div>

In order to work with TVM (Tensor Virtual Machine), it was necessary to observe and understand the working of an image that was already created.
- TVM already supports selected boards such as Pynq Z1 board but doesn’t have the support for TE0802.
- To better understand how to create our own support for TE0802 board and to understand further steps to create an environment for TVM, Pynq 2.6v image with TVM was run on the Pynq Z1 board
- sshfs was used to enable an Internet connection
- The TVM classification model was successfully run on the Target Pynq Z1board

## Running Bare Metal Application
<div>
  <img align="right" width="30%" src="https://github.com/arunbasilpaul/Custom-Pynq-OS-develpment-with-Petalinux/assets/171144888/f38c587d-8e21-40dd-b20b-3e97dead2596">
</div>

In the next step, a design of TE0802 would generate the required bitstream and later on the .xsa file for creating the PetaLinux Image. 
- The required board files and IPs were downloaded from the Trenz Electronics documentation. This enabled us to work with the TE0802 Board that was added to the list of boards available without directly interfering with Xilinx.
- All the steps were completed successfully and the Hello world application was run on the TE0802
This step was also used to confirm the functioning of the TE0802 Board for further applications along with the creation of the .xsa files for PetaLinux.

## PetaLinux
There was no Board Support Package file available for the direct creation of the Image for the TE0802 Board. Hence, a Board Support Package file  had to be created.

PetaLinux was chosen as:
- It enables developers to synchronize the software platform with the hardware design as it gains new features and devices.
- It will generate a custom, Linux Board Support Package including the drivers for Xilinx embedded processing IP cores, kernel and boot loader configurations.

NOTE: If the Trivial File Transfer Protocol directories were not accessed and hence were dropped during the creation of the image, this warning can be ignored as these directories and capabilities are unnecesary for the functionality of the current task and hence can be ignored.

## Pynq
The final step was to use the Pynq Linux driver to create a working Operating System. 

Pynq was used as:
- It provides a Jupyter-based framework with Python APIs for using Xilinx Adaptive Computing platforms
- It supports Zynq Ultrascale+ TE0802 target board

The commands used: 
- $ sudo echo
- $ make boot_files BOARDS=TE0802
- $ mkdir ccahe
- $ make images BOARDS=TE0802 PREBUILT=./prebuilt/bionic.aarch64.2.3.img
- $ ls ./output/

After the OS was successfully written to the SD Card through Balena Etcher, the TVM directory was downloaded from GitHub and the inference run successfully.
