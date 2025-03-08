+++
date = '2025-02-10T10:52:33+01:00'
draft = false
title = 'Week 15 - APK Madness and Final Presentation'
+++

# APK Madness and Final Presentation
Since everything's finished up, I can basically start leaning back already, right? Just deploy my APK once to see if it's actually running, and I'm good to go... right? Who would have known that this simple step would take me one full, additional week...

## The APK doesn't run
Building the APK was as easy as one would expect, as was deploying it on the Meta Quest 2 via SideQuest. Just one little problem: When I tried starting it after deployment, it just instantly closed, not giving me any more feedback as to why that happened.

Well, something always goes wrong when you develop for a system for the first time, just means that you'll need to google the problem. Daily routine, right?

Except that I didn't have an error message to search with, but maybe looking for the behavior would give me any leads...

Two hours of going through forum posts and other sources of somewhat similar (or not) problems later and having tried out multiple of their solutions - mostly concerned about APKs that worked once, but don't anymore - I could say pretty sure that I wouldn't find any solutions this way. I needed to find out more about what's happening, but would I get that information? It's not like I could just take a look at the console, and looking through the Quest's settings, I found no indication of any kind of system or event log.

So google it was, again, and as it turned out, I could use another software, called the *Meta Quest Developer Hub*, to take an actual look at the system logs. Having that installed, I connected my Quest to my PC again and let the Log be gathered, and well... there were a lot more logs than I expected. Good thing there were filters for the log severity, and I could literally look for crash reports, which reduced the amount of log entries to *just* a couple hundred.

Unfortunately, the logs were not helpful. They referenced my packages, or rather libraries used by me (libunity, libgame, libOVRplugin etc.), but didn't tell me what the actual problem was. They also referenced a tombstone file on the device, which I promptly found and took a look into, but it only added even more (for me) useless data in the form of an unreadable cache dump.

Maybe I made some problematic changes to the XR related stuff in my scene? I did try out some crazy stuff and broke it multiple times in the time of my project, but I thought I had reverted everything that went wrong. Developing my project backwards for a couple of hours did, however, not help. The problem should not lay within my scene then, I guessed.

So, the most probable cause for the problem should have been in the libraries i used, right? And the only place I could influence those is within the packages I used. But the only packages I could leave out were the ones that were in use because the project uses the Built-in Render Pipeline. So, did I need to port my project to the Universal Render Pipeline instead?

Before I started such an undertaking, I decided to just ask in the next lecture, and got told to take a look at the Shaders I used. Weird, since I did not do anything with those, and I also did not import anything non-straight-forward from the asset store (basically only the skateboard prefab for the wheels), but what did I know?!

Taking a thorough look at my project, I made sure that the only Shaders used were from the default (Standard) renderer, and no special effect - except the pre-integrated halos of the coins (and my TeleRollingBoard) were in use. Since I couldn't change anything about the standard shader - at least not that I knew of - the only way forward in my eyes was to go through with the Universal Render Pipeline Conversion, which would solve both the packages as well as the shaders problem.

Except that I did not know that there is a better way to convert the shader used to the URP one than having to manually change it in the inspector for every single material and having to reapply the used color maps again... and again and again... that went pretty straight forward. With the exception that the halo effect didn't work for the URP, so one Youtube tutorial later, I implemented an alternative glow effect that didn't look *that* much worse.

Testing and fixing the parkour a bit later, I was ready to give the installation of the APK another try. A build, a deployment, a failed starting, and a look into the logs later, I became somewhat desperate. Nothing changed, except that the referenced packages now included not my project and company name, but instead just *template.urpblank*, even though I *did* remember to put those values. I later found out that this required its own setting for the URP, but that was not my current problem.

As I said, I grew desperate. So, I created a new URP project and put the XR stuff in strictly as described in the slides, built, deployed and started it, and... it also crashed. Growing even more desperate, I created another new project, this time using the BiRP, added XR, built, deployed, started, crashed.

What, just what, what the heck? Four days into this problem, I gave up. I posted a description of my problem to the forum and asked others for their experience (which no one ever answered, forum activity this year was pretty bad outside of myself) and put together everything I knew and estimated (which wasn't much), added the actual logs as well as my repositories for the original and URP versions and just sent a request for help to Samuel.

I used the rest of the day to get a recording and film editing software running and recording a complete playthrough of my parkour while running via *Meta Quest Link* in Unity. Thinking back, there should've been a better way to record gameplay than to use the *Game* window within Unity, maybe even one where the game sound is also recorded, but whatever. I was too frustrated to even think about that at that time.

I at least now had a >5-minute video to show as replacement of the game demo to play during the final project presentation.

Two days of working as a working student later, I received Samuel's answer. Which is that he built my project, deployed it, and it worked. Almost in passing, he mentioned that there could be a problem with the system version of my Quest 2. As it turned out, my predecessor must have deactivated the automatic software updates for some reason, making my Quest incompatible with the newer framework versions of the packages. Because, one update session later, my APK just worked.

All of that work, the time and effort, the frustration, because of such a dumb and easy-to-fix problem... I really love software development sometimes.

For those interested, here's the [link to my repo of the URP version](https://github.com/theblacki/TRB_Parkour_URP "GitHub Repo with the URP version").

## Final Presentation Preparation
Considering that I had already created premium footage of my project including all of the possible interactions, I was able to include them into my [final project presentation](https://docs.google.com/presentation/d/19-JMaxupf-0s3u4k-S3_ZLYhaDf88JKTtpX8-zotNaA/edit?usp=sharing "The final project report google docs presentation"), as well as put my full video at the end so that everyone who forgot their VR goggles could at least watch that. All *thanks* to the APK shenanigans.

Well, at least that's done, and I've not only given some thoughts to the metrics for the study later, with all the interactions - and the footage of each I made for the video - the presentation became really nice in the end.

The final problem I encountered was that my fellow students who used the URP did not find out about the package naming issue mentioned before, making all of their packages have the same ones - in addition to the ones who still used the provided names from the BiRP version provided. I reminded everyone about those issues, and at least some of them were able to make amends before the deadline.

Good thing that this time, the problem when trying to deploy multiple packages with the same name onto the Quest 2 actually gave me a readable error message.