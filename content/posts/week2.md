+++
date = '2024-11-10T11:19:40+01:00'
draft = false
title = 'Week 2 - Idea Conceptualization and First Presentation Preparation'
+++

# Idea Conceptualization and First Presentation Preparation
Before being able to get started with the project, the core ideal and goal have to be defined and conceptualized. Premised on the project requirements, the concept should integrate both locomotion in and interaction with the game world.

## Self- vs. object-based locomotion
Instead of directly deciding upon a concept, I first tried to make smaller decisions for the direction. Primarily, I differentiated between what I would call self-based and object-based locomotion.

In the examples we saw as part of the lecture, the bow and arrow, which make the user teleport to the spot shot, would be categorized as the object-based kind, the default flying one as a self-based one, and the boat with a paddle as something in between.

The first question was thus, which of the approaches I would want to make the focus of my implementation. The problem with that, of course, being that i missed any kind of experience that could actually influence this decision. Instead, my decision was only influenced by rather superficial reasons:

- Which approach would make more fun? Both should make plenty if done correctly.
- Which one could lead to more (implementation) problems? With my development experience, both. However, considering the even lower amount of experience with XR development, self-based could probably lead to encountering more XR specific problems.
- Do I want to include actual self-movement (as in walking)? Considering the amount of space available in my development space (my home), definitely no. Better yet would be a concept that could be executed while sitting.
- Which approach would lead to more likeliness of motion sickness? Considering there'll be no self-movement, teleportation will probably be the only surefire way of circumventing motion sickness. For that, I expect object-based locomotion to be preferable.

That said, I opted for an object-based locomotion technique.

## But what object?
Since I decided upon having an object as the basis of my locomotion, I also wanted to have my entire interaction additionally to the locomotion based upon this object. The object should be in the center of the gameplay - and thus the user's attention.

So, if the locomotion is going to be teleportation based and dependent of the interaction with said object, what should that interaction look like?

The first idea, thanks to the example videos from the lecture, would be to shoot something somewhere and (opt to) teleport there afterwards, but nevermind that feeling like a cop-out for any kind of gun-like object, more interesting objects would mostly include more - let's say - expressionistic gesticulation, which would be harder in the works-while-sitting approach I imagined.

Also, wouldn't a more direct kind of interaction be more fulfilling? One where you don't just handle your object in some way to get to where you are, but you actively have to get the object to where you want it? Like... throwing?

Now the only thing to consider is how I want the object to behave when thrown, with two ideas primarily worth considering: The object can either be very aerodynamic or even flyable, or it can roll farther or even be driven. Considering that I want to teleport to the object once it got to where I want it to be, and I don'T want to make a flying game, I decided upon the latter.

And that is how the idea was determined: What I want to create is a throwable, rollable teleporter - or in short, a **TeleRollingBoard**.

## Project Pitch Creation
With that, I already got a good project name for the pitch next week.

After adding a couple of images to better convey the idea and marking a few keypoints, the [project pitch](https://docs.google.com/presentation/d/1HSSrnwskiwQ3RpPzYqDUE6AA4t3aTac4cEoAFSCfJhs/edit?usp=sharing "The project pitch google docs presentation") was finished.