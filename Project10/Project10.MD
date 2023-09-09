Preparing the NFS server
-------------------------
lsblk

sudo gdisk /dev/xvdf
sudo gdisk /dev/xvdg
sudo gdisk /dev/xvdh

lsblk

sudo yum install lvm2
sudo lvmdiskscan

sudo pvcreate /dev/xvdf1
sudo pvcreate /dev/xvdg1
sudo pvcreate /dev/xvdh1

sudo pvs

sudo vgcreate webdata-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1

sudo vgs

sudo lvcreate -n lv-opt -L 14G webdata-vg
sudo lvcreate -n lv-apps -L 14G webdata-vg
sudo lvcreate -n lv-logs -L 14G webdata-vg

sudo lvs

sudo vgdisplay -v
sudo lsblk

sudo mkfs -t xfs /dev/webdata-vg/lv-opt
sudo mkfs -t xfs /dev/webdata-vg/lv-apps
sudo mkfs -t xfs /dev/webdata-vg/lv-logs


sudo mkdir -p /mnt/apps

sudo mkdir -p /mnt/logs

sudo mkdir -p /mnt/opt

sudo mount /dev/webdata-vg/lv-apps /mnt/apps

sudo mount /dev/webdata-vg/lv-logs /mnt/log

sudo mount /dev/webdata-vg/lv-opt /mnt/opt

==========================================

/etc/httpd/conf/httpd.conf - log folder for appache2
======================================
stop here
===================

sudo blkid

sudo vi /etc/fstab

sudo mount -a
sudo systemctl daemon-reload
=======================
sudo mysql
CREATE DATABASE tooling;
CREATE USER `webaccess`@`<Web-Server-Private-IP-Address>` IDENTIFIED BY 'mypass';
GRANT ALL ON tooling.* TO 'webaccess'@'<Web-Server-Private-IP-Address>';
FLUSH PRIVILEGES;
SHOW DATABASES;
exit

=================
journalctl -xe
setenforce 0