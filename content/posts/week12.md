+++
date = '2025-01-18T10:48:22+01:00'
draft = false
title = 'Week 12 - Mounting the TRB and Remote Control'
+++

# Mounting the TRB and Remote Control
This week I implemented two new locomotion and interaction features, one being planned since the interim report, the other being another idea from the discussions thereafter.

## Flying and Riding on the TeleRollingBoard
One more idea from the report discussions outside the follow-after feature was to be able to fly on top of the thrown board. While I agreed at that time that it would be a nice feature, I did not expect to actually get to trying to implement it. Well, here we are.

And it was a good idea to leave this feature out until this late. equipped with a method that teleports the player *on top of* something, my very own, very malleable (for me at least) gravity, drag and friction options and implementation, as well as my newfound experience in using the XR features (especially, in this case, hand positions) gave me a nice head start in the realization of this feature.

Rather, the implementation was comically easy, using the functionality of the default teleport, but without reducing it to a single instance, but happen continually while its button is pressed. Except that I don't play a teleportation sound every frame.

Less straight forward was the ability to influence the flight direction. I wanted it to work somewhat like a glider, where you could move left or right by moving the center of mass, for which i opted to use the center of both hands instead.

That worked only somewhat, however, and I was not able to figure out why the same movement could lead to drastically different outcomes, going to extremes of a move leading to almost no difference in the flight path, to the same move instantly making the board crash into the ground, some hundreds of Unity units away.

After quite some debugging, I dropped the feature with the controller positions as steering interaction, and just used the left controller's analog stick instead. Which works, and deterministically right at that.

```csharp
float horizontalInput = OVRInput.Get(OVRInput.Axis2D.PrimaryThumbstick).x;
rb.AddForce(flyInputStrength * horizontalInput * transform.right, ForceMode.Force);
```

However, I learned that very day that you could look around by moving said analog sticks - on either controller at that.

*Good to know, isn't it? I turned myself or my chair all this time...*

Unfortunately I did not find out how to deactivate the ability to look around, so the steering is somewhat unusable, but I'll still keep it in the way it is now.

## Remote Controlling the TeleRollingBoard
A feature I had planned since the very start is the ability to remote control the TeleRollingBoard. While I initially planned to move it with the analog sticks, my experience from the steering made me rethink my approach.

Instead, I implemented the ability to grab with one's left hand and have the board then move the same direction as the player moved their hand - of course, including rotational movement.

First, I wanted to yet again use one of my positions queues, but I soon realized that this heavily restrains the possible movement without having to swoosh around with one's hand like a maniac. Instead, I saved the initial position of the left hand when grabbing the air and use the vector from that position to the current one instead. Well, that said, I still use one of my queues for the rotation - can't quite escape my past, it seems.

The code is much like the computation of the throwing of the TeleRollingBoard, except that it needs to access the parameters and components of the TeleRollingBoard GameObject:

```csharp
if (!initialSet)
{
    initialSet = true;
    initialPosition = transform.position;
}
Vector3 movement = (TrbScript.CurrentlyOutsideRange ? 0.2f : 1) * remoteControlSpeed * (transform.position - initialPosition);
if (movement.magnitude > TrbScript.maxSpeed * TrbScript.speedSlider.sliderValue) movement = TrbScript.maxSpeed * TrbScript.speedSlider.sliderValue * movement.normalized;
Rigidbody rb = teleRollingBoard.GetComponent<Rigidbody>();
rb.AddForce(movement, ForceMode.VelocityChange);
rb.angularVelocity = 0.4f * remoteControlSpeed * (transform.eulerAngles - oldRotations.Peek()) / nrOldPositions;
```

The end result works nicely, at least it does ever since I reduced the angular velocity change, which were way too powerful before.