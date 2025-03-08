+++
date = '2025-02-01T10:51:49+01:00'
draft = false
title = 'Week 14 - Game Mechanics Tweaking and Repair'
+++

# Game Mechanics Tweaking and Repair
Two weeks before the final presentation, it was finally time to take another look at the original game mechanics - that being the parkour relevant scripts.

## Original Game Mechanics
As it turned out, even though I included the still relevant parts from the original scripts, the actual parkour did not quite work at the start of this week.

Even though this was only the result of some missing references, it made me take a closer look at an area of my game that still needed some straightening.

One thing I had to adapt was the fact that teleporting past all the triggers was way too easy, and happened more often than not even when not intended. I fixed that problem by making the TeleRollingBoard not only also able to collect coins, but instead fully act like the player (restricted to collisions, of course).

Including a teleportation of the player to the task area when triggered by the board, the game was soon playable again.

I also included the TeleRollingBoard to the T-object of the interaction task - of course without all of its scripts.

Finally, I disabled the TeleRollingBoard while the player works on their tasks, so that it is not possible to accidentally move outside of the task area.

With this, the game was ready to be played in the final presentation in two weeks. I just need to build and test the APK, but how hard can that possibly be?