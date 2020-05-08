# Help and Support

If you cannot find an answer from one of your issue there, your question was probably already answer on the official Discord, you can join it there: [https://discord.gg/QTuvsPd](https://discord.gg/QTuvsPd)

## Content

- [Connection Failed: Couldn't load resource DatabaseAPI. :(](https://github.com/OfficialDarkzy/DRP-Core/wiki/Help-and-Support#connection-failed-couldnt-load-resource-databaseapi-)
- [My character is not created when I press create](https://github.com/OfficialDarkzy/DRP-Core/wiki/Help-and-Support#connection-failed-couldnt-load-resource-databaseapi-)
- [I have a "No such export DBAsyncQuery in resource externalSQL" error](https://github.com/OfficialDarkzy/DRP-Core/wiki/Help-and-Support#i-have-a-no-such-export-dbasyncquery-in-resource-externalsql-error)
- [I have a "strfnd" error](https://github.com/OfficialDarkzy/DRP-Core/wiki/Help-and-Support#i-have-a-strfnd-error)
- [I get errors in my console for dependencies](https://github.com/OfficialDarkzy/DRP-Core/wiki/Help-and-Support#i-get-errors-in-my-console-for-dependencies)
- [I get lots of errors for "character" in my console](https://github.com/OfficialDarkzy/DRP-Core/wiki/Help-and-Support#i-get-lots-of-errors-for-character-in-my-console)

### Connection Failed: Couldn't load resource DatabaseAPI. :(

Be sure there is the **fxmanifest.lua** inside the DatabaseAPI folder with the following:

    fx_version 'adamant'
    games { 'rdr3', 'gta5' }

    server_script 'server.js'

### My character is not created when I press create

Put **license** and **phonenumber** columns to **Default Null** inside your database.

### I have a "No such export DBAsyncQuery in resource externalSQL" error

Make sure you have all the latest scripts from DRP, and if the error continues, go to the file where the error was raised and change all the `exports["externalsql"]:DBAsyncQuery` with `exports["externalsql"]:AsyncQueryCallback`

### I have a "strfnd" error

This is most likely an issue with your database login information. If you are adamant it is not, then made sure you have the latest install of DRP and check that all your fields in your database have a default value.

### I get errors in my console for dependencies

Make sure you have all the right resources installed for a certain script to work.

### I get lots of errors for "character" in my console

Please make sure you have read the readme and installed the framework correctly.