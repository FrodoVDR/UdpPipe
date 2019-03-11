# UdpPipe
A UDP Traffic Routing Utility

UdpPipe needs more packages than Python 2.7. We show what to install using the example
of a Raspberry Pi installation with Debian Jessie (Raspbian). First the package python-dev
has to be installed to get the necessary Python extensions later:

```sudo apt-get install python-dev python-pip openssl git```

Simply ignore apt-get's comment if the other packages are already on board.
Once apt-get has run through, use pip to add two Python packages:

```pip install daemon-runner pycrypto```

If UdpPipe is to forward privileged ports (< 1024), it must run on head under the root account.
Otherwise, a normal user account is the safer option. 

There are matching systemd scripts in the systemd folder.
The udppipe-server.service script is for the head service on the home server.
udppipe-client.service is for the tail computer on the internet.

In the sample folder you will find examples of the head or tail configuration which must be copied to /etc.

Next step clone this git:

```cd /usr/local
git clone "this git"```

On the server at home:

cp /usr/local/UdpPipe/sample/server/udppipe.ini /etc

On the client on the internet:

cp /usr/local/UdpPipe/sample/client/udppipe.ini /etc

Change the ini files to the setting you need.

Next install the systemd services:

At home:

ln /usr/local/UdpPipe/systemd/udppipe-server.service /etc/systemd/system/udppipe-server.service

systemctl enable udppipe-server.service

systemctl start udppipe-server.service

On the Internet:

ln /usr/local/UdpPipe/systemd/udppipe-client.service /etc/systemd/system/udppipe-client.service 

systemctl enable udppipe-client.service

systemctl start udppipe-client.service

You can find more information at
- c't 6/2018, S. 152: <https://www.heise.de/ct/ausgabe/2018-6-Per-UDP-ins-Heimnetz-trotz-CG-NAT-und-DS-Lite-3976627.html>
- UdpPipe-Source, udptunnel: http://ct.de/ydk1

Last but not least many thanks to https://github.com/liebrandapps/UdpPipe, unfortunately his website on this topic is no longer available.
