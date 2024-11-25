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

Then run the script by running the following command:

```chmod +x setup.sh```

```sudo ./setup.sh```

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

Service file generate-index.service that runs the generate_index script. 
```
# Clone the repo containing the generate_index script
git clone https://gitlab.com/cit2420/2420-as3-starting-files.git /var/lib/webgen/bin
# You must clone this repo to get the generate_index script

# Create a service file that will run generate_index script
cat <<EOL > /etc/systemd/system/generate-index.service
[Unit]
Description=Generate index.html
After=network-online.target
Wants=network-online.target

[Service]
User=webgen
Group=webgen
ExecStart=/var/lib/webgen/bin/generate_index

[Install]
WantedBy=multi-user.target
EOL
```

generate-index.timer that runs the generate-index.service everyday at 5:00
```
# Create generate-index.timer file that will run the service everyday at 05:00
cat <<EOL > /etc/systemd/system/generate-index.timer
[Unit]
Description=Run generate-index.service everyday at 05:00

[Timer]
OnCalendar=*-*-* 05:00:00  # Run the service everyday at 05:00
Persistent=true

[Install]
WantedBy=timers.target
EOL
```
**Verification**

To verify that the timer is active and that the service runs successfully, you can use the following commands:

1. Check the status of the service: 
```
systemctl status generate-index.service
```

2. Check if the timer is active: 
```
systemctl status generate-index.timer
```

3. Check logs to confirm the service runs successfully: 
```
journalctl -u generate-index.service
```

These commands will help you ensure that the timer is set up correctly and that the service is running as expected.
### Task 3: Modify the main nginx.conf 

### Task 4: Set up a firewall

### Task 5: Droplet's IP and webserver 
