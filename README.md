# LibTotemInfo-1.0
A compatible implementation of `GetTotemInfo()` API for WoW Classic 1.13.3.


## Desc
You should know that Blizzard removed the totem information API in Wow Classic, which caused many totem timers to not work.

I created a simple addon and restored one of the APIs (`GetTotemInfo`). In this way most totem timers can work normally.

The code from [RotationMaster](https://git.neuromancy.net/projects/RM/repos/rotationmaster/browse/fake.lua?until=a0a2fc3bdfb5fa8199f14d66bd22666258f67aa4&untilPath=fake.lua) and edited / fixed by SwimmingTiger.


## Usage

Put it in your _classic_\Interface\AddOns folder and open the game. Your totem timer should work properly.


## For AddOn Developer

You can embed the project, just like this:

### your-addon.toc
```
libs\!LibTotemInfo\embeds.xml
your-file.lua
```

### your-file.lua
```
local GetTotemInfo = LibStub("LibTotemInfo-1.0").GetTotemInfo
for i =1, 4 do
    print(GetTotemInfo(i))
end
```

### The Global API

When `GetTotemInfo` does not exist, the library will register `GetTotemInfo` as its own implementation. So addons that rely on `GetTotemInfo` can use this function directly, without having to instantiate it from LibStub.

Interfaces currently implemented:

```
haveTotem, totemName, startTime, duration, icon = GetTotemInfo(1 through 4)
```

See details at https://wow.gamepedia.com/API_GetTotemInfo
