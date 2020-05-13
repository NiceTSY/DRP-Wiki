# Help and Support

If you cannot find an answer from one of your issue there, your question was probably already answer on the official Discord, you can join it there: [https://discord.gg/QTuvsPd](https://discord.gg/QTuvsPd)

## Content

- [My character is not created when I press create](https://github.com/OfficialDarkzy/DRP-Core/wiki/Help-and-Support#connection-failed-couldnt-load-resource-databaseapi-)
- [I have a "No such export DBAsyncQuery in resource externalSQL" error](https://github.com/OfficialDarkzy/DRP-Core/wiki/Help-and-Support#i-have-a-no-such-export-dbasyncquery-in-resource-externalsql-error)
- [I have a "strfnd" error](https://github.com/OfficialDarkzy/DRP-Core/wiki/Help-and-Support#i-have-a-strfnd-error)
- [I get errors in my console for dependencies](https://github.com/OfficialDarkzy/DRP-Core/wiki/Help-and-Support#i-get-errors-in-my-console-for-dependencies)
- [I get lots of errors for "character" in my console](https://github.com/OfficialDarkzy/DRP-Core/wiki/Help-and-Support#i-get-lots-of-errors-for-character-in-my-console)
- [I am stuck on Awaiting scripts](https://github.com/OfficialDarkzy/DRP-Core/wiki/Help-and-Support#i-am-stuck-on-awaiting-scripts)

### My character is not created when I press create

1. Check if every column inside your database for the character table have a default value.
2. Clear your cache

### I have a "No such export DBAsyncQuery in resource externalSQL" error

1. Make sure you have all the latest scripts from DRP
2. Go to the file where the error was raised and change all the `exports["externalsql"]:DBAsyncQuery` with `exports["externalsql"]:AsyncQueryCallback`

### I have a "strfnd" error

1. Make sure you have all the latest scripts from DRP
2. Check if your database port is not blocked by the firewall
3. Check if all your columns inside the database have a default value
4. The database is not configured correctly check your `config.json` in the **externalSQL** resource

### I get errors in my console for dependencies

1. One of the needed resource is not installed, check the **fxmanifest.lua** to know which one

### I get lots of errors for "character" in my console

1. The database is not configured correctly check your `config.json` in the **externalSQL** resource

### I am stuck on Awaiting scripts

1. Clear your cache