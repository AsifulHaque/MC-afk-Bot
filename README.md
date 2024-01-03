# Afk Bot
<p align="center"> 
    <img src="https://img.shields.io/github/issues/urfate/afk-bot">
    <img src="https://img.shields.io/github/forks/urfate/afk-bot">
    <img src="https://img.shields.io/github/stars/urfate/afk-bot">
    <img src="https://img.shields.io/github/license/urfate/afk-bot">
</p>

<p align="center">
    Functional minecraft AFK bot for servers
</p>

<p align="center">
    Anti-AFK, Auto-Auth, Microsoft/Offline accounts support.
</p>

## Installation

 1. [Download](https://github.com/urFate/Afk-Bot/tags) the latest package.
 2. Download & install [Node.JS](https://nodejs.org/en/download/)
 3. Run `npm install` command in bot directory.
 
 ## Usage
 
 1. Configure bot in `settings.json` file. [Bot configuration is explained in our wiki](https://urfate.gitbook.io/afk-bot/bot-configuration)
 2. Start bot with `node .` command.

## Features

 - Anti-AFK Kick Module
 - Move to target block after join
 - Mojang/Microsoft Account support
 - Chat log
 - Chat messages Module
 - Auto reconnect
 - Supported server versions: `1.8 - 1.19.3`. Use ViaVersion+ViaBackwards on the Server versions > 1.19.3

## Bug
 - Currently All Server messages (even during server kick) causes throwing an exception from framing.js which causes the bot to stop. Currently I have not found any solution to this as my knowledge of working with NodeJS is very low. Only workaround I found is to to remove the chat formatting functions alltogether (which sadly disables all chat features):
 ### Step 1 : Replace the line in *node_modules\minecraft-protocol\src\transforms\framing.js*
 Replace
 > throw e; 
 with 
 > console.log("Error: Throw e at Farming.js:67");
 This does not stop the error, and bot disconnects after *'keepalive timeout'*, but does not entirely stop the bot(program) so it can reconnect again after specified delay.
 ### Step 2 : Comment/Remove some lines in node_modules\prismarine-chat\index.js
 Step 1 only fixes the fullstoping of the bot, but does nothing to stop the disconnect. Though due to reconnection feature the bot can safely reconnect again, but everytime someone sends a msg in chat, this happens which is annoying. To stop this only thing we can do for now is to ignore the chat & chat formatting altogether. For this:
 > Comment almost entire function *static fromNetwork (type, params)* leaving only the first line
 > At the last line (of **this** function i.e. *static fromNetwork (type, params)* ), return an empty/dummy str, like this: *return ''* or *return ''* 

 Now bot will not recieve any chat exept for an empty string. On the bright side, it will not abrupty disconnect/stop when someone types something in chat.

 Since this framing.Js file is inside node_modules which is dynamically generated, the changes for this *"workaround"* are not tracked by git. This needs to be done every time a project is created **after** *npm install* is done.

 ### License
 [MIT](https://github.com/urFate/Afk-Bot/blob/main/LICENSE)

