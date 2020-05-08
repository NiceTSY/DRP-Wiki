

# Server Events

Following you will find all the server-side events, and their description, that are currently in use inside the DRP-Framework. For better looking they are in alphabetical order by DRP-scripts.

| DRP script| Arguments | Description |
| :---: | :---: |:--- |
| Where the events is | Argument(s) it needs | Brief description about the event |

> Remember you can use **TriggerServerEvent()** from the **client side** or **TriggerEvent()** from the **server side**

## Contents

- [drp_bank](https://github.com/OfficialDarkzy/DRP-Core/wiki/Server-Events#drp_bank)
    - DRP_Bank:DepositMoney
    - DRP_Bank:LaunderMoney
    - DRP_Bank:RequestATMInfo
    - DRP_Bank:WithdrawMoney
- [drp_clothing](https://github.com/OfficialDarkzy/DRP-Core/wiki/Server-Events#drp_clothing)
    - clothes:save
    - DRP_Clothing:FirstSpawn
    - DRP_Clothing:RestartClothing
    - DRP_Clothing:SaveModel
- [drp_core](https://github.com/OfficialDarkzy/DRP-Core/wiki/Server-Events#drp_core)
    - DRP_Core:AddPlayerToTable
    - DRP_Core:BanPlayer
    - DRP_Core:ConnectionSetWeather
    - DRP_Core:KickPlayer
    - DRP_Core:SendMessage
    - DRP_TimeSync:ConnectionSetTime
- [drp_death](https://github.com/OfficialDarkzy/DRP-Core/wiki/Server-Events#drp_death)
    - DRP_Core:TriggerDeathStart
    - DRP_Bank:DropOnDeath
    - DRP_Bank:PickupDroppedCash
    - DRP_Death:GetDeathStatus
    - DRP_Death:Revived
 - [drp_garage](https://github.com/OfficialDarkzy/DRP-Core/wiki/Server-Events#drp_garage)
    - DRP_Auction:AddVehicleToAuction
    - DRP_Auction:CheckOwnership
    - DRP_Auction:GetVehicleList
    - DRP_Auction:Purchase
    - DRP_Auction:PurchaseChecker
    - DRP_CarWash:CheckMoney
    - DRP_Garages:CheckVehicleOwner
    - DRP_Garages:GetSelectedVehicleData
    - DRP_Garages:GetVehicles
    - DRP_Garages:GetVehiclesForImpound
    - DRP_Garages:GiveKeys
    - DRP_Garages:ImpoundStateChanger
    - DRP_Garages:RequestOpenMenu
    - DRP_Garages:RequestStoreVehicle
    - DRP_Garages:StateChanger
    - DRP_Garages:UpdateVehicle
    - DRP_Garages:UpdateVehicleFuel
 - [drp_id](https://github.com/OfficialDarkzy/DRP-Core/wiki/Server-Events#drp_id)
    - DRP_ID:CreateCharacter
    - DRP_ID:DeleteCharacter
    - DRP_ID:Disconnect
    - DRP_ID:LastKnownPosition
    - DRP_ID:RequestOpenMenu
    - DRP_ID:SaveCharacterLocation
    - DRP_ID:SelectCharacter
- [drp_jobcore](https://github.com/OfficialDarkzy/DRP-Core/wiki/Server-Events#drp_jobcore)
    - DRP_JobCore:Salary
    - DRP_JobCore:StartUp
- [drp_LegacyFuel](https://github.com/OfficialDarkzy/DRP-Core/wiki/Server-Events#drp_legacyfuel)
    - fuel:pay
    - fuel:petrolcanpay
- [drp_soda](https://github.com/OfficialDarkzy/DRP-Core/wiki/Server-Events#drp_soda)
    - DRP_Soda:checkAccounts
- [drp_tattoos](https://github.com/OfficialDarkzy/DRP-Core/wiki/Server-Events#drp_tattoos)
    - DRP_Tattoos:GetTattoos
    - DRP_Tattoos:PutClothesBackOn
    - DRP_Tattoos:SaveTattoos

## drp_bank

### DRP_Bank:DepositMoney

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_bank | [amount] | Deposit a certain [amount] to the bank account of the character |

**example**: 
```lua
TriggerServerEvent("DRP_Bank:DepositMoney", 250)
```

### DRP_Bank:LaunderMoney

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_bank | none | Clean all the dirty money of the character and return it as cash |

**example**: 
```lua
TriggerServerEvent("DRP_Bank:LaunderMoney")
```

### DRP_Bank:RequestATMInfo

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_bank | none | Get the character bank data and open the ATM menu through the client event "DRP_Bank:OpenMenu" |

**example**: 
```lua
TriggerServerEvent("DRP_Bank:RequestATMInfo")
```

### DRP_Bank:WithdrawMoney

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_bank | [amount] | Withdraw a certain [amount] from the bank account of the character |

**example**: 
```lua
TriggerServerEvent("DRP_Bank:WithdrawMoney", 250)
```

## drp_clothing

### clothes:save

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_clothing | [player_data] | Save the [player_data] skin to the database |

**example**: 
```lua
for i = 0, 11 do
    player_data.cdrawables[i+1] = GetPedDrawableVariation(GetPlayerPed(-1), i)
    if i ~= 2 then
        player_data.ctextures[i+1] = GetPedTextureVariation(GetPlayerPed(-1), i)
    end
    player_data.cpalette[i+1] = GetPedPaletteVariation(GetPlayerPed(-1), i)
end

TriggerServerEvent("clothes:save", player_data)
```

### DRP_Clothing:FirstSpawn

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_clothing | none | Get the default clothing for first spawn and return them through the client event "clothes:spawn" |

**example**: 
```lua
TriggerServerEvent("DRP_Clothing:FirstSpawn")
```

### DRP_Clothing:RestartClothing

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_clothing | none | Reset the clothes of the [source] to database clothes through the client event "DRP_Clothing:ResetClothing" |

**example**: 
```lua
TriggerServerEvent("DRP_Clothing:RestartClothing")
```

### DRP_Clothing:SaveModel

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_clothing | [model] | Save the clothe's [model] of a character to the database |

**example**: 
```lua
local skin = "mp_m_freemode_01"
TriggerServerEvent("DRP_Clothing:SaveModel", skin)
```

## drp_core

### DRP_Core:AddPlayerToTable

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_core | none | Add the player to the users table inside the database |

**example**: 
```lua
TriggerServerEvent("DRP_Core:AddPlayerToTable")
```

### DRP_Core:BanPlayer

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_core | [selectedPlayer] [message] [time] [permban] | Ban a [selectedPlayer] for a selected [time] or [permban] from the server and send him a [message] |

**example**: 
```lua
local thisMoron = --get the player as you want--
TriggerServerEvent("DRP_Core:KickPlayer", thisMoron, "This is an admin message", 1000, false)
```

### DRP_Core:ConnectionSetWeather

| DRP script| Arguments |Description |
| :---: | :---: | :--- |
| drp_core | none | Sync the weather for the player trough the client event "DRP_Core:SetWeather" |

**example**: 
```lua
TriggerServerEvent("DRP_Core:ConnectionSetWeather")
```

### DRP_Core:KickPlayer

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_core | [selectedPlayer] [message] | Kick a [selectedPlayer] from the server and send him a [message] |

**example**: 
```lua
local thisMoron = --get the player as you want--
TriggerServerEvent("DRP_Core:KickPlayer", thisMoron, "This is an admin message")
```

### DRP_Core:SendMessage

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_core | [message] | Pass an admin [message] to the player |

**example**: 
```lua
TriggerServerEvent("DRP_Core:SendMessage", "This is an admin message")
```

### DRP_TimeSync:ConnectionSetTime

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_core | none | Sync the time for the player trough the client event "DRP_TimeSync:SetTime" |

**example**: 
```lua
TriggerServerEvent("DRP_TimeSync:ConnectionSetTime")
```

## drp_death

### DRP_Core:TriggerDeathStart

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_death | none | Start the trigger for the death status through the client event "DRP_Core:InitDeath" |

**example**: 
```lua
TriggerServerEvent("DRP_Core:TriggerDeathStart")
```

### DRP_Bank:DropOnDeath

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_death | none | Drop the cash money of the character when he died if it is enabled in the config file |

**example**: 
```lua
TriggerServerEvent("DRP_Bank:DropOnDeath")
```

### DRP_Bank:PickupDroppedCash

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_death | [amount] | Return the dropped [amount] of money to the character |

**example**: 
```lua
TriggerServerEvent("DRP_Bank:PickupDroppedCash", 250)
```

### DRP_Death:GetDeathStatus

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_death | none | Return the death status of the character through the client event "DRP_Death:IsDeadStatus" |

**example**: 
```lua
TriggerServerEvent("DRP_Death:GetDeathStatus")
```

### DRP_Death:Revived

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_death | [boolValue] | Update the death status of the character thanks to the [boolValue] |

**example**: 
```lua
TriggerServerEvent("DRP_Death:Revived", true)
```

## drp_garage

### DRP_Auction:AddVehicleToAuction

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [mods] [price] | Add the car with the specified [mods] to the auction under the specified [price] |

**example**: 
```lua
local ped = PlayerPedId()
local vehData = GetVehiclePedIsUsing(ped)
TriggerServerEvent("DRP_Auction:AddVehicleToAuction", vehData, 1000000)
```

### DRP_Auction:CheckOwnership

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [vehicledata] [plate] | Check the ownership of the vehicule with the specified [plate] |

**example**: 
```lua
local ped = PlayerPedId()
local vehData = GetVehiclePedIsUsing(ped)
local plate = GetVehicleNumberPlateText(veh)
TriggerServerEvent("DRP_Auction:CheckOwnership", vehData, plate)
```

### DRP_Auction:GetVehicleList

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | none | Get the vehicule taht are currently under auction and return them through the client event "DRP_Auction:VehicleList" |

**example**: 
```lua
TriggerServerEvent("DRP_Auction:GetVehicleList")
```

### DRP_Auction:Purchase

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | none | Not working :troll: |

**example**: 
```lua
TriggerServerEvent("DRP_Auction:Purchase")
```

### DRP_Auction:PurchaseChecker

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [price] | Check if the buyer has enought bank money to pay the auction [price] |

**example**: 
```lua
TriggerServerEvent("DRP_Auction:PurchaseChecker", 1000000)
```

### DRP_CarWash:CheckMoney

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [cost] | Check if the character has enougth money to pay carwash [cost] |

**example**: 
```lua
TriggerServerEvent("DRP_CarWash:CheckMoney", 10)
```

### DRP_Garages:CheckVehicleOwner

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [netid] [plate] | Check if the character is the owner of the vehicule with the specified [plate] and [netid] |

**example**: 
```lua
local ped = PlayerPedId()
local veh = GetVehiclePedIsIn(ped, false)
local plate = GetVehicleNumberPlateText(veh)
local id =  NetworkGetNetworkIdFromEntity(veh)
TriggerServerEvent("DRP_Garages:CheckVehicleOwner", plate, id)
```

### DRP_Garages:GetSelectedVehicleData

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [vehicle_id] [type] | Return the [vehicule_id] info from the [type] of garage it was |

**example**: 
```lua
TriggerServerEvent("DRP_Garages:GetSelectedVehicleData", 1, "garage")
```

### DRP_Garages:GetVehicles

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | none | Return all vehicules info of a character through the client event "DRP_Garages:GarageCommand" |

**example**: 
```lua
TriggerServerEvent("DRP_Garages:GetVehicles")
```

### DRP_Garages:GetVehiclesForImpound

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [plate] [impoundslot] | Put the vehicule with the specified [plate] to the specified [impoundslot] |

**example**: 
```lua
local ped = PlayerPedId()
local veh = GetVehiclePedIsIn(ped, false)
local plate = GetVehicleNumberPlateText(veh)
TriggerServerEvent("DRP_Garages:GetVehiclesForImpound", plate, 1)
```

### DRP_Garages:GiveKeys

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [id] [plate] | Give a key of the vehicule with the specified [plate] and [id] |

**example**: 
```lua
local ped = PlayerPedId()
local veh = GetVehiclePedIsIn(ped, false)
local plate = GetVehicleNumberPlateText(veh)
local id =  NetworkGetNetworkIdFromEntity(veh)
TriggerServerEvent("DRP_Garages:GiveKeys", plate, id)
```

### DRP_Garages:ImpoundStateChanger

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [plate] [state] [impoundslot] | Change the impound [state] of the vehicule with the specified [plate] to a the specified [impoundslot] |

**example**: 
```lua
local ped = PlayerPedId()
local veh = GetVehiclePedIsIn(ped, false)
local plate = GetVehicleNumberPlateText(veh)
TriggerServerEvent("DRP_Garages:StateChanger", plate, "IMPOUND", 1)
```

### DRP_Garages:RequestOpenMenu

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [menu] | Get the character's cars and show them inside the wanted [menu] via the client event "DRP_Garages:OpenGarageMenu" |

**example**: 
```lua
TriggerServerEvent("DRP_Garages:RequestOpenMenu", "open_garage_menu")
```

### DRP_Garages:RequestStoreVehicle

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [plate] | Store the vehicule with the specified [plate] |

**example**: 
```lua
local ped = PlayerPedId()
local veh = GetVehiclePedIsIn(ped, false)
local plate = GetVehicleNumberPlateText(veh)
TriggerServerEvent("DRP_Garages:RequestStoreVehicle", plate)
```

### DRP_Garages:StateChanger

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [plate] [state] | Change the [state] of the vehicule with the specified [plate] |

**example**: 
```lua
local ped = PlayerPedId()
local veh = GetVehiclePedIsIn(ped, false)
local plate = GetVehicleNumberPlateText(veh)
TriggerServerEvent("DRP_Garages:StateChanger", plate, "IN")
```

### DRP_Garages:UpdateVehicle

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [plate] [data] [garage_slot] [fuel_level] | Update the vehicule with the specified [plate] |

**example**: 
```lua
local ped = PlayerPedId()
local veh = GetVehiclePedIsIn(ped, false)
local plate = GetVehicleNumberPlateText(veh)
local vehMods = VehicleData(veh)
local fuel_level = exports["drp_LegacyFuel"]:GetFuel(veh)
TriggerServerEvent("DRP_Garages:UpdateVehicle", plate, vehMods, 1, fuel_level)
```

### DRP_Garages:UpdateVehicleFuel

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garage | [plate] [fuel_level] | Update the [fuel_level] of the vehicule with the specified [plate] |

**example**: 
```lua
local ped = PlayerPedId()
local veh = GetVehiclePedIsIn(ped, false)
local plate = GetVehicleNumberPlateText(veh)
local fuel_level = exports["drp_LegacyFuel"]:GetFuel(veh)
TriggerServerEvent("DRP_Garages:UpdateVehicleFuel", plate, fuel_level)
```

## drp_id

### DRP_ID:CreateCharacter

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | [newCharacterData] | Create a new character with its [newCharacterData] for a player |

**example**: 
```lua
local data = --create the data as you want--
TriggerServerEvent("DRP_ID:CreateCharacter", {name = data.name, age = data.age, gender = data.gender, dob = data.dob})
```

### DRP_ID:DeleteCharacter

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | [character_id] | Delete the character with the specified [character_id] |

**example**: 
```lua
TriggerServerEvent("DRP_ID:DeleteCharacter", 1)
```

### DRP_ID:Disconnect

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | none | Return the fact that player disconnect |

**example**: 
```lua
TriggerServerEvent("DRP_ID:Disconnect")
```

### DRP_ID:LastKnownPosition

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | [ped] | Return through the client event "DRP_ID:LoadSelectedCharacter" the [ped] last known position |

**example**: 
```lua
local ped = PlayerPedId()
TriggerServerEvent("DRP_ID:LastKnownPosition", ped)
```

### DRP_ID:RequestOpenMenu

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | none | Open the character selector menu through the client event "DRP_ID:OpenMenu" |

**example**: 
```lua
TriggerServerEvent("DRP_ID:RequestOpenMenu", true)
```

### DRP_ID:SaveCharacterLocation

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | [x] [y] [z] | Save to the database the character location |

**example**: 
```lua
local ped = PlayerPedId()
local pos = GetEntityCoords(ped, true)
TriggerServerEvent("DRP_ID:SaveCharacterLocation", pos.x, pos.y, pos.z)
```

### DRP_ID:SelectCharacter

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | [character_id] | Select the character thanks to its [character_id] and show the Spawn Selector |

**example**: 
```lua
TriggerServerEvent("DRP_ID:SelectCharacter", 1)
```

## drp_jobcore

### DRP_JobCore:Salary

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_jobcore | none | Trigger the salary service for jobs |

**example**: 
```lua
TriggerServerEvent("DRP_JobCore:Salary")
```

### DRP_JobCore:StartUp

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_jobcore | none | Start the DRP_JobCore for the character |

**example**: 
```lua
TriggerServerEvent("DRP_JobCore:StartUp")
```

## drp_LegacyFuel

### fuel:pay

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_LegacyFuel | [price] | Pay the [price] for the fuel the character put in the vehicule |

**example**: 
```lua
TriggerServerEvent("fuel:pay", 150)
```

### fuel:petrolcanpay

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_LegacyFuel | [price] [refill] | Pay the [price] of buying or refuelling a petrol can thanks to [refill] |

**example**: 
```lua
TriggerServerEvent("fuel:petrolcanpay", 150, false)
```

## drp_soda

### DRP_Soda:checkAccounts

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_soda | none | Check if the character has the money and have enough inventory space to get a soda |

**example**: 
```lua
TriggerServerEvent("DRP_Soda:checkAccounts")
```

## drp_tattoos

### DRP_Tattoos:GetTattoos

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_tattoos | none | Get the tattoos of the character and return them through the client event "DRP_Tattoos:CharacterTattoos" |

**example**: 
```lua
TriggerServerEvent("DRP_Tattoos:GetTattoos")
```

### DRP_Tattoos:PutClothesBackOn

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_tattoos | none | Put back the player's clothes |

**example**: 
```lua
TriggerServerEvent("DRP_Tattoos:PutClothesBackOn")
```

### DRP_Tattoos:SaveTattoos

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_tattoos | [tattoosList] [price] [value] | Set the tattoos from [tattoosList] to a character with the following [price] and [value] |

**example**: 
```lua
local currentTattoos = {}
local tattoosList = {}

for _, v in pairs(tattoosList) do
    TriggerServerEvent("DRP_Tattoos:SaveTattoos", currentTattoos, 100, {category = v.category, texture = v.nameHash})
end
```