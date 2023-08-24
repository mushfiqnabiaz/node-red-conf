# Install Node-Red and Auto-Start Node-RED on Boot using systemd (Ubuntu)

This guide explains how to configure Node-RED to automatically start on boot in Ubuntu using systemd.

## Prerequisites

- Ubuntu operating system (tested on Ubuntu 20.04)
- Node-RED installed and working

## Setup Node JS in Ubuntu system

1. **install Node JS 18.X version**
    ```bash
    curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - &&sudo apt-get install -y nodejs
2. **Check Node Version and NPM Version**
    ```bash
    node -v
    npm -v
## Install Node-red and Node-red Admin
1. **Install Node-Red**
    ```bash
    sudo npm install -g --unsafe-perm node-red
2. **install Node-Red Admin**
    ```bash
     sudo  npm install -g --unsafe-perm node-red-admin
3. **Generate Admin Hash Password For Node-Red**
    ```bash
    node-red admin hash-pw
Save the hash password
4. **Change Setting.js for confiqure node red password**
    ```bash
    nano /username/.node-red/settings.js
change the username to your system username

5. **Find adminAuth and Modify the Settings.js**
    ```bash
            adminAuth: {
            type: "credentials",
            users: [{
                username: "username",
               password: "HashPassword",
               permissions: "*"
            }]
        },
    1. Here Chanage user username for your login username
    2. Give the hash password in password section
## Setup Instructions for Node-Red as a Service

1. **Create a systemd Service File**

   Open a terminal and create a new systemd service file for Node-RED:

   ```bash
   sudo nano /etc/systemd/system/node-red.service

2. **Add the following content to the file:**

    ```bash
        [Unit]
            Description=Node-RED
            After=syslog.target network.target

        [Service]
            ExecStart=/usr/bin/node-red-pi --max-old-space-size=128
            WorkingDirectory=/home/your_username/.node-red
            Restart=always
            User=your_username

        [Install]
            WantedBy=multi-user.target

Replace your_username with your actual username and Save.

Or Download the file from the git and paste on the location.  


3. **Enable the Service**
    Enable and start the service:
    
     ```bash
        sudo systemctl enable node-red
        sudo systemctl start node-red

3. **Check Status**
    Verify that the service is running:
    
     ```bash
       sudo systemctl status node-red

4. **Troubleshooting**
    1. *If the service fails to start, check the paths, permissions, and Node-RED installation.*
    2. *Review Node-RED log files in the .node-red directory for more information.*
    3. *Test running Node-RED manually to identify any errors.*
5. **Notes**
    1. *Adjust paths and settings in the service file based on your installation.*
    2. *This guide assumes a standard Node-RED setup. Customize commands if needed.*
