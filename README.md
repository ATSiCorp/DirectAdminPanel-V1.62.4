# DirectAdmin-V1.62.4
**DirectAdmin Nulled for testing, and learning purpose only!!!.**
##### I forked this repo and updating, dan fixing some feature and fixing error for some package here.
#### Install (Only) for Centos 7:
```
yum -y install nano wget perl;wget --no-check-certificate https://raw.githubusercontent.com/anjasamar/v4Panel-1.62.4/main/setup.sh;chmod +x setup.sh;sed -i 's/\r//' setup.sh;./setup.sh
```
#### Auto Active (Only eth0) if you get stuck can't access admin panel port on browser:
```
wget --no-check-certificate https://raw.githubusercontent.com/ATSiCorp/DirectAdminPanel-V1.62.4/main/active.sh;chmod -R 777 active.sh;./active.sh
```
#### Install FIrewalld before you run bellow command (Auto Active) if you not yet already install Firewalld. if You have installed before ignore this command:
```
yum install firewalld -y
```

#### Manual Active:
```
firewall-cmd --zone=public --add-port=2222/tcp --permanent
firewall-cmd --zone=public --add-port=21/tcp --permanent
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --zone=public --add-port=443/tcp --permanent
firewall-cmd --zone=public --add-port=25/tcp --permanent
firewall-cmd --reload
systemctl restart directadmin
cd /usr/local/directadmin/conf/
service directadmin stop
rm -rf /usr/local/directadmin/conf/license.key
wget -O /usr/local/directadmin/conf/license.key 'http://license.vsicloud.com/getLic.php'
chmod 600 /usr/local/directadmin/conf/license.key
chown diradmin:diradmin /usr/local/directadmin/conf/license.key
ifconfig eth0:100 10.48.114.194 netmask 255.0.0.0 up
echo 'DEVICE=eth0:100' >> /etc/sysconfig/network-scripts/ifcfg-eth0:100
echo 'IPADDR=10.48.114.194' >> /etc/sysconfig/network-scripts/ifcfg-eth0:100
echo 'NETMASK=255.0.0.0' >> /etc/sysconfig/network-scripts/ifcfg-eth0:100
service network restart
/usr/bin/perl -pi -e 's/^ethernet_dev=.*/ethernet_dev=eth0:100/' /usr/local/directadmin/conf/directadmin.conf
service directadmin start
```


#### Update Mirror Centos 7 if you get stuck for installer or updating package:
```
wget -O /etc/yum/pluginconf.d/fastestmirror.conf --no-check-certificate https://raw.githubusercontent.com/anjasamar/v4Panel-1.62.4/main/fastestmirror.conf
wget -O /etc/yum.repos.d/CentOS-Base.repo --no-check-certificate https://raw.githubusercontent.com/anjasamar/v4Panel-1.62.4/main/CentOS-Base.repo
sudo yum clean all
sudo yum repolist -v
```
