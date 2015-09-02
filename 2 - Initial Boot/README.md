# Initial Boot

Now that we have Arch Linux ARM on the micro sd card, safely remove the micro sd card from your computer and put it into the raspberry pi 2.

It is assumed that you have a network that has:

* DHCP server
* DNS server
* Internet access

If you do not have these, you will have to configure your pi's networking interface manually, [link](https://wiki.archlinux.org/index.php/Network_configuration#Static_IP_address), and set the host file manually, [link](https://wiki.archlinux.org/index.php/Network_configuration#Local_network_hostname_resolution). You will also need to install some packages manually, [link](https://wiki.archlinux.org/index.php/Offline_installation_of_packages#A_simple_example).

Connect the ethernet to the pi and networking switch. Make sure the switch has an ethernet of it's own going to the internet.

If you have a hdmi display monitor, you may plug it into the pi.

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

If ping and ssh did not work, then you need to connect your pi to an hdmi display monitor. If you do not have one, you can get a [vga to hdmi converter](http://www.ebay.com/bhp/vga-to-hdmi-converter), along with a usb keyboard. Make sure to reboot your pi with everything connected.

Once you have logged into the pi as ```root```, assuming the ethernet cable is connected and has internet connectivity, run
```bash
dhcpd
```

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

If you are using Windows, run Putty and put in ```alarmpi``` under the host, as shown below.

<a href="https://github.com/bliz937/piDoop/blob/master/2%20-%20Initial%20Boot/images/0.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/2%20-%20Initial%20Boot/images/0.png" alt="ssh on Windows using Putty" align="middle" /></a>





---

[<< prev](https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/README.md#installing-arch-linux-arm) | [next >>]()
