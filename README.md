# [Thrive](https://www.thrivebureau.com "Thrive ERP's Homepage") Install Script

Thrive Bureau ERP Installation Instruction v17

open ports:
8068 - App
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
sudo wget https://raw.githubusercontent.com/u16052642/thrive_erp_install_script17/divinlonji_thrive_ent1768/thrive1768_install.sh

** sudo wget https://raw.githubusercontent.com/u16052642/thrive_erp_install_script17/master/thrive1768_install.sh


step 2)
sudo chmod +x thrive1768_install.sh

step 3)
sudo ./thrive1768_install.sh

Step 4)
1. wkhtmltopdf -V
2. sudo apt-get remove --purge wkhtmltopdf
3. wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2_amd64.deb
4. sudo dpkg -i libssl1.1_1.1.1f-1ubuntu2_amd64.deb
5. wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.focal_amd64.deb
6. sudo apt install ./wkhtmltox_0.12.5-1.focal_amd64.deb

Step 5)
after finishing installation you will see the (your vps ip):8068 then you should provide the master password then use database name and user id and password

Step 6)
vi /etc/thrive1768-server.conf

addons: /thrive1768/thrive1768-server/thrive/addons,/thrive1768/custom/addons,

/thrive1768/custom/addons/thrive_addons_17,/thrive1768/custom/addons/thrive_addons_17/finance,/thrive1768/custom/addons/thrive_addons_17/hr,/thrive1768/custom/addons/thrive_addons_17/inventory_mrp,/thrive1768/custom/addons/thrive_addons_17/marketing,/thrive1768/custom/addons/thrive_addons_17/miscellaneous,/thrive1768/custom/addons/thrive_addons_17/productivity,/thrive1768/custom/addons/thrive_addons_17/fleet,/thrive1768/custom/addons/thrive_addons_17/sales,/thrive1768/custom/addons/thrive_addons_17/services,/thrive1768/custom/addons/thrive_addons_17/website,/thrive1768/custom/addons/thrive_addons_17/POS,/thrive1768/custom/addons/thrive_addons_17/reporting,/thrive1768/custom/addons/thrive_addons_17/purchase,/thrive1768/custom/addons/thrive_addons_17/crm,/thrive1768/custom/addons/thrive_addons_17/events,/thrive1768/custom/addons/thrive_addons_17/industry,/thrive1768/custom/addons/thrive_addons_17/security_companies/security_payroll_addons_v17,/thrive1768/custom/addons/thrive_addons_17/themes,/thrive1768/custom/addons/thrive_addons_17/project,/thrive1768/custom/addons/thrive_addons_17/construction,/thrive1768/custom/addons/thrive_addons_17/admin_settings


then upload the extra modules within these custom directories above.

when need manually start restart or stop then use this command:

sudo /etc/init.d/thrive1768-server restart
sudo /etc/init.d/thrive1768-server stop
sudo /etc/init.d/thrive1768-server start
sudo /etc/init.d/thrive1768-server force-reload

log file:
tail -400f /var/log/thrive1768/thrive1768-server.log

Start Eagle service: sudo service thrive1768-server start
Stop Eagle service: sudo service thrive1768-server stop
Restart Eagle service: sudo service thrive1768-server restart


python addons: 
sudo apt install python3-pandas -y
sudo apt install python3-geopy -y
sudo apt install python3-cachetools -y
pip3 install phonenumbers
pip3 install pdfminer.six

log file:
tail -400f /var/log/thrive1768/thrive1768-server.log

========================================================================================================================================================

**** PostressSQL user and Password change**********
1. 
sudo su postgres
psql

2.
to list all users
\du

3.modify user password
ALTER USER thrive1768  WITH PASSWORD 'Blank@2022';

========================================================================================================================================================

***Database Backup setup***

1. install the following:
pip install dropbox
pip install pyncclient
pip install nextcloud-api-wrapper
pip install boto3
pip install paramiko

2. Create backup Directory on local:
mkdir /opt/thrive_backup
chmod 777 /opt/thrive_backup

3. Restart services
sudo /etc/init.d/thrive1768-server stop
sudo /etc/init.d/thrive1768-server start

4. login to portal and activate the plugin in app center

5. secttings -> Technical (only on debug mode) -> Automatic DB backup -> Backup Config -> Create

6. secttings -> Technical (only on debug mode) -> Automation-> Scheduled Actions (to config scheduled backup) -> Backup : Automatic Database Backup



==================================================================================================================================================================================================================================================================================================================

*Uninstall Thrive*

* Stop Server
* Remove all Thrive files
* Remove postgresql from system

1. STOP SERVER
  sudo /etc/init.d/thrive1768-server stop
2. REMOVE ALL Thrive FILES (main home directory)
  sudo rm -Rf thrive1768
3. REMOVE CONFIG FILES
  sudo rm -rf /etc/thrive1768.conf
  sudo rm -rf /etc/thrive1768/thrive1768.conf (if any)
  sudo rm -rf /etc/thrive1768-server.conf (if any)
  sudo update-rc.d -f thrive1768 remove 
  sudo update-rc.d -f thrive1768-server remove (if thrive1768-server instead of thrive1768)
  sudo rm -f /etc/init.d/thrive1768 (or thrive1768-server)
4. REMOVE USER AND USER GROUP (htop)
  sudo userdel -r postgres
  sudo groupdel postgres
5. REMOVE DATABASE
  sudo apt-get remove postgresql -y
  sudo apt-get --purge remove postgresql\* -y
  sudo rm -rf /etc/postgresql/
  sudo rm -rf /etc/postgresql-common/
  sudo rm -rf /var/lib/postgresql/


==================================================================================================================================================================================================================================================================================================================


*SSL Cert & Domain settings*

create DNS record with domian providers and link it to IP. create "A record" for both www.example.com and example.com

1. 
sudo apt-get update -y
sudo apt-get install nginx -y

2. 
sudo service nginx start
**sudo systemctl start nginx

3.
cd /etc/nginx/sites-enabled

4.
sudo rm default|sudo vi default

#### NB!! Delete what's in the current file
add the following config details below into the file
=======================================
#thrive server
upstream thrive {
server 127.0.0.1:8068;
}
upstream thrivechat {
server 127.0.0.1:8074;
}

#edit servername
server {
listen 80;
server_name DNS/Domain name (e.g erp.thrive.com www.erp.thrive.com crm.matupunuka.co.za);

proxy_read_timeout 720s;
proxy_connect_timeout 720s;
proxy_send_timeout 720s;


# Add Headers for thrive proxy mode
proxy_set_header X-Forwarded-Host $host;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;
proxy_set_header X-Real-IP $remote_addr;

# log
access_log /var/log/nginx/thrive.access.log;
error_log /var/log/nginx/thrive.error.log;

# Redirect requests to thrive backend server
location / {
proxy_redirect off;
proxy_pass http://thrive;
}

location /longpolling {
proxy_redirect off;
proxy_pass http://thrivechat;
}

# common gzip
gzip_types text/css text/less text/plain text/xml application/xml application/json application/javascript;
gzip on;


client_body_in_file_only clean;
client_body_buffer_size 32K;
client_max_body_size 500M;
sendfile on;
send_timeout 600s;
keepalive_timeout 300;
}

==========================================

5. test nginx config:
sudo nginx -t

6.
sudo rm /etc/nginx/sites-available/default
sudo ln -s  /etc/nginx/sites-enabled/default /etc/nginx/sites-available/default

7.
vi /etc/thrive1768-server.conf
paste below code:

proxy_mode=True
xmlrpc_interface = 127.0.0.1


8.
sudo /etc/init.d/thrive1768-server stop
sudo /etc/init.d/thrive1768-server start

9. 
sudo systemctl stop nginx
sudo systemctl start nginx
sudo systemctl reload nginx


*****INSTALL SSL*****

sudo apt install certbot python3-certbot-nginx -y

sudo systemctl reload nginx

sudo ufw allow "Nginx Full"
sudo ufw delete allow "Nginx HTTP"

sudo certbot --nginx -d example.com -d www.example.com

Follow the steps:
email: support@thrivebureau.com

Y

N

*Wait for a bit: after seeing 2 SUCCESSFULLY DEPLOYED CERTIFICATE messages then you are done

***if any failure, try installing again by running:
  certbot install --cert-name eg.thrivebureau.com






