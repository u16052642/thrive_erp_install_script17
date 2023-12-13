# [Thrive](https://www.thrivebureau.com "Thrive ERP's Homepage") Install Script

Thrive Bureau ERP Installation Instruction

open ports:
8069 -App
8074 - logs

How to calculate RAM size needed:
RAM size (in GB) = (number of users/10) + (size of the database/10GB) For example, if you have 50 users and a database size of 100GB, the estimated RAM size required would be: RAM size = (50/10) + (100/10) = 5 + 10 = 15 GB

=====================================

For installation in VPS server use these three lines, in the end of the installation process, when asking for GitHub user id: then input your GitHub email then input your password, it will install thrive_bureau_erp.

login to vps terminal then insert three lines then it will start automatically start the installation process

sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt -y install net-tools vim screen curl tcpdump sysstat wget telnet bmon htop mlocate

step 1)
sudo wget https://raw.githubusercontent.com/u16052642/thrive_erp_install_script17/master/thrive1768_install.sh

step 2)
sudo chmod +x thrive1768_install.sh

step 3)
sudo ./thrive1768_install.sh


after finishing installation you will see the (your vps ip):8069 then you should provide the master password then use database name and user id and password


vi /etc/thrive1768-server.conf
addons: /thrive1768/thrive1768-server/thrive/addons,/thrive1768/custom/addons,

/thrive1768/custom/addons/new/finance,/thrive1768/custom/addons/new/hr,/thrive1768/custom/addons/new/inventory_mrp,/thrive1768/custom/addons/new/marketing,/thrive1768/custom/addons/new/miscellaneous,/thrive1768/custom/addons/new/productivity,/thrive1768/custom/addons/new/reporting,/thrive1768/custom/addons/new/sales,/thrive1768/custom/addons/new/services,/thrive1768/custom/addons/new/website,/thrive1768/custom/addons/thrive_addons_16


then upload the extra modules within these custom directories above.

when need manually start restart or stop then use this command:

sudo /etc/init.d/thrive1768-server restart
sudo /etc/init.d/thrive1768-server stop
sudo /etc/init.d/thrive1768-server start
sudo /etc/init.d/thrive1768-server force-reload

Start Eagle service: sudo service thrive1768-server start
Stop Eagle service: sudo service thrive1768-server stop
Restart Eagle service: sudo service thrive1768-server restart


python addons: 
sudo apt install python3-pandas -y
sudo apt install python3-geopy -y
sudo apt install python3-cachetools -y
pip3 install pdfminer.six


log file:
tail -400f /var/log/thrive1768/thrive1768-server.log

##### 1. Download the script:
sudo wget https://raw.githubusercontent.com/u16052642/thrive_erp_install_script17/divinlonji_thrive_ent1768/thrive1768_install.sh

sudo chmod +x thrive1768_install.sh

sudo ./thrive1768_install.sh



