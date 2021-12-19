#######

Prerequisites
1) aws account
2) PHP7.2 or later
3) httpd
4) lamp-mariadb10.2 or later

########
Technologies
1) ec2 instance
2) vpc 
3) sunet group
4) internet getway
5) MySQL

########
vpc
1) create a vpc(10.0.0.0/16) with one public subnet and two private     subnate
2) create internet getway and attach with vpc
3) set route table for public(10.0.0.0/24) and private          (10.0.1.0/24,10.0.2.0/24) subnet and provide path to public subnet      to internet (0.0.0.0/0)
4) create a security group allow port-3306 for mysql/aurora and         port-22 for ssh
######## 
Database
1) create a rds database, select mysql 
2) select user-name, server-name, password,vpc,subnet group
3) clic on create
########
AWS elastic compute cloud
1) launch ec2 with previous created vpc and public subnet ,enable        auto     assign ip
2) set privious created security group
3) access the ec2 through putty 

Install an Apache web server with PHP

$ sudo amazon-linux-extras install -y lamp-mariadb10.2php7.2 php7.2
$ sudo yum install -y httpd
$ sudo systemctl start httpd
$ sudo systemctl enable httpd
$ sudo usermod -a -G apache ec2-user
$ exit
$ sudo chown -R ec2-user:apache /var/www
$ sudo chmod 2775 /var/www
   find /var/www -type d -exec sudo chmod 2775 {} \;
$ find /var/www -type f -exec sudo chmod 0664 {} \;

Connect your Apache web server to your DB instance
$ cd /var/www
   mkdir inc
   cd inc
$ >dbinfo.inc
   nano dbinfo.inc

   <?php

define('DB_SERVER', 'db_instance_endpoint');
define('DB_USERNAME', 'tutorial_user');
define('DB_PASSWORD', 'master password');
define('DB_DATABASE', 'sample');

?>
$ cd /var/www/html
$ >SamplePage.php
   nano SamplePage.php
                
                


