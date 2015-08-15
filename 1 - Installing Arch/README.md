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


### root shell

In Ubuntu, open up a shell, this can usually be done by pressing *ctrl*+*alt*+*t* on the desktop.

In the shell, type in

```bash
sudo su
```

This will ask you for your password and then change you to the *root* user.

<a href="https://github.com/bliz937/piDoop/blob/master/1%20-%20Installing%20Arch/images/4.png"><img src="https://raw.githubusercontent.com/bliz937/piDoop/master/1%20-%20Installing%20Arch/images/4.png" alt="Linux sudo su to root" align="middle" /></a>

---

[<< prev](https://github.com/bliz937/piDoop/blob/master/0%20-%20Requirements/README.md#minimum-requirements) | [next >>]()

[1]: https://en.wikipedia.org/wiki/Category:Ubuntu_(operating_system)_derivatives
