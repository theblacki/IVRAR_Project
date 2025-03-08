+++
date = '2024-11-15T11:19:40+01:00'
draft = false
title = 'Week 3 - Project Start'
+++

# Project Start
This week I started on the actual project, though I did not yet get all that far.

## Roll-A-Ball VR
Since I've already had experience with working with Unity, I opted not to implement a Roll-A-Ball Game before. Not so for the XR Version though, so I imported the package provided and followed the instructions to get the VR integration running. I encountered no problems doing so.

Getting it running with Meta Quest Link also did not pose any problems. I decided that once I had some time, I'd try out playing some games on my Meta Quest 2.


## First scaffolding for the TRB
After getting the Roll-A-Ball VR integration working, I imported the base parkour for the project and tested how it works in its default state.

Following my concept, I created the game object for the TeleRollingBoard and added a new script for its behavior. Within, I created the pseudo code for the interactions I had planned, primarily the throwing, but also teleporting the player to the board, as well as teleporting the board back to the player (e.g. if they missed the throw).