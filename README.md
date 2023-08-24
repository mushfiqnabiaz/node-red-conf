# Auto-Start Node-RED on Boot using systemd (Ubuntu)

This guide explains how to configure Node-RED to automatically start on boot in Ubuntu using systemd.

## Prerequisites

- Ubuntu operating system (tested on Ubuntu 20.04)
- Node-RED installed and working

## Setup Instructions

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
