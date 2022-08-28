# Nagios-Config
Nagios formerly known as Nagios, is a free and open-source computer-software application that monitors systems, networks and infrastructure. Nagios offers monitoring and alerting services for servers, switches, applications and services. It alerts users when things go wrong and alerts them a second time when the problem has been resolved.

#installing the required Packages
yum install php
yum install httpd
yum install gcc glibc glibc-common
yum install gd gd-devel

#Add user and group and make a directory
useradd -m nagios
passwd nagios
groupadd nagioscmd
usermod -a -G nagioscmd nagios
usermod -a -G nagioscmd apache
mkdir ~/downloads
cd ~/downloads

#install pluggins
wget http://prdownloads.sourceforge.net/sourceforge/nagios/nagios-4.4.6.tar.gz
wget http://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz
