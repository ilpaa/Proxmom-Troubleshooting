# Setting Up Static IP Address on Ubuntu Server

This guide will walk you through the process of configuring a static IP address on an Ubuntu Server machine. 

## Prerequisites

- Access to your Ubuntu Server via SSH or physical access.
- Basic understanding of the Linux command line.

## Steps

### 1. Determine Network Interface Name

Open a terminal on your Ubuntu Server and type the following command to determine the name of your network interface:

```bash
ip a
```

Look for the network interface name, typically starting with "en" (Ethernet) or "wl" (Wireless).

### 2. Edit Netplan Configuration

Ubuntu Server uses Netplan to manage network configurations. You'll need to edit the Netplan configuration file. Open the configuration file using a text editor like Nano:

```bash
sudo nano /etc/netplan/01-netcfg.yaml
```
Replace `01-netcfg.yaml` with the appropriate file name if it's different.

### 3. Configure Static IP
Inside the Netplan configuration file, you'll see a YAML structure similar to the following:

```bash
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3: # Replace enp0s3 with your network interface name
      dhcp4: yes
```

Change `dhcp4: yes` to:

```bash
dhcp4: no
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4
```

Replace your_static_ip, your_subnet_mask, and your_gateway_ip with your desired static IP address, subnet mask, and gateway IP address respectively.

## 4. Apply Changes

After making the necessary changes, save the file and exit the text editor. Apply the new network configuration using the following command:

```bash
sudo netplan apply
```

## 5. Verify
Check if the changes have taken effect by running:

```bash
ip a
```

Look for your network interface and verify that it's configured with the static IP address you set.


