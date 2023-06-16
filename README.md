# Growtopia-Multibot-Lua
Fully working don't pay for AutoFarm app

## Error
```lua

Unzip rar in Vendor
```

## FindItem
```lua

function FindItem(id)
    for _, itm in pairs(GetInventory()) do
        if itm.id == id then
            return itm.amount
        end
    end
    return 0
end
```
## Plant
```lua

function plant()
    for _, tile in pairs(GetTiles()) do
        if tile.fg == 0 and GetTile(tile.x, tile.y + 1).fg ~= 0 and GetTile(tile.x, tile.y + 1).fg ~= itemid then
            FindPath(tile.x, tile.y)
            Sleep(50)
            Hit(0, 0, 3)
            Sleep(500)
        end
    end
end
```
## Harvest
```lua

function harvest()
    for _, tile in pairs(GetTiles()) do
        if tile.fg == 3 then
            FindPath(tile.x, tile.y)
            Sleep(500)
            Hit(0, 0, 18)
            Sleep(200)
            Collect(3)
            if FindItem(2) > 50 or FindItem(2) == 55 then
                return true
            end
        end
    end
    return false
end
```

## Break
```lua

function bbreak()
    while FindItem(2) > 0 do
        Hit(1, -2, 2)
        Sleep(dplace)
        Hit(1, -1, 2)
        Sleep(dplace)
        Hit(1, 0, 2)
        Sleep(dbreak)
        for i = 1, 3 do
            Hit(1, -2, 18)
            Sleep(dbreak)
        end
        for i = 1, 3 do
            Hit(1, -1, 18)
            Sleep(dbreak)
        end
        for i = 1, 3 do
            Hit(1, 0, 18)
            Sleep(dbreak)
        end
        if FindItem(2) == 1 or FindItem(2) < 2 then
            if harvest() then
                break
            end
        end
    end
end
```

