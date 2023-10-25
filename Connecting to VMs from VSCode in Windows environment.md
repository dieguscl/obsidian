# Considerations

- You are working on a Windows machine
- You have VMs running on Hyper-V
- You want to connect to those machines to work in them (preferrably from VS Code)
- You have an SSH config file dictating the IPs of your VMs and hostnames

If this sound like you, then you probably know what it can be annoying to deal with this setup, so keep reading

# Problems to solve

- VMs changing their IP address after a reboot
- Updating the SSH config file each time
- SSH prompting for a password on each connection

# How to solve them

## IP changes

The way that I decided to handle IP addresses changing on every reboot was with a PowerShell script. It does the following: 

1. Read the IP address of a specific VM based on the MAC address
2. Change the specific line of the SSH config where the IP lives

