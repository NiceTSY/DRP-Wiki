# How to install - Windows-based

This document should help you install the whole DRP-Framework inside a Windows-based environment. For this tutorial, I am using a local Windows 10 Home distribution.

## Content

- [Prerequisites](https://github.com/OfficialDarkzy/DRP-Core/wiki/How-to-install---Windows#prerequisites)
    - Install XAMPP
- [Install DRP-Framework](https://github.com/OfficialDarkzy/DRP-Core/wiki/How-to-install---Windows#install-drp-framework)
    - Install DRP-Core scripts
    - Install DRP-ID scripts
    - DatabaseAPI and externalSQL configuration
    - Start your server

## Prerequisites

We will assume the following:
> You are using an admin account.
> You already have installed a fresh FiveM FXServer without any other scripts (for the moment).

**1. Install XAMPP**

> You can use any other AMP (such as MAMP) software or even install MySQL and PHPmyAdmin by yourself. But to ease the process we will use XAMPP.

**Download the files**

Go to [https://www.apachefriends.org/download.html](https://www.apachefriends.org/download.html)
From the website choose the file you want (choose the Windows distribution, for me, it was version 7.4.3), and download it.
Go to your download folder, and launch the xampp installer. During the installation, you will be asked if you need a few other programs, you only need **Apache**, **MySQL**, **PHP** and **PHPmyAdmin**.
Do not forget to clear the Learn more about Bitnami for XAMPP option

**Start and Configure XAMPP**

Normally the **Control Panel** should have pop in front of you, in the **Modules section**, you will find all the web services available. You can start each service by clicking the Start button.
After launching the services, you should be able to access the XAMPP dashboard via the following link (if using a VPS just change the **localhost** with whatever is your IP address):

> http://localhost/dashboard

**/!\ Important if you are using a VPS**

If your server is on a VPS and you try to access the **PHPmyAdmin**, a webpage should appear and tell you that you cannot access the server because it is only available on the **Localhost**, you can easily fix that:
Go to the following folder C:\xampp\apache\conf\extra and open the file http-xampp.conf. There change the following:

    # since XAMPP 1.4.3
    <LocationMatch "^/(?i:(?:security))">
        AllowOverride AuthConfig Limit
        Require local
        ErrorDocument 403 /error/XAMPP_FORBIDDEN.html.var
    </LocationMatch>

With:

    # since XAMPP 1.4.3
    <LocationMatch "^/(?i:(?:security))">
        AllowOverride AuthConfig Limit
        Order deny, allow
        Allow from all
        Require all granted
        # If you only want to allow some connexion you can use Deny from all and Allow from TheIpAdressYouWantToAllow
        ErrorDocument 403 /error/XAMPP_FORBIDDEN.html.var
    </LocationMatch>
    Restart XAMPP.

**Change default security settings ~ RECOMMENDED**

Configure it with the "XAMPP Shell" (command prompt). Open the shell from the XAMPP control pane and execute this command:

`mysqladmin.exe -u root password YOURNEWPASSWORD`

**Full FAQ for XAMPP**

[https://www.apachefriends.org/faq_windows.html](https://www.apachefriends.org/faq_windows.html)

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

- Open your resource folder, go to [gamemodes] then [maps] open "fivem-map-skater" go into fxmanifest then change `resource_type 'map' { gameTypes = { ['basic_gamemode'] = true } }` to `resource_type 'map' { gameTypes = { ['drp_core'] = true } }`
- Import the **core.sql** to your database, either by using the import function from PHPmyAdmin or any other Database Tool of your choice.
- Change your **server.cfg** accordingly with all the resources you added in the previous step and comment the `ensure fivem` line. It should look like this:

![server.cgf](https://i.ibb.co/YLN3VWM/config-cfg-1.png)

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

![server.cgf](https://i.ibb.co/2gkW0Yg/config-cfg-2.png)

**3. DatabaseAPI and externalSQL configuration**

Open the following file, with either nano or with your FTP and any NotePad app, the **config.json** in externalSQL folder.
Change the info inside following those instructions:    

**Instructions**
____
- **host**, is where the database is, so do not change it unless it is not on the same server
- **port**, is the port the ExternalSQL will use to talk to your database, it needs an unused one (so not 3306 which is the one used by default by MySQL/MariaDB)
- **route**, is where the API folder is located, do not touch it unless you like boo-boo
- **secret**, is used to encrypt the talk between ExternalSQL and the Database, it needs to be changed to a random string 
- **community**, is the name of your community
____
- **connectionLimit**, is how much-simultaned connections are authorised, do not change it unless you know what you do
- **host**, is where the database is, so do not change it unless it is not on the same server
- **user**, is the user used for the connexion to MySQL/MariaDB (ndlr the one you created) if you have not made a new one keep root
- **password**, is the password of the previous **user**, only add one if you have a password on with this specific **user**
- **database**, is the name of the database where your data is, be sure it is the right name!
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
			"user": "root",
			"password": "",
			"database": "drp"
		},
		
		"devmodeactive": false,
		"createtokenonstart": true
	}

**4. Start your server**

Start normally your server