# Client Events

Following you will find all the client-side events, and their description, that are currently in use inside the DRP-Framework. For better looking they are in alphabetical order by DRP-scripts.

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| Where the events is | Argument(s) it needs | Brief description about the event |

> Remember you can use **TriggerClientEvent()** from the **server side** or **TriggerEvent()** from the **client side**
> **source** is always required from a call from a server-sided scripts and represent a single player, if you want to call the event for all player change **source** with **-1**

## Contents

- [drp_bank](https://github.com/OfficialDarkzy/DRP-Core/wiki/Client-Events#drp_bank)
    - DRP_Bank:ActionCallback
    - DRP_Bank:OpenMenu
- [drp_clothing](https://github.com/OfficialDarkzy/DRP-Core/wiki/Client-Events#drp_clothing)
    - clothes:spawn
- [drp_core](https://github.com/OfficialDarkzy/DRP-Core/wiki/Client-Events#drp_core)
    - DRP_TimeSync:SetTime
    - DRP_WeatherSync:SetWeather
- [drp_death](https://github.com/OfficialDarkzy/DRP-Core/wiki/Client-Events#drp_death)
    - DRP_Core:InitDeath
    - DRP_Death:IsDeadStatus
    - DRP_Core:Revive
- [drp_garages](https://github.com/OfficialDarkzy/DRP-Core/wiki/Client-Events#drp_garages)
    - DRP_Garages:CreateImpoundVehicle
    - DRP_Garages:CreatePersonalVehicle
    - DRP_Garages:GarageCommand
    - DRP_Garages:GiveKeysToVehicleInfront
    - DRP_Garages:ImpoundVehicle
    - DRP_Garages:OpenGarageMenu
    - DRP_Garages:StoreVehicle
- [drp_id](https://github.com/OfficialDarkzy/DRP-Core/wiki/Client-Events#drp_id)
    - DRP_ID:CloseSpawnSelectionMenu
    - DRP_ID:LoadSelectedCharacter
    - DRP_ID:OpenMenu
    - DRP_ID:OpenVehicleList
    - DRP_ID:SpawnSelection
    - DRP_ID:UpdateMenuCharacters
    - sendProximityMessageMe
    - sendProximityMessageRoll
    - sendProximityShowId
- [drp_LegacyFuel](https://github.com/OfficialDarkzy/DRP-Core/wiki/Client-Events#drp_LegacyFuel)
    - fuel:removeFuelorAddPetrolcan
- [drp_notifications](https://github.com/OfficialDarkzy/DRP-Core/wiki/Client-Events#drp_notifications)
	- DRP_Core:CustomIcon
    - DRP_Core:CustomURLIcon
    - DRP_Core:Error
    - DRP_Core:Info
    - DRP_Core:Success
    - DRP_Core:Warning
- [drp_soda](https://github.com/OfficialDarkzy/DRP-Core/wiki/Client-Events#drp_soda)
	- DRP_Soda:getSoda
- [drp_tattoos](https://github.com/OfficialDarkzy/DRP-Core/wiki/Client-Events#drp_tattoos)
	- DRP_Tattoos:BoughtSuccess
	- DRP_Tattoos:CharacterTattoos
	- DRP_Tattoos:OpenMenu

## drp_bank

### DRP_Bank:ActionCallback

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_bank | [status] [message] [balance] [cash] | Show a [status] callback with a [message] with the new [balance] and [cash] of the player |

> [balance] and [cash] can be set to false for an error (like insufficient funds)

**example**: 
```lua
TriggerClientEvent("DRP_Bank:ActionCallback", source, true, "Success", 1000, 100)
-- or
TriggerClientEvent("DRP_Bank:ActionCallback", source, false, "Insufficiant Funds", false)
```

### DRP_Bank:OpenMenu

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_bank | [name] [balance] [cash] [menuName] | Open the bank [menuName] to the player [name] and show is  [balance] and [cash] |

**example**: 
```lua
local CharacterData = exports["drp_id"]:GetCharacterData(source)
TriggerEvent("DRP_Bank:GetCharacterMoney", CharacterData.charid, function(characterMoney)

	TriggerClientEvent("DRP_Bank:OpenMenu", source, CharacterData.name, characterMoney.data[1].bank, characterMoney.data[1].cash, menuName)
end)
```

## drp_clothing

### clothes:spawn

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_clothing | [data] | Spawn the [data] clothes to the ped of the player |

**example**: 
```lua
TriggerClientEvent("clothes:spawn", source, data)
```

## drp_core

### DRP_TimeSync:SetTime

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_core | [hours] [minutes] | Sync the time for the player to [hours]:[minutes] |

**example**: 
```lua
TriggerClientEvent("DRP_TimeSync:SetTime", source, 8, 30)
```

### DRP_WeatherSync:SetWeather

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_core | [weatherType] | Sync the weather for the player to the [weatherType] |

**example**: 
```lua
TriggerClientEvent("DRP_WeatherSync:SetWeather", source, "clear")
```

## drp_death

### DRP_Core:InitDeath

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_death | [time] | Start the death of the player for a certain [time] |

**example**: 
```lua
TriggerClientEvent("DRP_Core:InitDeath", source, 450)
```

### DRP_Death:IsDeadStatus

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_death | [data] | Check if the player ([data]) is dead or not |

**example**: 
```lua
local character = exports["drp_id"]:GetCharacterData(source)

exports["externalsql"]:AsyncQueryCallback({
	query = "SELECT * FROM `characters` WHERE `id` = :charid",
	data = {
	charid = character.charid
	}
}, function(deadResults)
	TriggerClientEvent("DRP_Death:IsDeadStatus", source, deadResults["data"])
end)
```

### DRP_Core:Revive

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_death | none | Revive the player |

**example**: 
```lua
TriggerClientEvent("DRP_Core:Revive", source)
```

## drp_garages

### DRP_Garages:CreateImpoundVehicle

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garages | [data] | Spawn a impounded vehicle with its [data] |

**example**: 
```lua
local character = exports["drp_id"]:GetCharacterData(source)
local thisVehicleInfo = {}

exports["externalsql"]:AsyncQueryCallback({
	query = "SELECT * FROM `vehicles` WHERE `id` = :vehicleid",
	data = {vehicleid = vehicle_id}
}, function(selectedVehicleData)
	local allVehicleData = selectedVehicleData["data"]
	for a = 1, #allVehicleData, 1 do
		local mods = json.decode(allVehicleData[a]["vehicleMods"])
		local plate = mods.plate
		table.insert(thisVehicleInfo, { ["modelLabel"] = allVehicleData[a]["modelLabel"], ["state"] = allVehicleData[a]["state"], ["vehicleMods"] = mods, ["plate"] = plate, ["fuel_level"] = allVehicleData[a]["fuel_level"], ["charid"] = character.charid})
	end

	TriggerClientEvent("DRP_Garages:CreateImpoundVehicle", src, thisVehicleInfo)
end)
```

### DRP_Garages:CreatePersonalVehicle

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garages | [data] | Spawn a player vehicle with its [data] |

**example**: 
```lua
local character = exports["drp_id"]:GetCharacterData(source)
local thisVehicleInfo = {}

exports["externalsql"]:AsyncQueryCallback({
	query = "SELECT * FROM `vehicles` WHERE `id` = :vehicleid",
	data = {vehicleid = 1}
}, function(selectedVehicleData)
	local allVehicleData = selectedVehicleData["data"]
	for a = 1, #allVehicleData, 1 do
		local mods = json.decode(allVehicleData[a]["vehicleMods"])
		local plate = mods.plate
		table.insert(thisVehicleInfo, { ["modelLabel"] = allVehicleData[a]["modelLabel"], ["state"] = allVehicleData[a]["state"], ["vehicleMods"] = mods, ["plate"] = plate, ["fuel_level"] = allVehicleData[a]["fuel_level"], ["charid"] = character.charid})
	end
		
	TriggerClientEvent("DRP_Garages:CreatePersonalVehicle", source, thisVehicleInfo)
end)
```

### DRP_Garages:GarageCommand

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garages | [data] | Show if the vehicle(s) stored in [data]is/are impound |

**example**: 
```lua
local vehicles = {}

TriggerEvent("DRP_ID:GetCharacterData", source, function(CharacterData)
exports["externalsql"]:AsyncQueryCallback({
	query = "SELECT * FROM `vehicles` WHERE `char_id` = :charid",
	data = {charid = CharacterData.charid}
}, function(vehicleData)
	local characterVehicles = vehicleData["data"]
	for a = 1, #characterVehicles do
		local mods = json.decode(characterVehicles[a]["vehicleMods"])
		local plate = characterVehicles[a].plate
		table.insert(vehicles, { ["id"] = characterVehicles[a]["id"], ["modelLabel"] = characterVehicles[a]["modelLabel"], ["state"] = characterVehicles[a]["state"], ["vehicleMods"] = mods, ["plate"] = plate, ["garage_slot"] = characterVehicles[a]["garage_slot"], ["impound_slot"] = characterVehicles[a]["impound_slot"], ["charid"] = CharacterData.charid })
	end
	
	TriggerClientEvent("DRP_Garages:GarageCommand", source, vehicles)
end)
```

### DRP_Garages:GiveKeysToVehicleInfront

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garages | none | Give the keys from the nearest vehicle to the player |

**example**: 
```lua
TriggerClientEvent("DRP_Garages:GiveKeysToVehicleInfront", source)
```

### DRP_Garages:ImpoundVehicle

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garages | [data] [impoundslot] [owned] | Impound the vehicle with its [data] to the [impoundslot] and set if it is [owned] or not |

**example**: 
```lua
exports["externalsql"]:AsyncQueryCallback({
	query = "SELECT * FROM `vehicles` WHERE `plate` = :plate",
	data = {plate = "38VTE875"}
}, function(selectedVehiclePlate)
	if #selectedVehiclePlate["data"] >= 1 then
		local allVehicleData = selectedVehiclePlate["data"]
		for a = 1, #allVehicleData, 1 do
			local allVehicleMods = json.decode(allVehicleData[a]["vehicleMods"])
			if plate == allVehicleMods.plate then
				TriggerClientEvent("DRP_Garages:ImpoundVehicle", source, allVehicleData, 1, true)
			end
		end
	else
	
	TriggerClientEvent("DRP_Garages:ImpoundVehicle", source, allVehicleData, 1, false)
	end
end)
```

### DRP_Garages:OpenGarageMenu

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garages | [vehicles] [menu] | Open the [menu] with the specified [vehicles] |

**example**: 
```lua
local vehicles = {}

TriggerEvent("DRP_ID:GetCharacterData", source, function(CharacterData)
	exports["externalsql"]:AsyncQueryCallback({
		query = "SELECT * FROM `vehicles` WHERE `char_id` = :charid",
		data = {charid = CharacterData.charid}
	}, function(vehicleData)
		local characterVehicles = vehicleData["data"]
		for a = 1, #characterVehicles do
			local mods = json.decode(characterVehicles[a]["vehicleMods"])
			local plate = characterVehicles[a].plate
			table.insert(vehicles, { ["id"] = characterVehicles[a]["id"], ["modelLabel"] = 	characterVehicles[a]["modelLabel"], ["state"] = characterVehicles[a]["state"], ["vehicleMods"] = mods, ["plate"] = plate, ["garage_slot"] = characterVehicles[a]["garage_slot"], ["impound_slot"] = characterVehicles[a]["impound_slot"], ["fuel_level"] = characterVehicles[a]["fuel_level"], ["charid"] = CharacterData.charid })
		end

		TriggerClientEvent("DRP_Garages:OpenGarageMenu", source, vehicles, "open_garage_menu")
	end)
end)
```

### DRP_Garages:StoreVehicle

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_garages | none | Store the nearest vehicle owned by the player |

**example**: 
```lua
TriggerClientEvent("DRP_Garages:StoreVehicle", source)
```

## drp_id

### DRP_ID:CloseSpawnSelectionMenu

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | none | Close the spawn selection menu |

**example**: 
```lua
TriggerEvent("DRP_ID:CloseSpawnSelectionMenu")
```

### DRP_ID:LoadSelectedCharacter

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | [ped] [spawn] [spawnInHotel] | Load the [ped] of the player to the [spawn] location |

> [spawnInHotel] is not yet in use and should be set to **true**

**example**: 
```lua
exports["externalsql"]:AsyncQueryCallback({
	query = "SELECT * FROM `characters` WHERE `id` = :character_id",
	data = {character_id = 1}
}, function(characterInfo)
	local lastKnownLocation = json.decode(characterInfo["data"][1].lastLocation)
	table.insert(character, {id = src, charid = character_id, playerid = characterInfo.data[1].playerid, gender = characterInfo.data[1].gender, name = characterInfo.data[1].name, age = characterInfo.data[1].age})
		CloseAllCameras(source)
		
		TriggerClientEvent("DRP_ID:LoadSelectedCharacter", src, "mp_m_freemode_01", lastKnownLocation, true)		
	end)
end)
```

### DRP_ID:OpenMenu

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | [characters] | Open the character selection menu with all the player [characters] |

**example**: 
```lua
TriggerEvent("DRP_Core:GetPlayerData", source, function(results)
	exports["externalsql"]:AsyncQueryCallback({
		query = "SELECT * FROM `characters` WHERE `playerid` = :playerid",
		data = {playerid = results.playerid}
	}, function(characters)
	local characters = characters["data"]
	
	TriggerClientEvent("DRP_ID:OpenMenu", source, characters)
	end)
end)
```

### DRP_ID:OpenVehicleList

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | [characterVehicles] | Show the [characterVehicles] from the character selection screen |

**example**: 
```lua
exports["externalsql"]:AsyncQueryCallback({
	query = "SELECT * FROM `vehicles` WHERE `char_id` = :character_id",
	data = {character_id = 1}
}, function(charactervehicle)
	local data = charactervehicle["data"]
	
	TriggerClientEvent('DRP_ID:OpenVehicleList', source, data)
end)
```

### DRP_ID:SpawnSelection

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | [ped] [spawn] | Open the spawn selection menu for the specific [ped] with the last [spawn] location |

**example**: 
```lua
exports["externalsql"]:AsyncQueryCallback({
	query = "SELECT * FROM `characters` WHERE `id` = :character_id",
	data = {character_id = 1}
}, function(characterInfo)
	local lastKnownLocation = json.decode(characterInfo["data"][1].lastLocation)
	table.insert(character, {id = src, charid = character_id, playerid = characterInfo.data[1].playerid, gender = characterInfo.data[1].gender, name = characterInfo.data[1].name, age = characterInfo.data[1].age})
		CloseAllCameras(source)
		
		TriggerClientEvent("DRP_ID:SpawnSelection", source, "mp_m_freemode_01", lastKnownLocation)		
	end)
end)
```

### DRP_ID:UpdateMenuCharacters

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | [characters] | Update the character selection menu with the [characters] of the player |

**example**: 
```lua
TriggerEvent("DRP_Core:GetPlayerData", source, function(results)
	exports["externalsql"]:AsyncQueryCallback({
		query = "SELECT * FROM `characters` WHERE `playerid` = :playerid",
		data = {playerid = results.playerid}
	}, function(characters)
		local characters = characters["data"]

		TriggerClientEvent("DRP_ID:UpdateMenuCharacters", player, characters)
	end)
end)
```

### sendProximityMessageMe

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | [id] [name] [message] | Send a [message] from the player [id] with the [name] to other players if they are close enough |

**example**: 
```lua
local character = GetCharacterData(source)
TriggerClientEvent("sendProximityMessageMe", -1, source, character.name, "This is a proximity message")
```

### sendProximityMessageRoll

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | [id] [name] [num] | Send a dice roll result: [num], from the player [id] with the [name] to other players if they are close enough |

**example**: 
```lua
local character = GetCharacterData(src)
num = math.random(1,6)
TriggerClientEvent("sendProximityMessageRoll", -1, source, character.name..num)
```

### sendProximityShowId

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_id | [id] [name] [message] | Send the player [id] with the [name], and a [message] to other players if they are close enough |

**example**: 
```lua
local character = GetCharacterData(source)
TriggerClientEvent("sendProximityShowId", -1, source, "^3ID:^0 Name: "..character.name.., "Gender: "..character.gender..", Age: "..character.age.. ", Temp County No: "..character.id..", CID: "..character.charid)
```

## drp_LegacyFuel

### fuel:removeFuelorAddPetrolcan

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_LegacyFuel | [vehicle] | Set the fuel level of the [vehicle] to the previously registered one |

> If vehicle is set to false will give petrol can to the player or refill it

**example**: 
```lua
TriggerClientEvent("fuel:removeFuelorAddPetrolcan", source, vehicle)
```

## drp_notifications

### DRP_Core:CustomIcon

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_notifications | [title] [body] [time] [iconFile] [showBar] [pos] | Show a notification with a [title] a [body] and a local [iconFile] during a certain [time] on a certain [pos]ition on the screen |

> [showBar] is a boolean and allow a progress bar to be shown on the notif, showing how much [time] is left before the notification disappear

**example**: 
```lua
TriggerClientEvent("DRP_Core:CustomIcon", source, "Example", tostring("This is a notif with a local icon file"), 2500, "./customPath/icon.png", true, "leftCenter")
```

### DRP_Core:CustomURLIcon

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_notifications | [title] [body] [time] [url] [showBar] [pos] | Show a notification with a [title] a [body] and a custom icon with the [url] during a certain [time] on a certain [pos]ition on the screen |

> [showBar] is a boolean and allow a progress bar to be shown on the notif, showing how much [time] is left before the notification disappear

**example**: 
```lua
TriggerClientEvent("DRP_Core:CustomURLIcon", source, "Example", tostring("This is a notif with a custom icon URL"), 2500, "https://customURL/icon.png", true, "leftCenter")
```

### DRP_Core:Error

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_notifications | [title] [body] [time] [showBar] [pos] | Show an error notification with a [title] and a [body] during a certain [time] on a certain [pos]ition on the screen |

> [showBar] is a boolean and allow a progress bar to be shown on the notif, showing how much [time] is left before the notification disappear

**example**: 
```lua
TriggerClientEvent("DRP_Core:Error", source, "Example", tostring("This is an error notif"), 2500, true, "leftCenter")
```

### DRP_Core:Info

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_notifications | [title] [body] [time] [showBar] [pos] | Show a success notification with a [title] and a [body] during a certain [time] on a certain [pos]ition on the screen |

> [showBar] is a boolean and allow a progress bar to be shown on the notif, showing how much [time] is left before the notification disappear

**example**: 
```lua
TriggerClientEvent("DRP_Core:Info", source, "Example", tostring("This is an info notif"), 2500, true, "leftCenter")
```

### DRP_Core:Success

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_notifications | [title] [body] [time] [showBar] [pos] | Show a success notification with a [title] and a [body] during a certain [time] on a certain [pos]ition on the screen |

> [showBar] is a boolean and allow a progress bar to be shown on the notif, showing how much [time] is left before the notification disappear

**example**: 
```lua
TriggerClientEvent("DRP_Core:Success", source, "Example", tostring("This is a success notif"), 2500, true, "leftCenter")
```

### DRP_Core:Warning

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_notifications | [title] [body] [time] [showBar] [pos] | Show a success notification with a [title] and a [body] during a certain [time] on a certain [pos]ition on the screen |

> [showBar] is a boolean and allow a progress bar to be shown on the notif, showing how much [time] is left before the notification disappear

**example**: 
```lua
TriggerClientEvent("DRP_Core:Warning", source, "Example", tostring("This is a warning notif"), 2500, true, "leftCenter")
```

## drp_soda

### DRP_Soda:getSoda

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_soda | none | Give the player a soda |

**example**: 
```lua
TriggerClientEvent("DRP_Soda:getSoda", source)
```

## drp_tattoos

### DRP_Tattoos:BoughtSuccess

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_tattoos | [value] | Insert the tattoos [value] to the ped's tattoo list |

**example**: 
```lua
TriggerClientEvent("DRP_Tattoos:BoughtSuccess", source, "MP_Bea_F_Chest_000")
```

### DRP_Tattoos:CharacterTattoos

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_tattoos | [playerTattoosList] | Apply the [playerTattoosList] to the player's ped |

**example**: 
```lua
local character = exports["drp_id"]:GetCharacterData(source)
exports["externalsql"]:AsyncQueryCallback({
	query = "SELECT * FROM `character_tattoos` WHERE `char_id` = :charid",
	data = {charid = character.charid}
}, function(tattoosResults)
	if(json.encode(tattoosResults["data"]) ~= "[]") then
		allTattoos = json.decode(tattoosResults["data"][1].tattoos)
		
		TriggerClientEvent("DRP_Tattoos:CharacterTattoos", src, allTattoos)
	else
		local tattooValue = json.encode({})
		exports["externalsql"]:AsyncQueryCallback({
			query = "INSERT INTO `character_tattoos` SET `tattoos` = :tattoos, `char_id` = :charid",
			data = {
				tattoos = tattooValue,
				charid = character.charid
			}
		}, function(yeet)
		
			TriggerClientEvent("DRP_Tattoos:CharacterTattoos", src, {})
		end)
	end
end)
```

### DRP_Tattoos:OpenMenu

| DRP script| Arguments | Description |
| :---: | :---: | :--- |
| drp_tattoos | none | Open the tattoos menu |

**example**: 
```lua
TriggerClientEvent("DRP_Tattoos:OpenMenu", source)
```