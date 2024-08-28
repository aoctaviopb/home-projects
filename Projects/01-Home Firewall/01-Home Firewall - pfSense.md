# Home Firewall - pfSense

***
- https://www.pfsense.org/
_pfSense_ is a free and open source firewall and router that also features unified threat management, load balancing, multi WAN, and more.
***

## Installation
We will download the firewall **pfSense** from the following repository:
- https://atxfiles.netgate.com/mirror/downloads/
The downloaded version was `pfSense-CE-2.7.2-RELEASE-amd64.iso.gz`

Once the download is completed is necessary to extract the compressed ISO and proceed with its installation in the selected host. In this example we are installing the firewall in a virtual machine (VMware Workstation).

### Copyright and Distribution Notice
First we must to accept the "Copyright and distribution notice". After this we will start the installation of the firewall.
![01-Home Firewall - pfSense](00-Assets/01-Home%20Firewall%20-%20pfSense.png)

### Install pfSense
Select the "Install" option and continue.
![01-Home Firewall - pfSense-1](00-Assets/01-Home%20Firewall%20-%20pfSense-1.png)

### Partitioning Disk
For this installation we will make use of an automatic partitioning of the disk.
![01-Home Firewall - pfSense-2](00-Assets/01-Home%20Firewall%20-%20pfSense-2.png)
- Then we will proceed with the installation

### Select Available Disk
Now we will select the available disk where the firewall will be installed.
![01-Home Firewall - pfSense-3](00-Assets/01-Home%20Firewall%20-%20pfSense-3.png)
- We can select this disk with the `space` key

### Reboot System
After a successful installation the final step is to reboot the system.
![01-Home Firewall - pfSense-4](00-Assets/01-Home%20Firewall%20-%20pfSense-4.png)


## Network Configuration
When the system we will start configuring the network that will be restricted by the firewall. We can observe that a network is already recognized as a valid one:
```shell
Valid interfaces are:

em0 00:0c:29:b8:11:91
```
- This is the network that our virtual machine is part of
### VLANs Configuration
![01-Home Firewall - pfSense-5](00-Assets/01-Home%20Firewall%20-%20pfSense-5.png)
To the question "Should VLANs be set up now?" we will answer "no" passing the key "n".
```shell
n
```

### WAN Interface
Now we will enter the name of the identified WAN. This interface is the one presented in [#Network Configuration](#Network%20Configuration).
![01-Home Firewall - pfSense-6](00-Assets/01-Home%20Firewall%20-%20pfSense-6.png)
```shell
em0
```

The system will ask to if we want to configure a LAN interface but for the moment we just need the WAN interface. Once this configuration is complete we will be prompted to a terminal with some options enable. This confirms that our network configuration was successful.
![01-Home Firewall - pfSense-7](00-Assets/01-Home%20Firewall%20-%20pfSense-7.png)
- You can take a look at your network interfaces and confirm that the IP address of the firewall host is part of VMware network:
![01-Home Firewall - pfSense-8](00-Assets/01-Home%20Firewall%20-%20pfSense-8.png)


## Graphic User Interface
Our firewall is running, now we can visit the given IP address in a web navigator and make use of the graphic user interface.
```shell
https://192.168.65.130/
```
![01-Home Firewall - pfSense-9](00-Assets/01-Home%20Firewall%20-%20pfSense-9.png)
With the default credentials we can log in:
```shell
admin:pfsense
```

And we can see in the firewall terminal a login request for "admin" user.
![01-Home Firewall - pfSense-10](00-Assets/01-Home%20Firewall%20-%20pfSense-10.png)

### Initial Configuration
Once logged in we will start the configuration of the firewall in the GUI.
![01-Home Firewall - pfSense-11](00-Assets/01-Home%20Firewall%20-%20pfSense-11.png)
- Click `Next` to start
#### General Information
Here we will enter some general information as the hostname and the domain name.
![01-Home Firewall - pfSense-12](00-Assets/01-Home%20Firewall%20-%20pfSense-12.png)
#### Time Server Information
We can configure the time server for our actual region.
![01-Home Firewall - pfSense-13](00-Assets/01-Home%20Firewall%20-%20pfSense-13.png)
#### Configure WAN Interface
In this screen we will configure the selected WAN interface. For this example we will select the type as "DHCP".
![01-Home Firewall - pfSense-14](00-Assets/01-Home%20Firewall%20-%20pfSense-14.png)
#### Set Admin WebGUI Password
Now we will change the default password for the "admin" user.
![01-Home Firewall - pfSense-15](00-Assets/01-Home%20Firewall%20-%20pfSense-15.png)
```shell
thisisapassword!
```

Finally we will reload the configuration and we will be finished.
![01-Home Firewall - pfSense-16](00-Assets/01-Home%20Firewall%20-%20pfSense-16.png)

And this will be the dashboard view when we connect to the firewall GUI.
![01-Home Firewall - pfSense-17](00-Assets/01-Home%20Firewall%20-%20pfSense-17.png)


### Aliases
pfSense let us add aliases that will help us with the administration of the network. For example we can assign the alias "Admin_PC" to the IP address of the host where the firewall was installed (`192.168.65.130` in our example) or we can assign an alias to a range network (`192.168.65.100-192.168.65.200`).

![01-Home Firewall - pfSense-18](00-Assets/01-Home%20Firewall%20-%20pfSense-18.png)

![01-Home Firewall - pfSense-19](00-Assets/01-Home%20Firewall%20-%20pfSense-19.png)
- The alias "Kali" was assigned to the host with the IP address `192.168.65.128`

### Firewall Rules



#### Rule 1 - Allow Request from Kali Host
![01-Home Firewall - pfSense-20](00-Assets/01-Home%20Firewall%20-%20pfSense-20.png)

![01-Home Firewall - pfSense-21](00-Assets/01-Home%20Firewall%20-%20pfSense-21.png)

#### Rule 2 - Allow Request from Windows Host



![01-Home Firewall - pfSense-22](00-Assets/01-Home%20Firewall%20-%20pfSense-22.png)


![01-Home Firewall - pfSense-23](00-Assets/01-Home%20Firewall%20-%20pfSense-23.png)



![01-Home Firewall - pfSense-24](00-Assets/01-Home%20Firewall%20-%20pfSense-24.png)





![01-Home Firewall - pfSense-25](00-Assets/01-Home%20Firewall%20-%20pfSense-25.png)



![01-Home Firewall - pfSense-26](00-Assets/01-Home%20Firewall%20-%20pfSense-26.png)


![01-Home Firewall - pfSense-27](00-Assets/01-Home%20Firewall%20-%20pfSense-27.png)







### Creating a Rule
- https://www.zenarmor.com/docs/network-security-tutorials/how-to-configure-pfsense-firewall-rules#pfsense-firewall-rules-examples


- https://www.youtube.com/watch?v=Vm98ofYp05g


```shell
Firewall host:
192.168.65.130

Kali host:
192.168.65.128

Windows host:
192.168.65.1
```




![01-Home Firewall - pfSense-28](00-Assets/01-Home%20Firewall%20-%20pfSense-28.png)



![01-Home Firewall - pfSense-29](00-Assets/01-Home%20Firewall%20-%20pfSense-29.png)



#### Blocking a Malicious IP







![01-Home Firewall - pfSense-30](00-Assets/01-Home%20Firewall%20-%20pfSense-30.png)



![01-Home Firewall - pfSense-31](00-Assets/01-Home%20Firewall%20-%20pfSense-31.png)







![01-Home Firewall - pfSense-32](00-Assets/01-Home%20Firewall%20-%20pfSense-32.png)




```shell
curl -i 192.168.65.128
```


















