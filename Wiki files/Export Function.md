
# Export Functions

Following you will find all the exported functions, and their descriptions, that are currently in use inside the DRP-Framework. For better looking they are in alphabetical order by DRP-scripts.

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| Where the function is | Argument(s) it needs | If server or client sided | Brief description of the function |

## Contents

- [externalSQL](https://github.com/OfficialDarkzy/DRP-Core/wiki/Export-Functions#externalsql)
    - AsyncQuery
    - AsyncQueryCallback
- [drp_core](https://github.com/OfficialDarkzy/DRP-Core/wiki/Export-Functions#drp_core)
    - DoesRankHavePerms
    - drawText
    - DrawText3Ds
	- GetClosestPlayer
	- GetPlayers
    - GetPlayerData
	- print_table
- [drp_death](https://github.com/OfficialDarkzy/DRP-Core/wiki/Export-Functions#drp_death)
    - isPedDead
- [drp_id](https://github.com/OfficialDarkzy/DRP-Core/wiki/Export-Functions#drp_id)
    - GetCharacterData
    - GetCharacterName
    - SpawnedInAndLoaded
- [drp_garages](https://github.com/OfficialDarkzy/DRP-Core/wiki/Export-Functions#drp_jobcore)
	- GetVehicleInFront
	- SpawnJobVehicle
    - UpdateVehicle
- [drp_jobcore](https://github.com/OfficialDarkzy/DRP-Core/wiki/Export-Functions#drp_jobcore)
    - DoesJobExist
	- GetJobLabels
    - GetPlayerJob
    - RequestJobChange
- [drp_LegacyFuel](https://github.com/OfficialDarkzy/DRP-Core/wiki/Export-Functions#drp_legacyfuel)
    - GetFuel
    - SetFuel
- [drp_progressBars](https://github.com/OfficialDarkzy/DRP-Core/wiki/Export-Functions#drp_progressbars)
    - startUI

## externalSQL

### AsyncQuery

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| externalsql | [queryData] | server | Perform a specific query with the [queryData] |

**example**: 
```lua
exports['externalsql']:AsyncQuery({
    query = "UPDATE `users` SET `name`=:name WHERE `id` = :id",
    data = { id = 1, name = "John Doe" }
})
```

### AsyncQueryCallback

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| externalsql | [queryData] [callback] | server | Perform a specific query with the [queryData] and release a useable [callback] |

**example**: 
```lua
exports['externalsql']:AsyncQueryCallback({
    query = "SELECT * FROM `characters` WHERE `playerid` = :playerid",
    data = { playerid = 1 }
}, function(characters)
    *a function*
end)
```

## drp_core

### DoesRankHavePerms

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_core | [rank] [perm] | server | Return a boolean value stating if the [rank] have the required [perm] |

> [perm] are configured inside the config.lua file in drp_core folder

**example**: 
```lua
local player =  GetPlayerData(source)
if exports['drp_core']:DoesRankHavePerms(player.rank, perm) then
    *do something*
end
```

### drawText

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_core | [text] [x] [y] | client | Show a [text] on a specific location [x, y] on the screen |

**example**: 
```lua
exports['drp_core']:drawText("This is a message", 0, 0)
```

### DrawText3Ds

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_core | [x] [y] [z] [text] | client | Draw a 3D [text] on a specific location [x, y, z] |

**example**: 
```lua
local coords =  GetEntityCoords(GetPlayerPed(source), false)
exports['drp_core']:DrawText3Ds(coords['x'], coords['y'], coords['z'] + 0.5, "This is a message")
```

### GetClosestPlayer

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_core | none | client | Return the closest player and its position |

**example**: 
```lua
local player, distance = exports['drp_core']:GetClosestPlayer()
TriggerClientEvent("chatMessage", source, tostring("^2The closest player is: ^1"..player.name.." at a distance of "..distance))
```

### GetPlayers

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_core | none | client | Return tan array of the active player |

**example**: 
```lua
local players = exports['drp_core']:GetPlayers()
for each _, player in ipairs(players) do
	TriggerClientEvent("chatMessage", source, tostring("^2The name of the player is: ^1"..player.name))
end
```

### GetPlayerData

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_core | [id] | server | Return the full player [id] data |

**example**: 
```lua
local player = exports['drp_core']:GetPlayerData(source)
TriggerClientEvent("chatMessage", source, tostring("^2Your Permission Rank is: ^1"..player.rank))
```

### print_table

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_core | [node] | client | Print the [node] table |

**example**: 
```lua
WIP
```

## drp_death

### isPedDead

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_death | none | client | Return a boolean value, showing if the player is dead or not |

**example**: 
```lua
if not exports['drp_death']:isPedDead() then
    *do something*
end
```

## drp_id

### GetCharacterData

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_id | [id] | server | Return the full character [id] data |

**example**: 
```lua
local character = exports['drp_id']:GetCharacterData(source)
TriggerClientEvent("chatMessage", source, tostring("^2Your Character ID is: ^1"..character.charid))
```

### GetCharacterName

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_id | [id] | server | Return the character [id] name |

**example**: 
```lua
local name = exports['drp_id']:GetCharacterName(source)
TriggerClientEvent("chatMessage", source, tostring("^2Your Character name is: ^1"..name))
```

### SpawnedInAndLoaded

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_id | none | client | Return a boolean value stating if the character is already spawned or not |

**example**: 
```lua
if exports['drp_id']:SpawnedInAndLoaded() then
    *do something*
end
```

## drp_garages

### UpdateVehicle

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_garages | none | client | Get the vehicle in front of the player |

**example**: 
```lua
local vehicleFront = GetVehicleInFront()
if vehicleFront ~= 0 then
	*do something*
end
```

### GetVehicleInFront

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_garages | [vehicle] [plate] [spawnPointx] [spawnPointy] [spawnPointz] [spawnPointh] [fuelLevel] | client | Spawn the [vehicle] with the [plate] to the [spawnpoint] with a certain [fuelLevel] |

**example**: 
```lua
WIP
```

### UpdateVehicle

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_garages | [veh] | client | Update the data of the [veh] |

**example**: 
```lua
WIP
```

## drp_jobcore

### DoesJobExist

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_jobcore | [job] | server | Return a boolean statting if the [job] exists or not |

> Jobs are set inside the config.lua file in the drp_jobcore folder

**example**: 
```lua
if exports['drp_jobcore']:DoesJobExist("UNEMPLOYED") then
    *do something*
end
```

### GetJobLabels

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_jobcore | [job] | server | Get the [job] label |

**example**: 
```lua
local jobLabel = exports['drp_jobcore']:GetPlayerJob(job)
TriggerClientEvent("chatMessage", source, tostring("^2Your current Job name is: ^1"..jobLabel))
```

### GetPlayerJob

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_jobcore | [player] | server | Get the [player] job |

**example**: 
```lua
local job = exports['drp_jobcore']:GetPlayerJob(source)
TriggerClientEvent("chatMessage", source, tostring("^2Your current Job is: ^1"..job.jobLabel))
```

### RequestJobChange

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_jobcore | [source] [job] [label] [otherData] | server | Make a player [source] under the a specific [job] with a [label] |

> [label] is the name of the job that the player will see and is set inside the drp_jobcore config.lua file

**example**: 
```lua
local job = "UNEMPLOYED"
local jobLabel = JobsCoreConfig.StaticJobLabels[job]
exports['drp_jobcore']:SetPlayerJob(source, job, jobLabel, false)
```

## drp_LegacyFuel

### GetFuel

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_LegacyFuel | [vehicle] | client | Return the amount of fuel inside a [vehicle] |

**example**: 
```lua
local playerPed=  PlayerPedId()
local vehicle = GetVehiclePedIsIn(playerPed, false)
local fuel_level = exports['drp_LegacyFuel']:GetFuel(vehicle)
TriggerClientEvent("chatMessage", source, tostring("^2Your Car fuel level is: ^1"..fuel_level))
```

### SetFuel

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_LegacyFuel | [vehicle] [fuel] | client | Set the amount of [fuel] inside a [vehicle] |

**example**: 
```lua
local playerPed=  PlayerPedId()
local vehicle = GetVehiclePedIsIn(playerPed, false)
exports['drp_LegacyFuel']:SetFuel(vehicle, 100)
```

## drp_progressBars

### startUI

| DRP script| Arguments | Export type | Description |
| :---: | :---: | :---: |:--- |
| drp_progressBars | [time] [text] | client | Show a progressbar with the specified [time] and [text] |

**example**: 
```lua
exports['drp_progressBars']:startUI(10000, "I am a text")
```