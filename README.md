# LibTotemInfo-1.0
A compatible implementation of `GetTotemInfo()` API for WoW Classic 1.13.3.


## Desc
You should know that Blizzard removed the totem information API from Wow Classic 1.13.3, which caused many totem timers to not work.

I created a simple addon and restored one of the APIs (`GetTotemInfo`). In this way most totem timers can work normally.

The code from [RotationMaster](https://git.neuromancy.net/projects/RM/repos/rotationmaster/browse/fake.lua?until=a0a2fc3bdfb5fa8199f14d66bd22666258f67aa4&untilPath=fake.lua) by PreZ and edited / fixed by SwimmingTiger.


## Usage

Download [LibTotemInfo-1.0.x.zip](https://github.com/SwimmingTiger/LibTotemInfo/releases) and put it in your `World of Warcraft\_classic_\Interface\Addons\!LibTotemInfo` folder. Please note the leading `!`, it is to make it load earlier than other addons. Don't rename it.

And, if you get the folder `LibTotemInfo-master`, you can rename it to`!LibTotemInfo` (This folder will appear when you download the repository ZIP directly. It is recommended to download the zip in [the Release page](https://github.com/SwimmingTiger/LibTotemInfo/releases)) or keep the current name. The latest version of the addon folder can be named under the following two names:
* `!LibTotemInfo`
* `LibTotemInfo-master`

Then it should be in the addon list and displayed as `Lib: TotemInfo-1.0`. Enable it, and your totem timer will work again.

![AddOn List](https://user-images.githubusercontent.com/4986069/70845656-49c31d80-1e8c-11ea-8c72-a6554110acbb.jpg)


### Verified working addons without modification
* NugRunning
  <br>(The latest version of NugRunning has LibTotemInfo embedded and no longer needs to be installed separately.)
* TotemTimers `1.06-classic`
* SamyTotemTimers `v2.6`
* PitBull4 `v4.1.21`

![Totem timer works](https://user-images.githubusercontent.com/4986069/70828913-57928780-1e27-11ea-9faf-c51fb934fadb.gif)


## For AddOn Developer

You can embed the project, just like this:

### your-addon.toc
```toc
libs\!LibTotemInfo\embeds.xml
your-file.lua
```

### your-file.lua
```lua
local GetTotemInfo = LibStub("LibTotemInfo-1.0").GetTotemInfo
for i =1, 4 do
    print(GetTotemInfo(i))
    print(GetTotemTimeLeft(i))
end
```

### The Global API

When `GetTotemInfo` does not exist, the library will register `GetTotemInfo` as its own implementation. So addons that rely on `GetTotemInfo` can use this function directly, without having to instantiate it from LibStub.

Interfaces currently implemented:

```lua
-- Added return value by the lib (not in Blizzard old interface):
--     spellid - int, the totem's spell id.
--     rank    - int (1 to 8) or nil, the rank of the totem spell.
--               nil indicates that there is no rank for this totem.
haveTotem, totemName, startTime, duration, icon, spellid, rank = GetTotemInfo(1 through 4)

timeLeft = GetTotemTimeLeft(1 through 4)
```

See details at https://wow.gamepedia.com/API_GetTotemInfo


## License

Inherited the Apache License Version 2.0 from the [Rotation Master](https://www.curseforge.com/wow/addons/rotation-master) project.
