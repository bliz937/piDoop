# Initial Boot

Now that we have Arch Linux ARM on the micro sd card, safely remove the micro sd card from your computer and put it into the raspberry pi 2.

It is assumed that you have a network that has:

* DHCP server
* DNS server
* Internet access

If you do not have these, you will have to configure your pi's networking interface manually, [link](https://wiki.archlinux.org/index.php/Network_configuration#Static_IP_address), and set the host file manually, [link](https://wiki.archlinux.org/index.php/Network_configuration#Local_network_hostname_resolution). You will also need to install some packages manually, [link](https://wiki.archlinux.org/index.php/Offline_installation_of_packages#A_simple_example).

Connect the ethernet to the pi and networking switch. Make sure the switch has an ethernet of it's own going to the internet.

If you have an hdmi display monitor, you may plug it into the pi.

Plug in the micro usb power cable into the pi and give it a few seconds, around 30 seconds, to boot.

Try pinging the pi - in Ubuntu.
```bash
ping alarmpi
```

If you get a response, try ssh
```bash
ssh alarmpi
```

The username and password are both ```root```.

#### Connecting with display monitor

If ping and ssh did not work, then you need to connect your pi to an hdmi display monitor. If you do not have one, you can get a [vga to hdmi converter](http://www.ebay.com/bhp/vga-to-hdmi-converter), along with a usb keyboard. Make sure to reboot your pi with everything connected.

Once you have logged into the pi as ```root```, assuming the ethernet cable is connected and has internet connectivity, run
```bash
dhcpd
```

#### Enable root login via ssh

If you could not ```ssh``` as root, then do the following:

```bash
nano /etc/ssh/sshd_config
```

Use the arrows on the keyboard to navigate down in the file until the ```Authentication``` section. Add

```PermitRootLogin yes```
press ctrl+x, y and enter.

Finally restart the ssh daemon to reload the config file:
```bash
systemctl restart sshd
```

Then, again, try to ssh into the pi:
```bash
ssh root@alarmpi
```

#### ssh from Windows

If you are using Windows, run Putty and put in ```alarmpi``` under the host, as shown below.

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/0.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/0.png" alt="ssh on Windows using Putty" align="middle" /></a>


#### Updating packages

Update the repositories and packages:
```bash
pacman -Syu
```

The image below is just to show what a typical update would look like, you may have more packages to update than what is in the image. That is ok.

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/1.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/1.png" alt="Arch Linux ARM update repo and packages with pacman -Syu" align="middle" /></a>

If you get an error like the one below

##### Manually installing packages with pacman

```bash
error: failed retrieving file 'systemd-225-1-armv7h.pkg.tar.xz' from mirror.archlinuxarm.org : Operation too slow. Less than 1 bytes/sec transferred the last 10 seconds
warning: failed to retrieve some files
```

Simply Google your package and install in manually as such:
<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/2.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/2.png" alt="Google Arch package" align="middle" /></a>

This search lead us to [us.mirror.archlinuxarm.org](http://us.mirror.archlinuxarm.org/armv7h/core/)

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/3.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/3.png" alt="US Arch Linux ARM" align="middle" /></a>

Copy the link to the package you require, in this case ours is ```systemd-225-1-armv7h.pkg.tar.xz```.

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/4.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/4.png" alt="Copying link to Arch Linux ARM package" align="middle" /></a>

In terminal, run the following:

```bash
cd /tmp
pacman -S wget
wget http://us.mirror.archlinuxarm.org/armv7h/core/systemd-225-1-armv7h.pkg.tar.xz
pacman -U systemd-225-1-armv7h.pkg.tar.xz
```

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/5.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/5.png" alt="Downloading Arch Linux ARM package with wget" align="middle" /></a>

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/6.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/6.png" alt="Installing Arch Linux ARM package with pacman -U" align="middle" /></a>

Then rerun
```bash
pacman -Syu
```

Simply repeat the process for any other packages which cannot be downloaded.

If you happen to get another error
```error: failed to commit transaction (conflicting files)```, simply run:

```bash
pacman -Sc
```

If the error still persists, have a link [here](https://wiki.archlinux.org/index.php/Pacman#.22Failed_to_commit_transaction_.28conflicting_files.29.22_error).

#### WiFi

If you would like to setup your USB Wifi adapter, follow this steps to follow, otherwise skip ahead.

We will be using the [Arch](https://wiki.archlinux.org/index.php/Wireless_network_configuration#Device_driver) documentation.
The WiFi adapter that we have is the Edimax 802.11b/g/n nano USB adapter - EW-7811Un. Plug in your adapter.

To confirm that the adapter is picking up on the pi, lets run

```bash
lsusb
````
As we can see, ```Device 006``` is our adapter.

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/7.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/7.png" alt="Arch Linux ARM lsusb" align="middle" /></a>

Looking at the end, ```[Realtek RTL8188CUS]```, gives us the chipset. We can confirm that this chipset is supported on Linux with [linux-wless.passys.nl](http://linux-wless.passys.nl/).

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/8.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/8.png" alt="Checking chipset support on linux-wless.passys.nl" align="middle" /></a>

We see that our driver is ```RTL8192CU```.
Running
```bash
pacman -Ss dkms*
```
We can see that the ```dkms-8192cu``` driver supports the RTL8188CUS chipset.

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/9.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/9.png" alt="Searching for drivers with pacman" align="middle" /></a>

Running the following to install it:

```bash
pacman -S dkms-8192cu
```

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/10.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/10.png" alt="Installing dkms-8192cu with pacman" align="middle" /></a>

If you get an error about ```kernel headers```, run
```bash
pacman -S linux-raspberrypi-headers
```
<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/11.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/11.png" alt="Installing dkms-8192cu kernel headers error" align="middle" /></a>

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/12.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/12.png" alt="Installing linux-raspberrypi-headers" align="middle" /></a>

After installing the driver, running ```ifconfig -a```, we can see our adapter being picked up.

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/13.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/13.png" alt="ifconfig -a" align="middle" /></a>

Next, we want to run ```wifi-menu``` to easily join a wireless network. Before doing so, install ```dialog``` and ```wpa_supplicant``` by
```bash
pacman -S dialog wpa_supplicant
```

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/14.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/14.png" alt="installing dialog to use wifi-menu" align="middle" /></a>

Running ```wifi-menu``` will give a display as such:

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/15.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/15.png" alt="running wifi-menu" align="middle" /></a>

We will join the network ```free4All``. This access point does not require a password to join, but we will show how to set the password should yours be. When selecting the access point, you can rename the profile for the access point. We have done so here and renamed ours to ```free```.

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/16.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/16.png" alt="wifi-menu renaming profile" align="middle" /></a>

```wifi-menu``` will then go back to terminal.
Should your access point require a password, simply edit the profile file. In our case, that would be

```bash
nano /etc/netctl/free
```

Changing ```security``` to your AP security type. For an example, say it is WPA2. Then make change it to ```security=wpa```. Then on a new line, add ```key=password```, where password is your AP password. Press ctrl+x to exit and save the file.

---

[<< prev](https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/README.md#installing-arch-linux-arm) | [next >>]()
