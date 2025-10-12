# How to set up Kali Linux

## what is virtual machine 

software-based emulation of a physical computer. It runs an OS and applications just like a physical computer, but it operates within a host system, using virtualised hardware resources such as CPU, memory, and storage. 

## what is a hypervisor 

software, firmware, or hardware that creates and manages VMs. it allows multiple VMs to run on a single physical host by sharing and allocating the hosts hardware resources, such as CPU, memory, and storage. 

There are two types : 

Type 1 : directly on hardware, better performance 
Type 2 : runs on host os, easier to use, personal use 

# WSL 2 

For this example we will be using WSL 2, windows subsystem for linux 2, allows you to run a full linux kernel directly on windows. provides light weight virtualised env to run linux distributions natively without the need for separate virtual machines or dual boot setup.

**step1** :

```powershell 

# run in admin mode 

Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

```

restart powershell back into admin 

**step2** : 

```powershell

dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart


# second command 

dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

```

restart 

**step3** 

install this :  (Linux kernal)[https://aka.ms/wsl2kernel]

**step4** 

```powershell

 wsl --set-default-version 2

 # dont close the terminal 

 go to ms sore and search for kali linux and install 

 open up the application and provide a username and password 

 # within this terminal, not powershell run this : 

sudo apt update && sudo apt upgrade -y

sudo apt install kali-desktop-xfce -y

# while waiting for that install go back to powershell and run this : 

wsl --list --verbose # checks version 

# go back to kali linux terminal and run this : 

sudo apt install xrdp -y

# lastly run this 

sudo service xrdp start # starts our server

# now that we have the gui lets go into, first we need our ip, within the same terminal 

ip add 

# in the search bar look for remote desktop connection, and type in your ip address 

# you will be prompted to type in your username and password 

when you close your server simply run this 

sudo service xrdp start # log in again 


```