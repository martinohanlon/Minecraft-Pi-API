#Minecraft Pi API

IN PROGRESS

##Description
The Minecraft Pi API is a 'server' based api where a client connects to a server and sends api command via TCP/IP. Each command is a string sent in clear text to the server which then executes that command.

Some of the information presented here is taken from the original (mcpi_protocol_spec.txt)[resources/mcpi_protocol_spec.txt] document which was distributed with Minecraft: Pi Edition

##Implementations

TODO - descriptions of the implementations

##Protocol
The mcpi-protocol enables an external process (program) to interact with a running instance of Minecraft Pi API.

The protocol can easily be implemented and used from any programming language that has network socket support. 

* Tcp-socket, port 4711 (in some implementations this can be changed)
* Commands are clear text lines (ASCII, LF terminated)

##Definitions
x,y,z -- vector of three integers.
xf,yf,zf -- vector of three floats.
blockTypeId -- integer. 0 is air.
blockData -- integer 0-15. Block data beyond the type, for example wool color.

##Co-ordinate System
Most coordinates are in the form of a three integer vector (x,y,z) which address a specific tile in the game world. (0,0,0) is the spawn point sea level. (X,Z) is the ground plane and Y is towards the sky.

##Commands

Commands are categorised by their status as:
* Official - part of the Minecraft: Pi Edition api and officially support by Mojang
* Standard - implementated generally across implementations considered to be in line with the ethos and structure of the api
* Extension - perhaps only implemented in one implementation, or there to deliver a specific requirement, or likely to change, or not appropriate for all implementations

If changes are made to the official implementation which supercede standard or extention functions it is expected that they will be removed.

No all commands are supported in all implementations, see the compatability table below.

###Official

world.getBlock(x,y,z) --> blockTypeId

world.setBlock(x,y,z,blockTypeId)
world.setBlock(x,y,z,blockTypeId,blockData)

world.setBlocks(x1,y1,z1,x2,y2,z2,blockTypeId)
world.setBlocks(x1,y1,z1,x2,y2,z2,blockTypeId,blockData)

world.getHeight(x,z) --> Integer

world.checkpoint.save()
world.checkpoint.restore()

world.setting(KEY,0/1)

world.getPlayerIds()

chat.post(message)

camera.mode.setNormal()
camera.mode.setThirdPerson()
camera.mode.setFixed()
camera.mode.setPos(x,y,z)

player.getTile() --> x,y,z
player.setTile(x,y,z)

player.getPos() --> xf,yf,zf
player.setPos(xf,yf,zf)

player.setting(KEY, 0/1)

entity.getTile(entityId) --> x,y,z
entity.setTile(entityId,x,y,z)

entity.getPos(entityId) --> xf,yf,zf
entity.setPos(entityId,xf,yf,zf)

events.block.hits() --> [pos,surface,entityId]
(pos is x,y,z surface is Integer, entityId is Integer)

###Standard

world.getBlocks --> [blockType]

world.getPlayerId(name) --> Integer

player.getDirection() --> xf, yf, zf
player.getRotation() --> Float
player.getPitch() --> Float

entity.getDirection(entityId) --> xf, yf, zf
entity.getRotation(entityId) --> Float
entity.getPitch(entityId) --> Float

events.chat.posts() --> [entityId,mesage]

###Extension

world.spawnEntity(type,x,y,z,tags) --> entityId
world.removeEntity(entityId)

##Compatability
O - Official
S - Standard
E - Extension

Command | O/S/E | Minecraft: Pi | Raspberry Juice | Raspberry Jam Mod | mcapi
--- | --- | --- | --- | --- |--- 
world.getBlock | O | Y | Y | Y | Y
world.setBlock | O | Y | Y | Y | Y
world.setBlock | O | Y | Y | Y | Y
world.setBlocks | O | Y | Y | Y | Y
world.setBlocks | O | Y | Y | Y | Y
world.getHeight | O | Y | Y | Y | Y
world.checkpoint.save | O | Y | N | N | N
world.checkpoint.restore | O | Y | N | N | N
world.setting | O | Y | N | N | N
world.getPlayerIds | O | Y | Y | N | N
world.getBlocks | S | N | Y | Y | Y
world.getPlayerId(name) | S  | N | Y | N | N
chat.post | O | Y | Y | Y | Y
camera.mode.setNormal | O | Y | N | Y | Y
camera.mode.setThirdPerson | O | Y | N | Y | Y
camera.mode.setFixed | O | Y | N | Y | Y
camera.mode.setPos | O | Y | N | N | N
player.getTile | O | Y | Y | Y | Y
player.setTile | O | Y | Y | Y | Y
player.getPos | O | Y | Y | Y | Y
player.setPos | O | Y | Y | Y | Y
player.setting | O | Y | N | N | N
player.getDirection | S | N | Y | Y | Y
player.getRotation | S | N | Y | Y | Y
player.getPitch | S | N | Y | Y | Y
player.setDirection | S | N | N | Y | N
player.setRotation | S | N | N | Y | N
player.setPitch | S | N | N | Y | N
entity.getTile | O | Y | Y | Y | Y
entity.setTile | O | Y | Y | Y | Y
entity.getPos | O | Y | Y | Y | Y
entity.setPos | O | Y | Y | Y | Y
entity.getDirection | S | N | Y | Y | Y
entity.getRotation | S | N | Y | Y | Y
entity.getPitch | S | N | Y | Y | Y
entity.setDirection | S | N | N | Y | N
entity.setRotation | S | N | N | Y | N
entity.setPitch | S | Y | Y | Y | N
events.block.hits | O | Y | Y | Y | Y
events.chat.posts | S | N | Y | Y | N
world.spawnEntity | E | N | N | Y | N
world.removeEntity | E | N | N | Y | N