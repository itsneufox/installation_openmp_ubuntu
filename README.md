<a href="https://www.open.mp"><img src="https://raw.githubusercontent.com/adib-yg/openmp-server-installation/main/screenshots/open-mp-logo.png" width="128" height="128" align="left"></a><h1>open.mp Server Installation<br>(All Debian based Linux)</h1>
<br>
> [!NOTE] 
> *If you are using the SA:MP server and didn't convert to open.mp yet, [please stop here and read this guide](https://github.com/adib-yg/openmp-server-installation)!*

> [!NOTE] 
> *If you are using the FCNPC plugin, please stop for now because this plugin does not work for open.mp currently.<br>
> But not for long! [You can help with a donation here on the Open Collective!](https://opencollective.com/openmultiplayer)*
<br>

## Introduction

Welcome! This repository contains a comprehensive guide on installing an open.mp server on Ubuntu or another Debian based Linux.<br>
Whether you're a beginner or just looking to refresh your knowledge, this guide should have something for you.

<br>

## Prerequisites
Before starting this guide, you should have:
- A machine running Ubuntu (20.04 or later recommended) or another Debian based Linux;
- Filezilla or WinSCP for file transfers;
- PuTTY or your hosting SSH solution;<br>
> [!NOTE] 
> *If you install WinSCP, the installer will prompt you to install PuTTY!<br>
> It's up to you if you want to install it or not, but you can always download it later!*
  
<br>

## Part A - Connect, update and create user

### Step 1 - Open PuTTY or your hosting SSH solution and connect to your  instance
> [!NOTE] 
> *There are compreensive guides on the web or even your hosting solution website on how to connect via PuTTY.<br>
> Some SSH connections need a key, so i can't provide any help here, but feel free to ask on open.mp discord or search the web!*

<br>

### Step 2 - Updating your Ubuntu instance
  - Let's ensure that your system is up-to-date:
```sh
sudo apt update
```
```sh
sudo apt upgrade
```
<br>

### Step 3 - Create a new user
  - For security reasons, it's best practice to create a new user specifically for running the server:
> [!NOTE] 
> *Change MyUserName to a username of your choice!*
```sh
sudo adduser MyUserName
```
  - *[OPTIONAL]* After creating the user, add it to the sudo group:
```sh
sudo usermod -aG sudo MyUserName
```
<br>

### Step 4 - Give permission to the root user
  - We need to give the root user access to the folder so when using Filezilla or WinSCP you can write and read the files inside the user folder:
```sh
chmod 775 /home/MyUserName
```
<br>

## Part B- Download and install the server files

### Step 5 - Download the server files
  - We can do this two ways, the **blind way** or the **noob-proof way**...

<br>

### The blind way:
I call it that because we are only using terminal to do the job!
  - Use **wget** to download the files from the open.mp repository
```sh
wget https://github.com/openmultiplayer/open.mp/releases/download/v1.2.0.2670/open.mp-linux-x86.tar.gz
```
> [!NOTE] 
> *In this guide we are downloading the static version!<br>
> Check the latest version marked with a green tag saying "Latest" [here](https://github.com/openmultiplayer/open.mp/releases), then right click the intended file and copy the link!*

   - Extract the downloaded files
```sh
tar -xzf open.mp-linux-x86.tar.gz
```
   - Navigate to the extracted directory
```sh
cd Server
```

<br>

### The noob-proof way:
You know why i call it that... I think...
  - [Go here](https://github.com/openmultiplayer/open.mp/releases) and check the release marked with a green tag saying "Latest";
  
  - Download the file called "open.mp-linux-x86.tar.gz";
> [!NOTE] 
> *In this guide we are downloading the static version!*

  - Use 7zip or your zip manager of choice and unzip the file downloaded;
  - Open Filezilla or WinSCP and drop the folder "Server" inside the folder of the user you created in **Part A**
  
<br>

## Part C - Finishing up and starting the server

### Step 6 - Install x86 files
> [!NOTE] 
> *If you used the noob-proof way, come back to PuTTY or your hosting SSH solution and navigate to your server folder using:*
>```sh
>cd Server
>```
  - We have to update apt:
```sh
sudo apt update
```
  - Let's enable support for 32-bit packages since we are on a 64-bit system:
```sh
sudo dpkg --add-architecture i386
```
  - Now to really install it:
```sh
sudo apt install libc6:i386
```
<br>

### Step 7 - Starting up the server
> [!NOTE] 
> *This is only needed once, after that you can skip to starting up without using chmod!*
>  - We need change the permissions of omp-server, specifically to make it executable:
>```sh
>chmod +x omp-server
>```


- The command to start it up:
```sh
nohup ./omp-server &
```
 - The terminal should then output something like this:
```
[1] MyNumberHere
MyUserName@ip-123-45-67-89:/home/MyUserName$ nohup: ignoring input and appending output to 'nohup.out'
```
  - Write down the number the terminal gave you and you can close the terminal!

> [!NOTE] 
> *If you forgot to write down the number, ~~YOU FUCKED UP~~ it's not problem, we will use the command 'top' on Step 8*

<br>

### Step 8 - Closing the server
So, now you know the server is working as intended and you want to close the server
  - If you wrote down the number in step 7 just do:
```sh
sudo kill MyNumberHere
```
> [!NOTE] 
> *Change MyNumberHere to the intended number!*

  - If you ~~fucked up my guide and~~ forgot to copy the number do:
```sh
top
```
  - Wait 2/3 seconds while the list updates and check for something like this at the top:
```
MyNumberHere | MyUserName | 00 | 0 | 00 | 00 | 00 | S | 0.0  | 0.0 | 0:00.00 | omp-server
```
  - Write it down or memorize it and then do:
```sh
sudo kill MyNumberHere
```
  
<br>

## Part D - Uploading your own gamemode and files

- Visit [this guide](https://github.com/adib-yg/openmp-server-installation) to understand how to transfer your files from your server to your Ubuntu instance.

> [!NOTE] 
> *Don't forget that Ubuntu can't read .dll files, always download the .so counterparts!*

<br>
<br>

# Help
If you have issues with the server or this guide, [please join the official open.mp Discord server](https://discord.gg/samp) and use the [#openmp-support](https://discord.com/channels/231799104731217931/966398440051445790) channel.

<br>
<br>

# Final words
If you feel anything wrong with this guide, please feel free to ping me @itsneufox on [the official open.mp Discord server](https://discord.gg/samp) and let me know!<br>

### Thanks to the open.mp team for their awesome work and their effort to keep this community alive!
