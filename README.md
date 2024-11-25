# Linux-Assignment3
Assignment 3 for ACIT 2420 

## Setup Instructions
Before you start the following tasks, make sure you do the following:

```sudo pacman -Syu```
This will update your system and make sure you have the latest packages.

```sudo pacman -S nginx```
This will install the nginx package.

```sudo pacman -S nvim```
This will install the nvim package.

## Tasks
### Task 1: Create a System User
```
#!/bin/bash

# To check if user is running on sudo
if [[ ! $EUID == 0 ]]; then
    echo "$0 is not running as root. Please use sudo."
    exit 1
fi

# Create user webgen with home directory at /var/lib/webgen
useradd -r -m -d /var/lib/webgen -s /usr/bin/nologin webgen 

# Create /bin and /HTML directories
mkdir -p /var/lib/webgen/bin 
mkdir -p /var/lib/webgen/HTML

# Ensure user webgen has ownership of the directories
chown -R webgen /var/lib/webgen
```

### Task 2: Create a Service file that runs generate_index script

### Task 3: Modify the main nginx.conf 

### Task 4: Set up a firewall

### Task 5: Droplet's IP and webserver 
