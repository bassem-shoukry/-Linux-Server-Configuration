# Linux Server Configuration Project - Udacity  Full Stack ND

#### DESCRIPTION
An Udacity Full Stack Web Developer III Nanodegree Project.

### Server Set up
1. Login into Amazon [Lightsail]('https://lightsail.aws.amazon.com') or Create new amazon web service account if you don't have one.
2.Create new instance ```OS Only```
3. Once your server has booted up login ssh using `ssh -i path\to\the\key\LightsailDefaultKey-eu-central-1.pem ubuntu@35.156.227.109`.
### Server Information
* Server IP Address: 35.156.227.109
* SSH server access port: 2200
* SSH login username: grader
* Application URL: http://catalog-udacity.com

#### Server Configuration Changes
1. Login ssh to server : `ssh -i grader grader@35.156.227.109 -p 2200`.
2. Update all currently installed packages. : `sudo apt-get update && sudo apt-get upgrade`.
3. Change ssh port to 2200 : `sudo nano /etc/ssh/sshd_config`.
    * then search for port and change value to 2220 instead of 22.
4.  Create grader user ```sudo adduser grader``` and enter your password.
5. add user to sudoers by create new file inside ``/etc/sudoers.d `` and add the following line `grader ALL=(ALL) NOPASSWD:ALL` and save file.

4. Firewall Setup and Configuration
* Setup Firewall with UFW : `sudo apt-get install ufw`
* disable default incoming ports : `sudo ufw default deny incoming`
* allow default outgoing ports : `sudo ufw default allow outgoing`
* then allow ports only we need : `sudo ufw allow 80/tcp` & `sudo ufw allow 123/tcp` &`sudo ufw allow 2200/tcp`

#### Software Installed
* Python3 :
`sudo apt-get install python3`
* python3-pip :
`sudo apt-get install python3-pip`

#### Apache Configuration
* Install Apache2 and libapache2-mod-wsgi-py3 : `sudo apt-get install apache2 libapache2-mod-wsgi-py3`
* Enable mod_wsgi using: `sudo a2enmod wsgi`
*  Set up a virtual host
    * Add this the following line : `WSGIPythonPath /var/www/catalog/catalog/venv3/lib/python3.6/site-packages` in  `/etc/apache2/mods-enabled/wsgi.conf` file
    * Create `/etc/apache2/sites-available/catalog.conf` file and add the following lines :
        ``` 
        <VirtualHost *:80>
             ServerName 13.59.39.163
           ServerAlias catalog-udacity.com
             WSGIScriptAlias / /var/www/catalog/catalog.wsgi
             <Directory /var/www/catalog/catalog/>
                 Order allow,deny
                   Allow from all
             </Directory>
             Alias /static /var/www/catalog/catalog/static
             <Directory /var/www/catalog/catalog/static/>
                   Order allow,deny
                   Allow from all
             </Directory>
             ErrorLog ${APACHE_LOG_DIR}/error.log
             LogLevel warn
             CustomLog ${APACHE_LOG_DIR}/access.log combined
         </VirtualHost>
        ```
    * Enable the new virtual host: `sudo a2ensite FlaskApp.conf.
    * Disable default virtual host : `sudo a2dissite 000-default.conf`.
    * Restart Apache: `sudo service apache2 restart`.
#### Database set up and configuration
* Install PostgreSQL :`sudo apt-get install postgresql postgresql-contrib`.
* Switch to postgres user : `sudo su - postgres`.
* Open PostgreSQL Terminal : `psql`.
* Create catalog user : `CREATE ROLE catalog WITH LOGIN PASSWORD 'catalog';`
* Add create database role to catalog user : `ALTER ROLE catalog CREATEDB;`
* create ubuntu user called `catalog` : `sudo adduser catalog` and enter your password
* Give to catalog user the permission to sudo by add the following line to `/etc/sudoers.d/grader` file `catalog  ALL=(ALL:ALL) ALL`

#### Set up Virtual Environment
* sudo apt-get install python3-venv
* python3 -m venv env
* source ./env/bin/activate
#### Dependencies Installed
* Flask : `pip3 install Flask`
* Requests : `pip3 install requests`
* Psycopg2 : `sudo apt-get install python3-psycopg2`
* Sqlalchemy : `pip3 install SQLAlchemy`
* oauth2client : `pip3 install --upgrade oauth2client`
* httplib2 ` :  pip3 install httplib2`
* Libpq-dev ` : sudo apt-get install ibpq-dev`

#### Server Setup II
  * after change ssh port from 22 to 2200 go to  amazon lightsail account then go to the instance and choose from the dropdown menu Manage 
  * choose Networking tab and click edit rules from firewall section 
  * add another select  custom  TCP  and port will be 2200 then save and delete ssh port
  * add NTB port add another select  custom  TCP  and port will be 123 then save
     
