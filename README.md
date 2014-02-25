vagrant-centos
==============

Want a CentOS base box for Vagrant?  Don't want a not-so-fresh feeling about downloading an untrusted one?


## Prepare your VirtualBox environment

Before attempting to create your new Vagrant base box, make sure you do the following

- have VirtualBox installed
- open VirtualBox, go to settings/preferences, choose 'Networking', and add at least one virtual (Host-only) network

That network will be used in step (3) below, where network adapter's name is `vboxnet0` (relevant for `vagrant-centos` file you'll find in this repo). HOSTIP below will most probably be `192.168.56.1` as a default IP of the `vboxnet0`, still it might happen that VirtualBox assigns some other IP address range, so check it out with `ifconfig` in your host OS and pick up your host's computer's IP address for adapter `vboxnet0` there.

_Note: Also, `vagrant-centos` file contains configuration for virtual SATA controller, which has 2 different syntaxes, based on the version of VirtualBox you're running. 2 possible options are both in the file, one of them active, and the other commented-out. See the file and change the active option if your Vagrant base box installation will say it sees no HDD to install to._


## Create your CentOS Vagrant base box

Create your own minimal CentOS base box for Vagrant in a few simple steps:

1. download a CentOS minimal ISO from your favorite mirror
2. run `bash vagrant-centos majorversion minorversion` (1) to create/start the VM and mini web server
3. hit TAB at the CentOS menu, append ` ks=http://HOSTIP:8000/vagrant-centos.ks` (2) (3), and hit ENTER
4. CTRL-C the web server **AFTER** the VM has automatically shut down, then wait for it to package

(1) the CentOS and guest additions ISO locations are specified in variables, and default to a Mac OS X layout<br>
(2) the Kickstart URL with dynamic host IP lookup is printed to the console<br>
(3) the Kickstart script defaults to the 'America/Chicago' time zone, which you can edit or provisioner-override

That's it! Tweak away. As-is, it only adds necessary packages for Vagrant, VirtualBox, and Puppet/Chef.

Notes: 64-bit VM, 512MB of RAM, 1GB of swap, LVM partitions, 'wheel' group, no SELinux, no firewall
