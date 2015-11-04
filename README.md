Zimbra ownCloud Zimlet
==========

If you find Zimbra ownCloud Zimlet useful and want to support its continued development, you can make donations via:
- PayPal: info@barrydegraaff.tk
- Bank transfer: IBAN NL55ABNA0623226413 ; BIC ABNANL2A

Demo video: https://www.youtube.com/watch?v=gfVLE22kJ6o

User manual : http://barrydegraaff.github.io/owncloud/

Integrating ownCloud in Zimbra Collaboration Suite, currently tested on:
- Windows: Internet Explorer 11, Microsoft Edge, Google Chrome, Firefox
- Linux: Google Chrome, Firefox

This Zimlet is designed for Zimbra version 8.6.

This Zimlet is not available for use in Zimbra Desktop.

Bugs and feedback: https://github.com/barrydegraaff/owncloud-zimlet/issues

========================================================================

### Install prerequisites
  - A running Zimbra server with Zimbra Proxy
  - A running ownCloud server

### Build the ownCloud Extension and Zimlet
The recommended method is to build from sources.

    [user@host ~]$ yum install -y git ant                                      # On RedHat/Fedora/CentOS
    [user@host ~]$ apt-get -y install git ant                                  # On Debian/Ubuntu
    [user@host ~]$ cd ~
    [user@host ~]$ rm owncloud-zimlet -Rf
    [user@host ~]$ git clone https://github.com/barrydegraaff/owncloud-zimlet
    [user@host ~]$ cd owncloud-zimlet
    [user@host owncloud-zimlet]$ git checkout 0.2.0
    [user@host owncloud-zimlet]$ cd extension && ant download-libs && cd ..    # Optional: you can download the libraries manually
    [user@host owncloud-zimlet]$ make

You should find the package file `owncloud-extension.tar.gz` ready to be deployed, send it to your server.

### Install the ownCloud Extension and Zimlet
Copy the package file `owncloud-extension.tar.gz` into `/tmp/`:

    [user@host owncloud-zimlet]$ scp owncloud-extension.tar.gz root@server:/tmp/owncloud-extension.tar.gz
    
Start the installer:
    
    [root@server tmp]# sudo -u zimbra tar -xzf /tmp/owncloud-extension.tar.gz -C /tmp/
    [root@server tmp]# cd /tmp/owncloud-extension && sudo ./install
     
Restart your mailbox to let the extension to be loaded:

	[zimbra@server zimbra]$ zmmailboxdctl restart

### Do you backup using zmmailbox tgz? Please be advised of proxy problems

I am sorry to inform you that exporting tgz files is considered broken by Zimbra: [https://bugzilla.zimbra.com/show_bug.cgi?id=101760](https://bugzilla.zimbra.com/show_bug.cgi?id=101760). 
Installing the proxy may break the tgz export feature a bit more, it is advised you bypass the proxy when using zmmailbox. Please see: [https://bugzilla.zimbra.com/show_bug.cgi?id=101760#c11](https://bugzilla.zimbra.com/show_bug.cgi?id=101760#c11)

========================================================================

### Contributors

* Michele Olivo [ZeXtras](https://www.zextras.com/)

### License

Copyright (C) 2015  Barry de Graaff

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see http://www.gnu.org/licenses/.
