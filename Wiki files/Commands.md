# Commands

In order to use a command, you need to be inside the chat (**T** key) and have the correct rank (user, admin, superadmin).

## Contents

- [Admin commands](https://github.com/OfficialDarkzy/DRP-Core/wiki/Commands#admin-commands)
- [Car commands](https://github.com/OfficialDarkzy/DRP-Core/wiki/Commands#car-commands)
- [Chat commands](https://github.com/OfficialDarkzy/DRP-Core/wiki/Commands#chat-commands)
- [Economy commands](https://github.com/OfficialDarkzy/DRP-Core/wiki/Commands#economy-commands)
- [Jobs commands](https://github.com/OfficialDarkzy/DRP-Core/wiki/Commands#jobs-commands)
- [Weather commands](https://github.com/OfficialDarkzy/DRP-Core/wiki/Commands#weather-commands)
- [Other commands](https://github.com/OfficialDarkzy/DRP-Core/wiki/Commands#other-commands)

## Commands

### Admin commands

| Command | Arguments type | Arguments | Example | Description | Rank | DRP script |
| ----------- | --- | --- | -------------- | --- | --- | --- |
| admin | none | - | /admin | Show the admin menu, permit to chat, reports, kick, ban or whitelist users | superadmin | drp_core |
| adminaddcop | [database ID] | [int] | /adminaddcop 1 | Set someone as a cop | superadmin | drp_core |
| adminrank | none | - | /adminrank | Show your admin rank | all | drp_core |
| adminrevive | none | - | /adminrevive | Revive yourself | admin | drp_death |
| coords | none | - | /coords | Send your current coords to the chat | admin | drp_core |
| showcoords | none | - | /showcoords | Show on screen your current coords | admin | drp_core |
| heal | none | - | /heal | Heal yourself | admin | drp_core |
| tp | [x] [y] [z] | - | /tp 100 -100 80 | Teleport yourself to the specified [x] [y] [z] coords | admin | drp_core |
| tpm | none | - | /tpm | Teleport yourself to the specified waypoint | admin | drp_core |

### Car commands

| Command | Arguments type | Arguments | Example | Description | Rank | DRP script |
| ----------- | --- | --- | -------------------------------- | --- | --- | --- |
| car | [vehicule] | - | /car zentorno | Teleport a [vehicule] in front of you | superadmin | drp_core |
| dv | none | - | /dv | Delete the closest vehicule | superadmin | drp_core |
| engine | none | - | /engine | Start/stop the engine of the vehicule you are currently in | all | drp_garages |
| fix | none | - | /fix | Fix the vehicule you are in | superadmin | drp_core |
| impound | [impound ID] | [1: Centrum; 2: Sandy Shores; 3: Paleto Bay] | /impound 1 | Impound the nearest vehicule to the specified [impound ID] garage | all | drp_garages |
| garage | none | - | /garage | Show all your registered vehicule, either inside a garage or not | all | drp_garages |
| hood | none | - | /hood | Open/close the hood of the vehicule you are currently in | all | drp_garages |
| trunk | none | - | /trunk | Open/close the trunk of the vehicule you are currently in | all | drp_garages |

### Chat commands

| Command | Arguments type | Arguments | Example | Description | Rank | DRP script |
| ----------- | --- | --- | -------------------------------- | --- | --- | --- |
| advert | [string] | [Your message] | /advert This is an advertisement | Advertise a [string] in the chat box | all | drp_core |
| me | [string] | [Your message] | /me This is a private message | Send a [string] to the nearest players | all | drp_core |
| ooc | [string] | [Your message] | /ooc This is out of character | Say a [string] out of character in the chat box | all | drp_core |
| tweet | [string] | [Your message] | /tweet This is a tweet | Tweet a [string] in the chat box | all | drp_core |

### Economy commands

| Command | Arguments type | Arguments | Example | Description | Rank | DRP script |
| ---------- | --- | --- | ----------------- | --- | --- | --- |
| addbank | [database ID] [amount] | [int] [int] | /addbank 1 100 | Add a certain [amount] to the bank account of the user with the [database ID] | superadmin | drp_core |
| addcash | [database ID] [amount] | [int] [int] | /addcash 1 100 | Add a certain [amount] of cash to the user with the [database ID] | superadmin | drp_core |
| bank | none | - | /bank | Show how much on your bank account you have | all | drp_bank |
| cash | none | - | /cash | Show how much cash you have | all | drp_bank |
| dirty | none | - | /dirty | Show how much dirty money you have | all | drp_bank |
| removebank | [database ID] [amount] | [int] [int] | /removebank 1 100 | Remove a certain [amount] from the bank account of the user with the [database ID] | superadmin | drp_core |
| removecash | [database ID] [amount] | [int] [int] | /removecash 1 100 | Remove a certain [amount] of cash to the user with the [database ID] | superadmin | drp_core |

### Jobs commands

| Command | Arguments type | Arguments | Example | Description | Rank | DRP script |
| --- | --- | --- | ---- | --- | --- | --- |
| job | none | - | /job | Show your current job | all | drp_jobcore |

### Weather commands

| Command | Arguments type | Arguments | Example | Description | Rank | DRP script |
| ------- | --- | --- | ------------- | --- | --- | --- |
| time | [hour] [minute] | [1-23] [0-59] | /time 1 30 | Set the time to a specific [hour] [minute] | admin | drp_core |
| weather | [type] | [extrasunny; clear; neutral; smog; foggy; overcast; clouds; clearing; rain; thunder; snow; blizzard; snowlight; xmas; hallowen] | /weather smog | Set the weather to a specific [type] | admin | drp_core |

### Other commands

| Command | Arguments type | Arguments | Example | Description | Rank | DRP script |
| ------- | --- | --- | -------- | --- | --- | --- |
| respawn | none | - | /respawn | Respawn yourself | admin | drp_death |
| showid | none | - | /showid | Show basic information about your character | all | drp_core |