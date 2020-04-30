# How do I configure internet access + web services for a linux guest?

## Goals

* Internet access for the guest.
* Access to guest provided web services from the host.
* Using a hostname instead of an IP address to access the guest.

## How

* Configure two virtual network adapters in the virtual machine: one in "Bridged" mode, the other in "Host-only" mode.
* For the "Bridged" mode adapter, confirm you are using the correct network adapter on the host (i.e. WiFi card or USB tethering via mobile phone).
* For the "Host-only" mode adapter, you need to connect the IP address assigned to the VM to a hostname.
    * The VirtualBox networking panel will show a hardware (i.e MAC) associated with the "Host-only" mode adapater.
    * Use `ifconfig`; it will display a MAC address with an IP address. Find the IP address linked to the above MAC address.
	* On the host, edit the hosts file and connect the IP address with the hostname you desire (e.g. virtualbox.srvr)

## Why

Configuring these individually is straight forward: for your guest host to access the internet, putting your network adapter into 'Bridged' or 'NAT' mode gets you that. 'Bridged' means that your guest will be seen on the network as a separate device. 'NAT' means that your host serves as a router and hides your guest from the rest of the network. For your guest host to provide services, "Bridged" is usually the mode you want, but that won't let you create a a hostname for your guest server because your IP address will always be changing.

One way to do this is to configure two virtual networking cards, one setup as a bridged adapter, the other setup as a host-only adapter. The bridged adapter allows us to access the internet; this needs to be configured to use specific networking hardware on the host. Since we want to use a specific hostname, we need to use "Host-only" too. Otherwise "Bridged" will only give us a dynamic IP address that can't be linked to a hostname.

# Why don't we use Hyper-V on Windows?

Hyper-V is marketed towards server deployments of guest OSes while Virtual Box is a more general solution, including supporting desktop usage. We use VB for our China bank management. Using Hyper-V doesn't allow us to use Virtual Box. And sharing folders isn't as straight forward.
