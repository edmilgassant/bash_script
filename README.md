# Script for enabling UFW in Ubuntu 22.04 LTS

### Getting Started
- UFW is an uncomplicated firewall that is a user-friendly system for managing a linux firewall. A more simple way to configure and manage iptables. 
- I am going to go over each command and pile it together into a bash script. let's begin!

### Checking status of ufw firewall

```bash
sudo ufw status
```

- If not enabled, run the following command:
```bash
sudo ufw enable
```
- You can create a script to automatically prompt to enable:
```bash
read -p "Enable ufw (y/n): " choice
```
The "read -p" means to read a prompt allowing the user to respond.
"choice" is a variable which stores the input 'y' or 'n' that the user responded with.

- If a user chooses yes or 'y' then add this:
```bash
if [[ "$choice" = [Yy] ]]; then
```
- "$choice" is an input that was stored with the variable (choice) when prompted with a response.
- [Yy] means if a user inputs 'Y' or 'y'

- Adding an option if a user chooses no:
```bash
elif [[ "$choice" = [Nn] ]]; then
```

- elif means another condition. So 'if' condition 1 is "this" then do (elif) condition 2.
- the rest is the same as described above.

### Pile bash script together
```bash
read -p "Enable ufw (y/n): " choice
        if [[ "$choice" = [Yy] ]]; then
        sleep 1
        sudo ufw enable
        echo''
        sleep 1
        sudo ufw status
        elif [[ "$choice" = [Nn] ]]; then
        echo 'skipping'
        fi
```
- I added echo which could be used to copy and output a statement within quotation marks or used for creating space. In this example I used it for creating space by keeping nothing in between the quotation marks.
- sleep is allowing how many seconds before executing the next command.
- fi means finished. Anything between if and fi bracket will be executed.
#

### Since we  understand those concepts as described above, this bash script I created should be easy to read and understand. Let's go!

```bash
#!/bin/bash
echo''
echo '~~~~~~~~~~~~~~~~~~'
echo '+   UFW SCRIPT   +'
echo '~~~~~~~~~~~~~~~~~~'
echo''
echo 'checking ufw install'

# Function to display loading animation
loading() {
    local delay=0.5
    local count=0
    while [ $count -lt 6 ]; do
        printf "-"
        sleep $delay
        count=$((count + 1))
    done
    printf "\n"
}

# Call the loading function
loading

# Run command
sudo ufw status

echo''
read -p "Enable ufw (y/n): " choice
        if [[ "$choice" = [Yy] ]]; then
        sleep 1
        sudo ufw enable
        echo''
        sleep 1
        sudo ufw status
        elif [[ "$choice" = [Nn] ]]; then
        echo 'skipping'
        fi
echo''
read -p "Add 80/tcp and 443/tcp rules (y/n): " choice
        if [[ "$choice" = [Yy] ]]; then
        echo''
        echo "Adding http/https rules"
        loading
        sudo ufw allow 80/tcp
        sudo ufw allow 443/tcp
        echo 'Rules added'
        elif [[ "$choice" = [Nn] ]]; then
        echo 'skipping'
        fi
echo""
read -p "Allow only your PC ssh connection? (y/n): " choice
        if [[ "$choice" = [Yy] ]]; then
        echo''
        sleep 1
        echo '----------------------------------------'
        echo 'Allowing only your PC connection via ssh'
        echo '----------------------------------------'
        loading
        sudo ufw allow from 10.5.4.58 to any port 22
        elif [[ "$choice" = [Nn] ]]; then
        echo 'skipping'
        fi
echo""
echo 'Deny all other IPs from accessing via ssh? (y/n): ' choice
echo''
        if [[ "$choice" = [Yy] ]]; then
        echo 'Denying all other IPs ssh access'
        sudo ufw deny 22
        elif [[ "$choice" = [Nn] ]]; then
        echo 'skipping'
        fi
echo''
sleep 1
echo ''
read -p "Enable ufw 'full' logging full? (y/n): " choice
        if [[ "$choice" = [Yy] ]]; then
        echo''
        sudo ufw logging full
        echo''
        sleep 1
        elif [[ "$choice" = [Nn] ]]; then
        echo 'skipping'
        fi
echo''
echo '+++++++++++++++++++++++++++'
echo '|    Script completed.    |'
echo '+++++++++++++++++++++++++++'
echo ''
sleep 1
echo 'List to add or remove rules with command below:'
echo 'ufw --help'
echo''
sleep 1
sudo ufw status verbose
```

This script enables ufw firewall if I choose too. It also allows rules and logs that I added into the script.
