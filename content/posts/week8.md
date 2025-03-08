+++
date = '2024-12-23T11:19:40+01:00'
draft = false
title = 'Week 8 - The Follow-after Feature and actual Visuals'
+++

# The Follow-after Feature and actual Visuals
The report presentation - or rather the discussion thereafter gave me some new ideas to work on, some of which I started on this week.

## Hand Poses
As mentioned in the presentation slides, I was inspired by the reverse classroom topic of another student and wanted to get hand poses for my TeleRollingBoard, meaning positions and orientations of the hands grabbing onto it.

As it turns out, those don't quite work when you use the controllers (visuals) - obviously - but I only thought of that after getting the creation of hand poses working - which differs heavily from how it was shown in the reverse classroom to the way it works now and with the Meta XR All-In-One Kit.

Well, another task for the backlog. For now, I had other features that were more important.

## The Follow-after Feature
One of the features suggested after the presentation was to have the player follow after the board trajectory after throwing instead of just teleporting to it. To make that happen I once again used a position queue of the board - a different one than that for the throwing mechanic as they behave differently.

The first implementation only made the player follow after the board on the ground (as in, the y-positions were all set to the player's height), but I threw that idea away before I even got to tackle problems like uneven ground - it just didn't make as much fun as following after the board in the air, and it didn't help against motion sickness as much as I expected. That may be a me-thing though, as I just had no problems with motion sickness at all during my debug- and gameplay sessions - with or without ground-projection.

So instead I made the player teleport to the actual former positions of the board. Problem with that was that the board's center is barely above the ground, which when translating it 1 to 1 to the players position means that the latter gets stuck in the ground more often than not, which the RigidBody *tries* to fix. Semi-Successfully so.

Because of that, I included an actual teleportation method for the Player (though in the TeleRollingBoard script), which uses a *Raycast* to look whether there's even enough space for the player and increases the teleportation position by half of the player's height when something is hit.

Lastly, the collection of all the board's positions made it that following the board through collisions and slowly petering out made the feature rather discomforting and boring respectively. My first idea was to smooth those values out of the queue, but luckily I thought of a less complex solution before implementing it. That being to only record new positions if they're a minimal distance away from the last.

That worked surprisingly well for both problems.

![New Follow-After Feature](https://raw.githubusercontent.com/theblacki/IVRAR_Project/master/static/img/week8/FollowAfter.gif "GIF of the TeleRollingBoard with the follow-after in action")

## TeleRollingBoard Visuals
The last thing I wanted to tackle before going into my well-deserved winter break was the TeleRollingBoard's appearance - that currently being a scaled basic 3D cube.

After unseccessfully searching for something that looked like a nice, flat, futuristic teleporter in the free unity assets, I decided to just make it myself instead.

For that, I used a hexagon model from a strategy game toolkit I used before in another project, took the wheels from a free skateboard asset and put all of them together to create a somewhat futuristic-ish, but final TeleRollingBoard. I also put one of those halos that were on all the coins onto the center of the top-level hexagon and made it blue.

![New TeleRollingBoard Visuals](https://raw.githubusercontent.com/theblacki/IVRAR_Project/master/static/img/week8/TRBvisuals.png "Screenshot of the TeleRollingBoard in the game scene")

Very futuristic, very realistic, incredible visuals, 10/10 - if I may say so myself.

Also, I put the rolling/sliding physics material I used before on all the wheels, and put one with much more friction on the hexagon.