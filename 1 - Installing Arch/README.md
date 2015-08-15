# Installing Arch Linux ARM

We will be using [Ubuntu](http://www.ubuntu.com/download/desktop) in a virtual machine - [Virtual Box](https://www.virtualbox.org).
Alternatively you can have Ubuntu, or any [Ubuntu derived distribution][1], installed on your machine, or run the [Live CD](http://www.ubuntu.com/download/desktop/try-ubuntu-before-you-install).

We will be running in root to avoid any permission holdups.

If you are not using a virtual machine, you can ignore the steps that have VM in the title.

We will not cover installing Ubuntu in a virtual machine, for that you can follow this guide: [link](https://askubuntu.com/questions/142549/how-to-install-ubuntu-on-virtualbox)

### Configure VM network

Once the VM has started, in the bottom right of the VM, right click on the network icon.

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/1.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/1.png" alt="Virtual box network icon" align="middle" /></a>

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/2.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/2.png" alt="Virtual box opening network configuration" align="middle" /></a>

The network configuration panel will open. To make things simple, make sure that the *Enable Network Adapter* check box is enabled and that the *Attached to* option is set to **NAT**

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/3.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/3.png" alt="Virtual box network attached to NAT" align="middle" /></a>

Simply click the *OK* button to save the changes.

#### Accessing the micro sd card from the VM

If you are using a VM, you will need to manually add the card to the VM. The following is taken from [www.sandyscott.net](http://www.sandyscott.net/2013/08/14/virtualbox-direct-drive-access/)

On your windows machine, click start and search for power shell. Right click on the result and select *Run as Administrator*.

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/5.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/5.png" alt="Windows 8.1 Power Shell run as Administrator" align="middle" /></a>

Change directory to your Virtual Box installation.

```PowerShell
cd 'C:\Program Files\Oracle\VirtualBox'
```

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/6.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/6.png" alt="Power Shell cd to Virtual Box install directory" align="middle" /></a>

List connected drives.

```PowerShell
WMIC.exe diskdrive list brief
```

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/7.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/7.png" alt="list drives WMIC" align="middle" /></a>

Notice that the last drive, *\\.\PHYSICALDRIVE2*, has *SD Card* in the name.

Create a link file to the SD Card.

```PowerShell
.\VBoxManage.exe internalcommands createrawvmdk -filename "C:\sdcard.vmdk" -rawdi
sk "\\.\PHYSICALDRIVE2"
```

If you get the error

```PowerShell
VBoxManage.exe: error: Error code VERR_PATH_NOT_FOUND
```

it is because you did not provide an absolute path for the vmdk.


Right click on your VM and select *settings*.

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/8.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/8.png" alt="Virtual Box settings" align="middle" /></a>

Click on *storage* and select the hard disk plus button.

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/9.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/9.png" alt="Virtual Box add hard disk" align="middle" /></a>

Select *Choose existing disk*.

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/10.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/10.png" alt="Virtual Box add hard disk choose existing disk" align="middle" /></a>

Navigate to where you saved the **vmdk**, select the vmdk and click open.

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/11.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/11.png" alt="Virtual Box adding vmdk" /></a>

If you get a permission error, close Virtual Box and open it as Administrator - same step as above with Power Shell. Then simply redo the above steps of adding the hard disk in the Virtual Box settings.

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/12.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/12.png" alt="Virtual Box vmdk persmission error" /></a>

You should now see two drives.

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/13.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/13.png" alt="Virtual Box added vmdk" /></a>

Click *ok* to close the settings window and click start on your VM to launch it.

### root shell

In Ubuntu, open up a shell, this can usually be done by pressing *ctrl*+*alt*+*t* on the desktop.

In the shell, type in

```bash
sudo su
```

This will ask you for your password and then change you to the *root* user.

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/4.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/4.png" alt="Linux sudo su to root" align="middle" /></a>

### Installing Arch Linux ARM on the micro sd

The following is taken from the [Arch Linux ARM](http://archlinuxarm.org/platforms/armv7/broadcom/raspberry-pi-2) website. This is to be done in Ubuntu.

Insert the micro sd card into the adapter, and then into your computer.

Find the sd card path.

```bash
fdisk -l
```

We are using an 8gb mirco sd card. As we can see from the image, the path to the card is **/dev/sdb**

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/14.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/14.png" alt="Linux fdisk -l" align="middle" /></a>



---

[<< prev](https://github.com/bliz937/piDoop/blob/master/0%20-%20Requirements/README.md#minimum-requirements) | [next >>]()

[1]: https://en.wikipedia.org/wiki/Category:Ubuntu_(operating_system)_derivatives
