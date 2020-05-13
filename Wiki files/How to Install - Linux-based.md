# How to install - Linux-based

This document should help you install the whole DRP-Framework inside a Linux-based environment. For this tutorial, I am using a VPS with Debian 10 installed from OVH, but it should work with any other Linux distribution/VPS.

## Content

- [Prerequisites](https://github.com/OfficialDarkzy/DRP-Core/wiki/How-to-install---Linux#prerequisites)
    - Update your server
    - Install XAMPP
    - Install Node.js and NPM
    - Install Screen
- [Install DRP-Framework](https://github.com/OfficialDarkzy/DRP-Core/wiki/How-to-install---Linux#install-drp-framework)
    - Install DRP-Core scripts
    - Install DRP-ID scripts
    - ExternalSQL configuration
    - Start your server

## Prerequisites

We will assume the following:
> You are using an admin connexion (understand an account which is either root or with sudo privileges).
> You already have installed a fresh FiveM FXServer without any other scripts (for the moment).

**1. Update your server**

Connect to your VPS with your account, and update the package list and the packages by typing the following commands:

    apt-get update
    apt-get upgrade

**2. Install XAMPP**

> You can use any other AMP (such as MAMP) softwares or even install MySQL and PHPmyAdmin by yourself. But to ease the process we will use XAMPP.

**Download the files**

Go to [https://www.apachefriends.org/download.html](https://www.apachefriends.org/download.html)
From the website choose the file you want (choose the Linux distribution, for me, it was version 7.4.3), **right-click** on the download button and choose **copy the link address**. Next in your console type `wget` followed by the link you just copied, you should have something like this (*the **X** are just representing the number of the version*):

`wget https://www.apachefriends.org/xampp-files/X.X.X/xampp-linux-x64-X.X.X-X-installer.run`

**Modify the authorisation**

Needed to launch the installation file:

`sudo chmod +x xampp-linux-x64-X.X.X-X-installer.run`

**Launch the installation**
 
`sudo ./xampp-linux-x64-X.X.X-X-installer.run`

During the installation, you will be asked if you need the Developer files, type **Y** and press **Enter**, now follow the instructions of the program.

**Start XAMPP**

`sudo /opt/lampp/lampp start`

You should be able to access the XAMPP dashboard now via the following link (just change the *X* with whatever is your IP address):
> http://xxx.xx.xx.xx/dashboard

If you try to access the **PHPmyAdmin**, a webpage should appear and tell you that you cannot access the server because it is only available on the **Localhost**, you can easily fix that:
With any FTP solution (like [FileZila](https://filezilla-project.org/)) you possess go to the following folder `/opt/lampp/etc/extra/` and open the file `http-xampp.conf`. There change the following:

    # since XAMPP 1.4.3
    <Directory "/opt/lampp/phpmyadmin">
        AllowOverride AuthConfig Limit
        Require local
        ErrorDocument 403 /error/XAMPP_FORBIDDEN.html.var
    </Directory>

With:

    # since XAMPP 1.4.3
    <Directory "/opt/lampp/phpmyadmin">
        AllowOverride AuthConfig Limit
        Order deny,allow
        Allow from all
        Require all granted
        # If you only want to allow some connexion you can use Deny from all and Allow from TheIpAdressYouWantToAllow
        ErrorDocument 403 /error/XAMPP_FORBIDDEN.html.var
    </Directory>

Restart XAMPP:

`sudo /opt/lampp/lampp restart`

**Change default security settings ~ RECOMMENDED**

By typing the following inside the console it will help you create a password for the current MySQL connection. Do not forget to write them done.

`sudo /opt/lampp/lampp security`

**3. Install Node.js and NPM**

You are required to add [Node.js PPA](https://nodejs.org/en/) to your system provided by the Nodejs official website. You can choose to either install the latest Node.js version or the long term support (LTS) version.
Latest:

    sudo apt-get install curl software-properties-common
    curl -sL https://deb.nodesource.com/setup_13.x | sudo bash -

LTS:

    sudo apt-get install curl software-properties-common
    curl -sL https://deb.nodesource.com/setup_12.x | sudo bash -

**Install the package**

NPM should be installed at the same time:

`sudo apt-get install nodejs`

**Check the version**

You should have an output like: `vXX.XX.XX`

    nod -v
    npm -v

**4. Install Screen**

This will be very useful for when you launch the server and you want to keep it open when you disconnect from your VPS.
You can found more information on their website: [https://linuxize.com/post/how-to-use-linux-screen/](https://linuxize.com/post/how-to-use-linux-screen/)
Just install the package:

`apt-get install screen`

## Install DRP-Framework

> If you do not wish to follow this step by step guide you can always check the README file there: [https://github.com/OfficialDarkzy/DRP-Core/blob/master/README.md](https://github.com/OfficialDarkzy/DRP-Core/blob/master/README.md)

**1. Install DRP-Core scripts**

**Get the scripts**

With FVM

    fvm install --save --folder=DRP OfficialDarkzy/DRP-Core

With Git

    cd resources
    git clone https://github.com/OfficialDarkzy/DRP-Core [DRP]

Manually

- Download [https://github.com/OfficialDarkzy/DRP-Core/archive/master.zip](https://github.com/OfficialDarkzy/DRP-Core/archive/master.zip)
- Unzip the folder
- Put all the folders in the resource/[DRP] directory

**Configuration**

- Import the **core.sql** to your database, either by using the import function from PHPmyAdmin or any other Database Tool of your choice.
- Change your **server.cfg** accordingly with all the resources you added in the previous step.

**2. Install DRP-ID scripts**

**Get the scripts**

With FVM

	fvm install --save --folder=DRP OfficialDarkzy/DRP-ID

With Git

	cd resources
	git clone https://github.com/OfficialDarkzy/DRP-ID [DRP]

Manually

- Download [https://github.com/OfficialDarkzy/DRP-ID/archive/master.zip](https://github.com/OfficialDarkzy/DRP-ID/archive/master.zip)
- Unzip the folder
- Put all the folders in the resource/[DRP] directory

**Configuration**

- Import all the table from the different resources (the **.sql** files) to your database, either by using the import function from PHPmyAdmin or any other Database Tool of your choice.
- Change your **server.cfg** accordingly with all the resources you added in the previous step. It should now look like this:

![server.cgf](https://i.ibb.co/Q95mt2P/server-cfg-3.png)

**3. ExternalSQL configuration**

Open the following file, with either nano or with your FTP and any NotePad app, the **config.json** in externalSQL folder.
Change the info inside following those instructions:    

**Instructions**
____
- **host**, keep it as "localhost"
- **port**, is the port the ExternalSQL will use to talk to your database, it needs an unused one (so not 3306 which is the one used by default by MySQL/MariaDB)
- **route**, is where the API folder is located, do not touch it unless you like boo-boo
- **secret**, is used to encrypt the talk between ExternalSQL and the Database, it needs to be changed to a random string 
- **community**, is the name of your community
____
- **connectionLimit**, is how much-simultaned connections are authorised, do not change it unless you know what you do
- **host**, is where the database is, so do not change it unless it is not on the same server
> /!\ If using ZAP-hosting you need to put the name of the server (go to Databases under Tools in the navigation panel), it should look like that `mysql-mariadb-X-XXX.zap-hosting.com`
- **port**, is the port used by MySQL (3306 by default)
- **user**, is the user used for the connexion to MySQL/MariaDB (ndlr the one you created) if you have not made a new one keep root
> /!\ If using ZAP-hosting you need to put the user given by ZAP (go to Databases under Tools in the navigation panel), it should look like that `zapXXXXXX-X`
- **password**, is the password of the previous **user**, only add one if you have a password on with this specific **user**
> /!\ If using ZAP-hosting you need to put the password given by ZAP (go to Databases under Tools in the navigation panel)
- **database**, is the name of the database where your data is, be sure it is the right name!
> /!\ If using ZAP-hosting you need to put the database name given by ZAP (go to Databases under Tools in the navigation panel), it should look like that `zapXXXXXX-X`
____
_Do not change those unless you know what you are doing_
- **devmodeactive**, if the developer mode needs to be activated
- **createtokenonstart**, if a token needs to be created
____

**config.json example**

	{
		"api": {
			"host": "localhost",
			"port": 2000,
			"route": "/external/api",
			"secret": "drpsecret",
			"community": "DRP"
		},
		"database": {
			"connectionLimit": 100,
			"host": "localhost",
			"port": 3306,
			"user": "root",
			"password": "",
			"database": "drp"
		},
		
		"devmodeactive": false,
		"createtokenonstart": true
	}

**4. Start your server**

Create a new screen session

`screen -S fxserver`

Go back to your server-data folder

`cd /home/WhateverIsYourPath/server-data`

Start normally your server

`bash /home/gta/run.sh +exec server.cfg`