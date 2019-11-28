# Linux Server Configuration Project - Udacity  Full Stack ND

#### DESCRIPTION
An Udacity Full Stack Web Developer III Nanodegree Project.
### Server Information
* Server IP Address: 35.156.227.109
* SSH server access port: 2200
* SSH login username: grader
* Application URL: http://catalog-udacity.com

#### Server Configuration Changes
1. Login ssh to server
<br>
`ssh -i grader grader@35.156.227.109 -p 2200`
2. Update all currently installed packages.
<br>
`sudo apt-get update && sudo apt-get upgrade`
3. Change ssh port to 2200
<br>
`sudo nano /etc/ssh/sshd_config` 
<br>
then search for port and change value to 2220 instead of 22


4. Firewall Setup and Configuration
* Setup Firewall with UFW
 <br>
 `sudo apt-get install ufw`
* disable default incoming ports 
<br>
`sudo ufw default deny incoming`
* allow default outgoing ports
<br>
 `sudo ufw default allow outgoing`
 <br>
* then allow ports only we need
<br>
`sudo ufw allow 80/tcp`
<br>
`sudo ufw allow 123/tcp`
<br>
`sudo ufw allow 2200/tcp`

#### Software Installed
* Apache2 :
`sudo apt-get install apache2 libapache2-mod-wsgi`
* PostgreSQL :
`sudo apt-get install postgresql postgresql-contrib`
* Python3 :
`sudo apt-get install python3`
* python3-pip
`sudo apt-get install python3-pip`
* virtual environment
`sudo virtualenv -p python3 venv3`

#### Dependencies Installed
* flask
* requests
* psycopg2
* sqlalchemy
* oauth2client
* httplib2
* libpq-dev
