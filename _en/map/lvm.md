---
title: Lua Voxel Manipulators
layout: default
root: ../..
idx: 3.4
description: Learn how to use LVMs to speed up map operations.
redirect_from: /en/chapters/lvm.html
---

## Introduction

The functions outlined in the [Basic Map Operations](environment.html) chapter
are easy to use and convenient, but for large areas they are not efficient.
Every time you call `set_node` or `get_node` your mod needs to communicate with
the engine, which results in copying. Copying is slow, and will quickly kill the
performance of your game.

* [Concepts](#concepts)
* [Reading into the LVM](#reading-into-the-lvm)
* [Reading Nodes](#reading-nodes)
* [Writing Nodes](#writing-nodes)
* [Example](#example)
* [Your Turn](#your-turn)

## Concepts

Creating a Lua Voxel Manipulator allows you to load large areas of the map into
your mod's memory at once. You can then read and write to this data without
interacting with the engine at all or running any callbacks, which means that
these operations are very fast. Once done, you can then write the area back into
the engine and run any lighting calculations.

## Reading into the LVM

You can only load a cubic area into an LVM, so you need to work out the minimum
and maximum positions that you need to modify. Then you can create and read into
an LVM like so:

```lua
local vm         = minetest.get_voxel_manip()
local emin, emax = vm:read_from_map(pos1, pos2)
```

An LVM may not read exactly the area you tell it to, for performance reasons.
Instead, it may read a larger area. The larger area is given by `emin` and `emax`,
which stand for *emerged min pos* and *emerged max pos*. An LVM will load the area
it contains for you - whether that involves loading from memory, from disk, or
calling the map generator.

## Reading Nodes

To read the types of nodes at particular positions, you'll need to use `get_data()`.
`get_data()` returns a flat array where each entry represents the type of a
particular node.

```lua
local data = vm:get_data()
```

You can get param2 and lighting data using the methods `get_light_data()` and `get_param2_data()`.

You'll need to use `emin` and `emax` to work out where a node is in the flat arrays
given by the above methods. There's a helper class called `VoxelArea` which handles
the calculation for you:

```lua
local a = VoxelArea:new{
    MinEdge = emin,
    MaxEdge = emax
}

-- Get node's index
local idx = a:index(x, y, z)

-- Read node
print(data[idx])
```

If you run that, you'll notice that `data[vi]` is an integer. This is because
the engine doesn't store nodes using their name string, as string comparision
is slow. Instead, the engine uses a content ID. You can find out the content
ID for a particular type of node like so:

```lua
local c_stone = minetest.get_content_id("default:stone")
```

and then you can check whether a node is stone like so:

```lua
local idx = a:index(x, y, z)
if data[idx] == c_stone then
    print("is stone!")
end
```

It is recommended that you find out and store the content IDs of nodes types
using load time, as the IDs of a node type will never change. Make sure to store
the IDs in a local for performance reasons.

Nodes in an LVM data are stored in reverse co-ordinate order, so you should
always iterate in the order of `z, y, x` like so:

```lua
for z = min.z, max.z do
    for y = min.y, max.y do
        for x = min.x, max.x do
            -- vi, voxel index, is a common variable name here
            local vi = a:index(x, y, z)
            if data[vi] == c_stone then
                print("is stone!")
            end
        end
    end
end
```

The reason for this touches computer architecture. Reading from RAM is rather
costly, so CPUs have multiple levels of caching. If the data a process requests
is in the cache, it can very quickly retrieve it. If the data is not in the cache,
then a cache miss occurs so it'll fetch the data it needs from RAM. Any data
surrounding the requested data is also fetched and then replaces the data in the cache as
it's quite likely that the process will ask for data near there again. So a
good rule of optimisation is to iterate in a way that you read data one after
another, and avoid *memory thrashing*.

## Writing Nodes

First you need to set the new content ID in the data array:

```lua
for z = min.z, max.z do
    for y = min.y, max.y do
        for x = min.x, max.x do
            local vi = a:index(x, y, z)
            if data[vi] == c_stone then
                data[vi] = c_air
            end
        end
    end
end
```

When you finished setting nodes in the LVM, you then need to upload the data
array to the engine:

```lua
vm:set_data(data)
vm:write_to_map(true)
```

For setting lighting and param2 data, there are the appropriately named
`set_light_data()` and `set_param2_data()` methods.

`write_to_map()` takes a Boolean which is true if you want lighting to be
calculated. If you pass false, you need to recalculate lighting at some future
date using `minetest.fix_light`.

## Example

```lua
-- Get content IDs during load time, and store into a local
local c_dirt  = minetest.get_content_id("default:dirt")
local c_grass = minetest.get_content_id("default:dirt_with_grass")

local function grass_to_dirt(pos1, pos2)
    -- Read data into LVM
    local vm = minetest.get_voxel_manip()
    local emin, emax = vm:read_from_map(pos1, pos2)
    local a = VoxelArea:new{
        MinEdge = emin,
        MaxEdge = emax
    }    
    local data = vm:get_data()

    -- Modify data
    for z = pos1.z, pos2.z do
        for y = pos1.y, pos2.y do
            for x = pos1.x, pos2.x do
                local vi = a:index(x, y, z)
                if data[vi] == c_grass then
                    data[vi] = c_dirt
                end
            end
        end
    end

    -- Write data
    vm:set_data(data)
    vm:write_to_map(true)
end
```

## Your Turn

* Create `replace_in_area(from, to, pos1, pos2)` which replaces all instances of
  `from` with `to` in the area given, where from and to are node names.
* Make a function which rotates all chest nodes by 90&deg;.
* Make a function which uses an LVM to cause mossy cobble to spread to nearby
  stone and cobble nodes.
  Does your implementation cause mossy cobble to spread more than a distance of one each
  time? How could you stop this?
