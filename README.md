# Xiphs_MCBEDS_Tools
Unofficial Minecraft Bedrock Edition Dedicated Server Management Tools

Xiph's Minecraft Bedrock Edition Dedicated Server Management Tools is a collection of shell scripts intended to automate and simplify the running and management of Mojang's Minecraft Bedrock Edition Dedicated Server for Linux.
This project and the provided scripts are not in any way affiliated, provided by, or otherwise endorsed by Mojang, Microsoft, or anyone involved with Minecraft, Minecraft Java Edition, or Minecraft Bedrock Edition. These scripts are created for my own use, and provided as-is in the event they may prove useful to others.

Currently, the publically available tools are:

run_mcbeds - Simple BASH wrapper script to provide a UNIX socket for daemonizing and controlling the Minecraft Bedrock Edition Dedicated Server

update_server - Intended to be run as part of a cronjob, checks the currently installed version of Minecraft Bedrock Dedicated Server against the currently available version, installing updates as they are detected. Includes the ability to warn logged in players of the impending update, with variable intervals and warnings; cleanly stops the server before upgrading; protects existing whitelists, permissions, and server properties from being clobbered by updates
