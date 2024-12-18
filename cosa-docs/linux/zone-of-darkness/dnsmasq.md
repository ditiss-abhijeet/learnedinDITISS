# `dnsmasq`

It is tool to manage DHCP and DNS services on the Fedora which helps manage small networks, assigning the users within the network with the IP address and then making a temprory entry in the DNS server, this helps in caching as the service works faster. Remember that **dnsmasq** is not an independent service running instead it works as a plugin to NetworkManger to get things done. It is the NetworkManager itself, in Fedora, that tells the dnsmasq to work, basically dnsmasq doesn't work on it own, it is the NetworkManager. 

Therefore don't use systemctl to manage the network while the dnsmasq is running. Becuase then there will be competition for the IP address allocation and DNS caching. Let dnsmasq run alone.

As a server administrator, using `dnsmasq` is essential for **Network Management and Automation** , On a server, managing dozens or hundreds of devices can be tricky. **DHCP via `dnsmasq`** automates IP address assignment, ensuring devices in your network can communicate seamlessly. Without it, you would need to manually assign static IPs, which is inefficient and error-prone.

Then, you need to **Dynamic DNS Updates**, Imagine a situation where devices, such as IoT sensors or client machines, keep joining and leaving the network. **Dynamic DNS** allows them to be reachable using their hostnames (like `printer.local`) instead of IPs, which can change frequently. This is essential for service availability and discoverability.

It also helps in **Efficient DNS Caching**, For remote offices or edge servers, DNS requests may be slow if every request hits the public DNS servers. **Caching DNS locally** reduces lookup times and ensures smooth access to frequently visited resources, improving both speed and reliability.

Importantly if you remember PXE boot from windows, PXE booting is a powerful tool in server administration when managing **diskless systems** or **provisioning new servers**. With `dnsmasq`, you can configure a PXE server to load operating systems over the network. This is crucial for **large-scale deployments** or when quickly restoring systems from backups.

Then you need to be able **Handling Local and Public DNS Zones**, As a server admin, you may need to **set up internal DNS zones** (e.g., `internal.example.com`) that are only visible within your network, while public DNS servers handle external queries. `dnsmasq` allows you to manage such zones efficiently.


# So what should be done?

*In that case*, you need to trust the NetworkManager to allow the changes to be made, if you need to make the configuration changes, make changes within the NetworkManager settings only.

```
sudo nano /etc/NetworkManager/NetworkManager.conf
```

NetworkManager ignore the dnsmasq file `/etc/dnsmasq.conf`, so all the network configurations are managed and followed by the NetworkMangers. Infact the DNS changes are also made by the NetworkManager in `/etc/resolv.conf`. 

You might need to check if the dnsmasq is running or not:

```
nmcli device show
```

These command will show the network details and don't forget to prevent the usage of systemctl along with dnsmasq as if you did, it will open a new running instance of the dnsmasq and then there will be fight! 

# How does the Process logically unfolds?

Initially NetworkManager will start when system boots up and it will start all the processes, then Networkmanager will assign the dnsmasq to handle the services of DHCP (Assigning IP addresses) and DNS (Maintaing records of Server). All the configurations will be of NetworkManager, not of dnsmasq, if any changes to the network occurs, it will update the dsnmasq, and rest all the management will keep of running by NetworkManager.

*How NetworkManager and dnsmasq Work Together?*, it will be as following:

1. NetworkManager **starts** when your system boots up. <br>

2. If Network Manage detects a network connection, it **starts** dnsmasq to handle:
   - DHCP (assigning IP addresses to devices on your network)
   - DNS caching (making websites load faster by storing DNS responses locally)
   <br>

3. NetworkManager **decides** what settings dnsmasq should use, **ignoring** the manual dnsmasq config file (`/etc/dnsmasq.conf`), because NetworkManager needs to be in full control. <br>

4. If the connection **changes** (e.g., you switch to a different Wi-Fi network or enable a VPN), **NetworkManager updates dnsmasq** settings automatically, ensuring your network keeps running smoothly. <br


# How to Set Up and Administer dnsmasq

First you need to install the dnsmasq using the [dnf](dnf.md) package manager in fedora.

```
sudo dnf install dnsmasq -y
```

Once done, you need to know **four** things, **first and foremost**, do not use systemctl to start the dnsmasq, **second**, you need to know that there is default **dns** running which is configured in **/etc/resolv.conf** file that will have the entry of default dns which will be resolving the IP addresses and now we need out NetworkManager using the dnsmasq configuration for running the DNS server, so we need to disable it using the below command.

```
sudo systemctl disable systemd-resolved
sudo systemctl stop systemd-resolved
```

# Basic Configuration

All dnsmasq-related configurations that you want NetworkManager to use should be placed in the following file below:

```
/etc/NetworkManager/dnsmasq.d/
```

This directory is where you add individual configuration files for specific tasks (e.g., managing DNS, DHCP, or network interfaces). 

If you need to create static DNS entries (i.e., specific IPs always map to specific hostnames), use this file as below:

```
/etc/dnsmasq.conf
```

