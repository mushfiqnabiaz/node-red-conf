# Auto-Start Node-RED on Boot using systemd (Ubuntu)

This guide explains how to configure Node-RED to automatically start on boot in Ubuntu using systemd.

## Prerequisites

- Ubuntu operating system (tested on Ubuntu XX.XX)
- Node-RED installed and working

## Setup Instructions

1. **Create a systemd Service File**

   Open a terminal and create a new systemd service file for Node-RED:

   ```bash
   sudo nano /etc/systemd/system/node-red.service
