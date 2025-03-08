+++
date = '2024-12-07T11:19:40+01:00'
draft = false
title = 'Week 6 - TRB Improvements'
+++

# TRB Improvements
This week, again, I worked on the TeleRollingBoard itself, improving different aspects of its behavior.

## GameObject Adaptations
I added some teleporter sounds to the TeleRollingBoard, one constant humming to make it easier to find when not in sight, and a whooshing sound effect when the player uses the teleport action. This probably marks the last changes I do with regards to sound, as including rolling, flying and impact sounds would probably lead to more headaches than it is worth. Also, the background music has not made me lose my mind, yet.

I also added another *Collider* to a new child of the TeleRollingBoard to make it act like the player, especially to be able to collect coins.

## Board-Player behavior
Within that child I also created a new script, so as to handle all the objects it could collide and interact with - which at the moment only includes coins, but should also include all the other interactions of the player object from the original game mechanics.

Which I will catch up on once I take an actual look at the latter.

But that also means the GameObject needs another *AudioSource* for it's own coin collection sound - instead of playing it from player's location.

And after I had the board collect literally everything it touched - leading to it deactivating everything it touched and making a collection sound, also including the player itself, which some of the XR scripts vehemently tried to autocorrect, which lead to some rather interesting bugs - I included a branch to check on the coin tag.

## Physics Improvements
I wanted to add the rotation of the board before being thrown to be included in the flying object, so I also added the board rotation to the *oldPositions* queue, making it a queue of tuples and adding the new difference as angular velocity to the *RigidBody* as part of the *letGo* branch:

```csharp
rb.angularVelocity = new Vector3(0, (transform.eulerAngles - oldPositions.Peek().Item2) / nrOldPositions, 0);
```

Additionally, I played around with the *RigidBody* and *Collider* components so as to make the board more like an actual rolling board - i.e. to make it *roll*, or currently rather glide on the floor. With a bit of drag control and friction, that soon worked a lot nicer.

After tweaking some of the movement translations and speed, I realized that the *RigidBody*'s own gravity is just too strong for the experience that I'm going for. As such, I included another public variable to add downward force whenever the board is not held (this time, I did so directly within *FixedUpdate*):

```csharp
if (!RightTrigger && !LeftTrigger && !DoReturn)
{
    rb.AddForce(gravityMultiplier * Vector3.down, ForceMode.Force);
}
```
The variable *gravityMultiplier* once again being public.