----------------------------------------------------
Deployment Guide: Ubuntu 20.04.4
----------------------------------------------------

https://releases.ubuntu.com/20.04.4/?_ga=2.126533133.1693286580.1651167948-1268987514.1651167948

sudo apt-get update

sudo apt upgrade


-----------------------------------------
Node.js installation
-----------------------------------------

https://github.com/nodesource/distributions/blob/master/README.md

curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -

sudo apt update

sudo apt-get install -y nodejs

------------------------------------------
Download Frontend repo
------------------------------------------
git init

git pull https://github.com/Willie-Pretorius/ITEC_CRDB_NODEJS_FRONTEND.git [branch]

npm install.

node app.js

Test your website on {serverip}:3000

ctrl+c  to proceed.


-------------------------------------------------
MongoDB installation
-------------------------------------------------

https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/

wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -

If you dont see "OK" refer to the documentation on mongodb.com.

echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list

sudo apt update.

sudo apt-get install -y mongodb-org

Once installation completes.

sudo systemctl start mongod

Test to make sure frontend can do query.



mongoDB service commands:

sudo systemctl start mongod

sudo systemctl enable mongod

sudo systemctl stop mongod

sudo systemctl restart mongod

sudo systemctl status mongod

mkdir CRDB

git clone


-------------------------------------------
Download backend Repo.
-------------------------------------------
git init

git pull https://github.com/Willie-Pretorius/ITEC_CRDB_Python_Script.git [branch]

sudo apt-get install pymongo


python3 main.py

setup ftp server details.


-----------------------------------------------------------------
Schedule routine python script.
-----------------------------------------------------------------

date --set="2 OCT 2006 18:00:00"

timedatectl set-timezone Africa/Johannesburg

crontab -e

add the following text to schedule routing script to run at 5am everyday.

00 05 * * * cd apps/crdb-backend && python3 routine_start.py


------------------------------------------------
## installing pm2 webserver.
------------------------------------------------
sudo npm install -g pm2 

pm2 start app.js from frontend dir

pm2 startup

copy and paste ink provided to enable startup on boot.

pm2 commands:

pm2 status

pm2 start

pm2 restart

pm2 stop.

pm2 unstartup systemd



-----------------------------------------------------
ufw firewall setup
-----------------------------------------------------

## input firewall rules.

sudo ufw allow from 172.0.0.0/24 to any port 22 proto tcp

sudo ufw allow from 192.168.0.0/24 to any port 22 proto tcp

sudo ufw allow http

sudo ufw allow https

sudo ufw enable


---------------------------------------------------
nginx reverse proxy setup
---------------------------------------------------

sudo apt install nginx

sudo vim /etc/nginx/sites-available/default

server_name yourdomain.com www.yourdomain.com;

location / {

        proxy_pass http://localhost:3000;
        
        proxy_http_version 1.1;
        
        proxy_set_header Upgrade $http_upgrade;
        
        proxy_set_header Connection 'upgrade';
        
        proxy_set_header Host $host;
        
        proxy_cache_bypass $http_upgrade;
        
    }
   
check configuration

sudo nginx -t

sudo service nginx restart

sudo nginx status


-----------------------------------------
update process
------------------------------------------

git stash

git fetch url [branch]

git pull url [branch] 


