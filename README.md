<a href="https://www.open.mp"><img src="https://raw.githubusercontent.com/adib-yg/openmp-server-installation/main/screenshots/open-mp-logo.png" width="128" height="128" align="left"></a>
<h1>Easy open.mp Server Installation<br>(All Debian based Linux)</h1>
<br><br>

> [!NOTE] 
> *If you are using the SA:MP server and didn't convert to open.mp yet, [please stop here and read this guide](https://github.com/adib-yg/openmp-server-installation)!*

> [!NOTE] 
> *If you are using the FCNPC plugin, please stop for now because this plugin does not work for open.mp currently.<br>
> [You can help with a donation here on the Open Collective!](https://opencollective.com/openmultiplayer)*

## Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Phase 1: Preparing the Environment](#phase-1-preparing-the-environment)
- [Phase 2: Installing open.mp Server Files](#phase-2-installing-openmp-server-files)
- [Phase 3: Configuring and Starting the Server](#phase-3-configuring-and-starting-the-server)
- [Phase 4: Managing the Server](#phase-4-managing-the-server)
- [Phase 5: Uploading Your Gamemode and Files](#phase-5-uploading-your-gamemode-and-files)
- [Help](#help)
- [Final Words](#final-words)

## Introduction

Welcome! This repository contains a comprehensive guide on installing an open.mp server on Ubuntu or another Debian based Linux.<br>
Whether you're a beginner or just looking to refresh your knowledge, this guide should have something for you.

## Prerequisites
Before starting, you should have:
- A machine running Ubuntu (20.04 or later recommended) or another Debian based Linux;
- WinSCP or Filezilla for file transfers;
- PuTTY or your hosting SSH solution;<br>
> [!NOTE] 
> *If you install WinSCP, the installer will prompt you to install PuTTY!<br>
> It's up to you if you want to install it or not, but you can always download it later!*

## Phase 1: Preparing the Environment

1. Connecting via SSH:
   - Use PuTTY or your hosting SSH solution to connect to your instance.

> [!NOTE] 
> Seek online guides or your hosting provider's documentation if you're unsure how to connect to your Linux Instance.

2. Updating your Linux Instance:
   - Before proceeding, let's ensure your system is up to date by running:

   ```sh
   sudo apt update
   ```
   ```sh
   sudo apt upgrade
   ```

3. Creating a secure service account:
   - For security reasons, we should create a dedicated service account without a home directory:

   ```sh
   sudo useradd -M svc-omp-server
    ```

4. Locking the service sccount:
   - Let's prevent the service account from being used for login:

   ```sh
   sudo usermod -L svc-omp-server
   ```

5. Creating a directory for the server files:
   - We will use the /opt directory, this is the standard location for third-party applications:

   ```sh
   sudo mkdir /opt/omp-server
   ```

6. Setting permissions for the directory:
   - Changing the group of the directory to match the service account:

   ```sh
   sudo chgrp svc-omp-server /opt/omp-server
   ```

   - Setting the g+s flag so new files inherit the correct group and remove access for others:

   ```sh
   sudo chmod g+s /opt/omp-server
   ```
   ```sh
   sudo chmod o-rwx /opt/omp-server
   ```

---

## Phase 2: Installing open.mp Server Files

7. Let's navigate to the server directory:
   - We need to switch to the /opt/omp-server directory where the server will be stored:

   ```sh
   cd /opt/omp-server
   ```

8. Downloading the open.mp server files:
   - Download the latest release of the open.mp server:

   ```sh
   sudo -u svc-omp-server wget https://github.com/openmultiplayer/open.mp/releases/download/v1.2.0.2670/open.mp-linux-x86.tar.gz
   ```

> [!NOTE] 
> You should check for the latest release at the open.mp GitHub Releases page: https://github.com/openmultiplayer/open.mp/releases.

9. Extracting the server files:
   - Once downloaded, extract the files:

   ```sh
   sudo -u svc-omp-server tar -xzf open.mp-linux-x86.tar.gz
   ```

---

## Phase 3: Configuring and Starting the Server

10. Installing the required x86 libraries:
    - Since the server runs as a 32-bit application, you need to enable 32-bit architecture support:

    ```sh
    sudo dpkg --add-architecture i386
    ```
    ```sh
    sudo apt update
    ```
    ```sh
    sudo apt install libc6:i386
    ```

11. Making the server executable:
    - Change the permissions so the server can be executed (only required once):

    ```sh
    cd /opt/omp-server/Server/
    ```

    ```sh
    sudo chmod +x omp-server
    ```

12. Starting the server:
    - Use the following command to start the server in the background:

    ```sh
    nohup ./omp-server &
    ```

    - The terminal will output a process ID (PID). Write this number down for future reference.

---

## Phase 4: Managing the Server

13. Stopping the server:
    - To stop the server, use the PID from step 12 and run:

    ```sh
    sudo kill <PID>
    ```

14. Finding the Process ID (if forgotten):

    - If you forget the process ID, run:

    ```sh
    top
    ```

    - Look for the omp-server process in the list, note the PID, press 'Q' to quit, and then kill the process as shown in step 13.

---

## Phase 5: Uploading Your Gamemode and Files

15. Upload your custom gamemodes and scripts:
    - Use WinSCP or Filezilla to transfer your gamemodes and scripts to the /opt/omp-server directory.
    Important: Make sure to use .so files for Linux plugins, as .dll files are only supported on Windows.

---

# Help
For any issues related to the server or this guide, [please join the official open.mp Discord server](https://discord.gg/samp) and post your questions in the [#openmp-support](https://discord.com/channels/231799104731217931/966398440051445790) channel.

---

# Final words
If you notice any inaccuracies or have suggestions regarding this guide, feel free to reach out to me @itsneufox on [the official open.mp Discord server](https://discord.gg/samp). I appreciate your feedback!


### A big thank you to Vince0789, Mido and others for raising important security concerns and assisting in enhancing the security practices in this guide!
### Additionally, thanks to the open.mp team for their incredible work and dedication!
