+++
date = '2025-01-25T10:48:22+01:00'
draft = false
title = 'Week 13 - Minor setbacks'
+++

# Minor setbacks
This week I tried to work through a couple of things in my backlog. I still had to get the actual parkour working again, but I decided to tackle other things first, so as to not break the mechanics again.

## Remote Grabbing
I wanted the teleport back of the board to not just be a teleport, but instead to lay it in the left hand, the same as if grabbed, maybe even that. Unfortunately, I was unable to find a way to set a grabbed object of the interaction rig. That is another one of those "obvious" features I'd just expect, like the isGrabbing bool from week 11.

## Virtual Hands instead of Controllers
I've seen virtual hands being shown instead of the controllers before, and I wanted that to also be the case for my project.

After a couple of hours of trying to swap a functionality, manually change the active visuals of the Rig or even put the hand visuals within the controller - unsuccessfully - I gave up on that and just reverted my completely corrupted Scene back to my last commit. Well, maybe for another project...

Instead, I used my time to introduce a good couple of Unity layers and tags, and gave every type of object in the scene a good thought about what they can and what I want them to collide and interact with. I had no problems with performance thus far, but I still feel somewhat more content now that this is done.

## Upside-down considerations
I planned for the board to behave differently dependent on whether or not it is currently upside down. One thing already implemented is the different friction when touching the floor, but I also wanted to make the teleport and riding impossible while upside-down, or maybe make the position - and rotation - of the player adapt to the current orientation of the board when teleporting.

The former, however, just turned out to be an unnecessary restriction, while the latter way the by far most disorientating VR interaction I had thus far. Scrapped.

Instead I removed any non-y-axis rotation when mounting the TeleRollingBoard, as they influenced the player's teleportation position.