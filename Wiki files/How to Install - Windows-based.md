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

![server.cgf](https://i.ibb.co/vBnqvkR/ressource-cfg1.png)

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

![server.cgf](https://i.ibb.co/VwpgJyc/resource-cfg2.png)

**3. DatabaseAPI and externalSQL configuration**

Open the following file, with either nano or with your FTP and any NotePad app, the **config.js** file in DatabaseAPI folder and **config.lua** in externalSQL folder.
Change the info inside following those instructions:    

**config.js**


    ExternalConfig = {};
    
    // Port API Runs On
    ExternalConfig.Server = {
        // This is the port that will be used by both application
        // to have lovely chit-chat if you change one change the other
        port: 2000
    }
    
    // Database Connection Configs
    ExternalConfig.Database = {
        // Not needed to change
        connectionLimit: 100,
        // Let it be
        host: "localhost",
        // This will be the user used for the connexion to MySQL
        // ndlr the one you created, if you have not made a new one
        // keep root
        user: "root", 
        // Only put a password if have a password on the user
        password: "",
        // This is the name of the database that it will access
        // be sure its the right name!
        database: "drp"
    };
    
    // API Configs
    ExternalConfig.API = {
        // Do not change unless you know what you do
        route: "/external/api",
        // Fucking change this to another random string and put the same
        // string in the config.lua of the externalsql
        secret: "CHANGEME"
    }
    
    ExternalConfig.DevModeActive = false;
    
    module.exports.config = ExternalConfig;
    module.exports.server = ExternalConfig.Server;
    module.exports.database = ExternalConfig.Database;
    module.exports.api = ExternalConfig.API;
    module.exports.dev = ExternalConfig.DevModeActive;

**config.lua**

    SQLConfig = {}
    
    -- Connection Configurations
    -- Let it be
    SQLConfig.host = "localhost"
    -- This is the port that will be used by both application
    -- to have lovely chit-chat, if you change one change the other
    SQLConfig.port = 2000
    -- Do not change unless you know what you do
    SQLConfig.apipath = "/external/api"
    -- Fucking change this to another random string and put the same
    -- string in the config.js of the DatabaseAPI
    SQLConfig.secret = "CHANGEME"
    -- The name of your community
    SQLConfig.community = "DRP"
    
    -- Further Configurations
    SQLConfig.CreateTokenOnStart = true
    
    --[[ DO NOT EDIT BELOW ]]--

**4. Start your server**

Start normally your server