+++
date = '2024-12-01T11:19:40+01:00'
draft = false
title = 'Week 5 - First Implementation of the TRB'
+++

# First Implementation of the TRB
This week I implemented the first playable, or rather interactable version of the TeleRollingBoard.

## Working with the XR Interaction Rig
There are two major areas which I worked on this week, one being the as-of-yet pseudo code in the new script mentioned last week, the other being the XR functionalities within Unity.

The more straight-forward part is adding the grabbable interaction on the TeleRollingBoard GameObject. Doing that just as I did for the Roll-A-Ball VR integration worked just as straight forward as I remembered it. Doing so also put a *RigidBody* and a *Collider* on my object, both of which I'd need either way - at least I thought so at that time.

However, for what I planned last week, that being teleporting the board back to the player, I needed to find the corresponding hand position somewhere within the *OVRCameraRigInteraction* GameObject. Considering that I looked for a hand position, instead of a controller position, I may have made it harder on myself than necessary, but the fact that putting the headset down makes different parts of the *OVRCameraRigInteraction* reset their positions did not make it any easier. Well, I sooner or later found the relevant child object and was able to reference it in my script.

![Left Hand Position](https://raw.githubusercontent.com/theblacki/IVRAR_Project/master/static/img/week5/leftHandHierarchy.png "Screenshot of the Unity Hierarchy Position")

## The TeleRollingBoard Behavior Script
With the Unity part finished, the first feature followed soon after: Returning the board back to the player's left hand. I created a function for every action I would later implement, all looking similar to the following:
```csharp
private bool DoTeleport => OVRInput.GetDown(OVRInput.Button.One);
```

I then created the handling of the relevant Input handling within the Update method, which works pretty straight forward:
```csharp
//resolve return to hand
if (DoReturn)
{
    transform.position = leftHandTransform.position + leftHandTransform.right * .1f;
    Stop();
}
```
The *Stop* method called clears any angular or linear velocity on the *RigidBody*, so that the board does not jump out of the hand after being teleported.

The teleportation of the player to the board worked similar, except that instead of a to-the-right offset, there is a upwards one.

## Physics with the RigidBody
So far so straight forward, the only thing missing is the throwing, the main method of interaction planned.

The approach I thought of last week is to save the boards positions while being held and compute the direction of the last position when let go from one before that.

For that, I take the grabbing controller input
```csharp
private bool RightTrigger => (OVRInput.Get(OVRInput.Axis1D.SecondaryIndexTrigger) > .4f
                           || OVRInput.Get(OVRInput.Axis1D.SecondaryHandTrigger) > .4f);
```
calculate the current situation
```csharp
//calculate control inputs - grab, teleport, return
bool letGo = isCurrentlyGrabbed && !IsGrabbingRight;
bool takeInHand = !isCurrentlyGrabbed && IsGrabbing;
isCurrentlyGrabbed = IsGrabbingRight;
```
where *IsGrabbing* checks for the *RightTrigger* and actual Collision with the hand, and *isCurrentlyGrabbed* is a global *bool*.

The *takeInHand* action only stops the board, similar to the *DoReturn* one explained before. The *letGo* one is more worth a look into:

```csharp
//resolve let go (throw)
if (letGo)
{
    Vector3 movement = (transform.position - oldPositions.Peek()) * throwingSpeed;
    if (movement.magnitude > maxSpeed * throwSpeed) movement = maxSpeed * throwSpeed * movement.normalized;
    rb.AddForce(movement, ForceMode.VelocityChange);
}
```
In here, *maxSpeed* and *throwSpeed* are public variables serialized into Unity for easier testing and tuning - at least that was the plan before I recognized how inconvenient it is to debug while interacting through a VR headset, at least as a wearer of glasses.

As Unity told me that just overwriting the *linearVelocity* of a *RigidBody* is bad (and also doesn't work anymore), it took me some time to find this way of adding force, but it works. More interesting is the *oldPositions* queue, whose calculation - after some testing and debugging - I put into *FixedUpdate* instead:

```csharp
//update position queue (don't care about delta)
oldPositions.Enqueue(transform.position);
if (oldPositions.Count > nrOldPositions) oldPositions.Dequeue();
```
Once again, *nrOldPositions is a public variable for tuning - initially set to 25 to safe half a second of positions, later reduced to 15 to accommodate quicker movement.

As good as all of that looks, for some reasons it just didn't work. The calculation did - at least included debug logs said so - but when letting go of the board, it just fell down to the floor with no sight of any forces working - except the *RigidBody*'s gravity, obviously.

It took multiple hours of debugging until I looked at the *isKinematic* variable of the *RigidBody*, which is set as *false* in Unity... which it should. When my force is set, however, for some reason, it is set to *true* instead. When I put down my VR headset to look at Unity, however, it is still set to *false*.

*Isn't that interesting?*

Less than half an hour later, I debugged far enough into the *Grabbable.cs* script of Meta XR to see that whenever something is grabbed, its *RigidBody*'s *isKindematic* value gets set to *true*, and, when let go, back to *false*. Also, that happens in a branch that is controlled via a global variable. A public one, serialized into Unity.

Finding the relevant GameObject within the *OVRCameraRigInteraction*, I soon find the relevant option, deactivate it, and well... now it works.

*Is it not nice, when multiple hours of frustrated debugging end up in you feeling like a goof? Exactly, it is not.*

In comparison to that the fact that the board sometimes just goes through the floor mad for a much easier problem. I just increased the Collision Detection up to *Continuous Dynamic* for my central interaction object - which seemed fair - and it worked.

You can see the first working state of the parkour in the following video:

[![WIP TeleRollingBoard Demo](http://img.youtube.com/vi/XAqnQijZuik/0.jpg)](http://www.youtube.com/watch?v=XAqnQijZuik)