# Xiphs_MCBEDS_Tools
Unofficial Minecraft Bedrock Edition Dedicated Server Management Tools

Xiph's Minecraft Bedrock Edition Dedicated Server Management Tools is a collection of shell scripts intended to automate and simplify the running and management of Mojang's Minecraft Bedrock Edition Dedicated Server for Linux.
This project and the provided scripts are not in any way affiliated, provided by, or otherwise endorsed by Mojang, Microsoft, or anyone involved with Minecraft, Minecraft Java Edition, or Minecraft Bedrock Edition. These scripts are created for my own use, and provided as-is in the event they may prove useful to others.

Currently, the publically available tools are:

## mcbeds_mgr
mcbeds_mgr - A BASH wrapper script to provide a UNIX socket for daemonizing and controlling, starting, stopping, and updating the Minecraft Bedrock Edition Dedicated Server. The behavior is controlled via a set of flags, or dependednt on how the script is called:

If run as "mcbeds_start" an instance of the server located at ${SERVER} is started, and UNIX socket at ${SERVER}/${PORT} is created to pass in commands and return results.

If run as "mcbeds_stop" the server located at ${SERVER} broadcasts a 1-hour, 30 minute, 15 minute, 10 minute, 5 minute, and 1 minute warning to players in-game, then the server is stopped.

If run as "mcbeds_update" the script checks for any available updates to the software. If an update is found, it is downloaded, then a warning of the impending uipdate is broadcast to players at 1 hour, 30 minutes, 15 minutes, 10 minutes, 5 minutes, and one minute before the server is stopped and restarted.

The script checks three locations for runtime command files: /etc/mcbeds.rc, /usr/local/etc/mcbeds.rc, and ${HOME}/.mcbedsrc. This file should contain at a minimum an entry for SERVER that defines the path to the install directory of the Minecraft server. Full contents are:
SERVER=/Path/to/server
PORT=UNIX_Socket_File_to_use (defaults to 12011)
LOG=/Path/to/where/logs/should/be/written (defaults to ${SERVER}/mcbeds.log)
DOWNLOAD=/Path/to/where/server/updates/should/be/downloaded (defaults to ${HOME}/Downloads)
BASE_URL='https://url.to/minecraft/bedrock/dedicated/server/repository' - there should never be any reason to change this unless Mojang switches up where they store the distribution, or you want to use a specific mirror.

The script, regardless of how it is called, accepts the following flags:

-h    Print a usage summary and exit

-r    Start the server  
-s    Stop the server  
-u    Update the server  
-D    The DOWNLOAD directory to use for downloading and tracking the server version  
-L    Specify the name of the log file to write to  
-M    A reason for shutdown to broadcast to players (if -N not specified)  
-N    Override any server shutdown timing and stop the server NOW  
-P    The UNIX socket to listen on in ${SERVER}/  
-S    Specify the SERVER directory to manage on the command line, overriding what is in /etc/mcbeds.rc, /usr/local/etc/mbeds.rc and ${HOME}/.mcbedsrc  

## mcbeds.service
A Systemd service file that will allow managing Minecraft from Systemd. Provides for start, stop (immediate), and restarting in the event of a server crash or update restart.

Assumes a user "minecraft" exists, that the server runs from within this user's home directory, and that mcbeds_run and mcbeds_stop are symbolically linked to mcbeds_mgr in /usr/local/sbin/ 

## mcbeds.init
A SyetmV init script, for those who prefer init over Systemd. Provides for start, stop (immediate), and restarting the server.

Assumes a user "minecraft" exists, that the server runs from within this user's home directory, and that mcbeds_run and mcbeds_stop are symbolically linked to mcbeds_mgr in /usr/local/sbin/ 
