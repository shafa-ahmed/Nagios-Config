# Nagios-Config
Nagios formerly known as Nagios, is a free and open-source computer-software application that monitors systems, networks and infrastructure. Nagios offers monitoring and alerting services for servers, switches, applications and services. It alerts users when things go wrong and alerts them a second time when the problem has been resolved.

#installing the required Packages
yum install php
yum install httpd
yum install gcc glibc glibc-common
yum install gd gd-devel

#Add users, group and make a directory
useradd -m nagios
passwd nagios
groupadd nagioscmd
usermod -a -G nagioscmd nagios
usermod -a -G nagioscmd apache
mkdir ~/downloads
cd ~/downloads

#install Packages and pluggins
wget http://prdownloads.sourceforge.net/sourceforge/nagios/nagios-4.4.6.tar.gz
wget http://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz

#Extract the packages and configure it
tar zxvf nagios-4.4.6.tar.gz
cd nagios-4.4.6
./configure --with-command-group=nagioscmd

#Compilation of Packages
make all
make install
make install-init
make install-config
make install-commandmode


make install-webconf

#Creating user and password for the Nagios Console
htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin

systemctl restart httpd
systemctl restart httpd.service

#Extract the pluggins, configure it and also compilation of Pluggins
tar zxvf nagios-plugins-2.3.3.tar.gz
cd nagios-plugins-2.3.3
./configure --with-nagios-user=nagios --with-nagios-group=nagios
make
make install


#To make nagios on
chkconfig nagios on

#To check, everything goes good or not(FINAL STAGE)
/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg


systemctl restart nagios
systemctl enable nagios
systemctl status  nagios
systemctl restart httpd
systemctl enable httpd
systemctl status httpd

