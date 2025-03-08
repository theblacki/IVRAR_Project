+++
date = '2025-01-12T10:48:22+01:00'
draft = false
title = 'Week 11 - In-world Settings Control'
+++

# In-world Settings Control
This week, I recognized that not being able to tweak stuff in Unity while wearing the VR headset is rather inconvenient. More than that, some of the regulators could be nice to be chosen by the players themselves. So, that became my goal for this week.

## Settings Sliders on the Board
I put Sliders, consisting of a rectangle (to visualize the mechanic range of the slider) and a ball on top of the TeleRollingBoard and furnished it with a *TMP* label. Each slider got a grabbable interaction, like the board itself has one, as well as a script that just computed and provided the current value:

```csharp
sliderValue = (slider.localPosition.x + radius) / (2 * radius);
```
With the *sliderValue* being a public variable and the radius being half the global length of the mechanic range.

I put two sliders on the TeleRollingBoard, one for the throwing speed multiplier and another for the effective range. I've made it so that whenever the Board is outside of the range, it's drag as well as the gravity is heavily increased.

The slider values were included within the TeleRollingBoard script, leading to some adaptions to existing code, e.g. the throw action from week 5:

```csharp
if (movement.magnitude > maxSpeed * speedSlider.sliderValue) movement = maxSpeed * speedSlider.sliderValue * movement.normalized;
```

I made it so that the sliders were only active while the board was grabbed by the left hand and constrained the sliders' movement to the local x-axis in the same range as used within slider value script, making their behavior pretty much the way I intended for it to be. This is how the final sliders looked like:

![New Slider Visuals](https://raw.githubusercontent.com/theblacki/IVRAR_Project/master/static/img/week11/Sliders.gif "Screenshot of the TeleRollingBoard with active Sliders and without halo")

## OnTriggerEnter/Exit shenanigans
While debugging with the sliders, I was able to put my finger on a problem I observed before, that being the grab checks from the original game mechanics (dependent on the *OnTriggerEnter*/*Exit* methods) just did not seem to work as intended. The OnTriggerExit seems to sometimes just... trigger, even though the object is still being grabbed.

I searched for a in-house solution from the XR kit, but was not successful in finding one. I still feel like there has to be one, as that would just be, well, obvious, but for the moment I fixed the problem by making the state switch dependent on the triggers held - or not held, more specifically.