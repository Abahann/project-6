## Step 1:Preparing a Web Server

`Command: lsblk to inspect block devices that are associated to the  Server and viewing of the newly configured partition on the 3 disks`
![lsblk status](./images/lsbk%20status.png)
`sudo pvcreate`
![pvs status](./images/pvs%20status.png)
`sudo vgcreate`
![vgs status](./images/vgs%20status.png)
`sudo lvcreate`
![lvs status](./images/lvs%20status.png)
`sudo lsblk:  to verify the entire setup`
`sudo mkfs.ext4 /dev/vg-webdata/apps-lv`
![mkfs.ext4 status](./images/mkfs.ext4%20status.png)
`sudo mkfs.ext4 /dev/vg-webdata/logs-lv`
![mkfs.ext4 logs-lv status](./images/mfst.ext4%20logs-lv%20status.png)
`sudo mount /dev/vg-webdata/apps-lv /var/www/html/:to mount /var/ww/html on apps-lv logical volume`
![mount apps-lv status](./images/mount%20app-lv%20status.png)

## Step 2:Preparing the Database Server
`Commands:lsblk

sudo gdisk /dev/xvdf /dev/xvdg /dev/xvdh

sudo yum install lvm2 -p

sudo mount /dev/vg-database/db-lv /db

sudo blkid

sudo mount -a

sudo sytemctl daemon-reload
`
![step2 status](./images/step2%20status.png)

## Step 3: Installing of Word Press on Web Server EC2
`Commands:
sudo yum -y update(Update the repository)

sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json (Install wget, Apache and it’s dependencies)

sudo systemctl enable httpd(Start Apache)

sudo systemctl start httpd

sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm (To install PHP and it’s depemdencies)

sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm

sudo yum module list php

sudo yum module reset php

sudo yum module enable php:remi-7.4

sudo yum install php php-opcache php-gd php-curl php-mysqlnd

sudo systemctl start php-fpm

sudo systemctl enable php-fpm

sudo setsebool -P httpd_execmem 1

sudo systemctl restart httpd (Restart Apache)
`
![httpd status](./images/httpd%20status.png)

`Commands: to Download wordpress and copy wordpress to /var/www/html
  
  mkdir wordpress
  
  cd   wordpress

   sudo wget http://wordpress.org/latest.tar.gz

  sudo tar xzvf latest.tar.gz

  sudo rm -rf latest.tar.gz

  cp wordpress/wp-config-sample.php wordpress/wp-config.php

  cp -R wordpress /var/www/html/
`
## Step 4: Install MySQL on your DB Server EC2

`sudo yum update`
`sudo yum install mysql-server`
`sudo systemctl status (Verify that the service is up and running)`

## Step 5:Configure DB to work with WordPress

`Commands:

sudo mysql

CREATE DATABASE wordpress;

CREATE USER `myuser`@`<Web-Server-Private-IP-Address>` IDENTIFIED BY 'mypass';

GRANT ALL ON wordpress.* TO 'myuser'@'<Web-Server-Private-IP-Address>';

FLUSH PRIVILEGES;

SHOW DATABASES;

exit
`
![db status](./images/db%20status.png)

## Step 6:Configure WordPress to connect to remote database.

`Commands : sudo yum install mysql`
`sudo mysql -u admin -p -h <DB-Server-Private-IP-address>`
 Verify if you can successfully execute SHOW DATABASES; command and see a list of existing databases.

Change permissions and configuration so Apache could use WordPress:

Enable TCP port 80 in Inbound Rules configuration for your Web Server EC2 (enable from everywhere 0.0.0.0/0 or from your workstation’s IP)

Try and access  from the browser the link to your Wordpress
![wordpress status](./images/wordpress%20status.png)












