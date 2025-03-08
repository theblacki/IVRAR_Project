+++
date = '2025-03-05T11:42:29+01:00'
draft = false
title = 'Week 18 - New Metrics and Study'
+++

# New Metrics and Study
Before the study execution could begin, I had to include all the metrics I wanted to gather into the game. Good that I already gave that some thought for my final presentation.

## Metrics
I included more metrics specific to my project with its many kinds of interaction techniques. Of course, the default interaction task metrics and global times were still measured.

Additionally, the frequency of use of the different techniques, including throws and callbacks, as well as the average distance to the ground were all monitored.

Most of the new stuff came down to initial button presses or counters in existing branches, but the average distance to the ground uses simple math in cooperation with the good old *Raycast* - only on a geometry layer, which is one of the layers I created in week 13. Since I don't want to save the thousands of individual numbers until I log the average, I made sure to compute then out of only two values instead:

```csharp
//metrics for avg player height
Physics.Raycast(player.transform.position, Vector3.down, out RaycastHit hit, 1f, geometryLayer);
float currentHeight = player.transform.position.y - hit.point.y;
metrics.AvgDistToGround = (metrics.AvgDistToGround * metrics.AvgCount + currentHeight) / ++metrics.AvgCount;
```

I gathered all the data in the *ParcourCounter* class, including the *DataRecording* data sets and included a method to write them to the device as logs.

## Study Execution
The study was executed with two players with differing VR experience, as well as myself. Player 2 has their own VR headset, while Player 3 does not. None of the other two players got any more information than that they're to get through the parkour, try to collect the coins, and solve the tasks, as well as the following control sheet:

![TRB Control Sheet](https://raw.githubusercontent.com/theblacki/IVRAR_Project/master/static/img/week18/AllInputs.png "The Possible Interactions and their Controller Mappings")

The players all used the same Quest 2 and played through the following parkour:

[![Final TeleRollingBoard Demo](http://img.youtube.com/vi/0CBcWFlK5ng/0.jpg)](http://www.youtube.com/watch?v=0CBcWFlK5ng)

## Study Results
|   Data Set   | Total Time Needed | Coins Collected | Average Manipulation Error | Average Time Needed |        Techniques Used*        | Average distance to the ground | 
|:------------:|:-----------------:|:---------------:|:--------------------------:|:-------------------:|:------------------------------:|:------------------------------:|
| **Player 1** |
| First Stage  |        2:40       |      15/16      |           0.123            |         6.559s      |   6, 6, 67, 11, 33, 5          |              0.460             |
| Second Stage |        1:30       |      30/30      |           0.111            |         8.170s      |   7, 2, 60, 5, 24, 9           |              2.600             |
| Final Stage  |        1:54       |      21/23      |           0.103            |         6.193s      |   5, 6, 53, 7, 15, 1           |              5.594             |
|--------------|-------------------|-----------------|----------------------------|---------------------|--------------------------------|--------------------------------|
| **Player 2** |
| First Stage  |        8:44       |      15/16      |           0.107            |         13.578s     | 79, 83, 245, 10, 48, 0         |              53.078            |
| Second Stage |        7:22       |      30/30      |           0.0              |         0.0s        | 59, 30, 197, 20, 69, 0         |              121.850           |
| Final Stage  |        4:31       |      23/23      |           0.882            |         10.248s     | 49, 7, 176, 5, 28, 0           |              12.090            |
|--------------|-------------------|-----------------|----------------------------|---------------------|--------------------------------|--------------------------------|
| **Player 3** |
| First Stage  |        5:51       |      15/16      |           0.151            |         16.883s     | 49, 3, 103, 1, 19, 0           |              1.356             |
| Second Stage |        9:04       |      30/30      |           0.135            |         11.267s     | 22, 29, 297, 141, 169, 8       |              34.732            |
| Final Stage  |        2:28       |      23/23      |           0.132            |         9.181s      | 1, 14, 96, 6, 33, 0            |              3.145             |

\*the frequency of technique uses, in the order *Teleport, Mount, Throw, Remote, Recalls, FollowAfter*

The first set of data corresponds to the run shown in the video above. It should also be mentioned that the first stage was missing one coin, so every participant actually collected all coins within part 1. Also, player 2 skipped the second interaction task by throwing the board above the trigger zone.

The results are not entirely unexpected, but as much as I'm positively surprised by everyone really trying to gather all the coins, I also did not expect the fact that you can gain much height by using the teleportation while holding the board to be abused that much.

Luckily, neither of them figured out that the remote control works while the TRB is mounted...

I expected both players to spend some time to figure the mechanics out, which one did right at the start and the other in the second segment, but it seems one of them never even figured out the follow-after action... Well, there *were* many possible actions, and none of them were exclusively mandatory.

As it turned out, the follow-after action was not very popular, but that was already mentioned as feedback on the final presentations, and I wouldn't have used it myself if not to show it within the video...

## Conclusion
Within this project, I encountered many expected, and even more unexpected problems. I was able to solve many of them and at least learned something from the rest.

The concept was enhanced and refined along the development process, and many more feature were added after I received feedback. With the exception of the height gaining glitch, I am very pleased with the final state of the project and what I've accomplished within the process.

It was a lot of fun getting to know the XR development process, and I've already ordered my own Meta Quest to be able to continue playing and developing in XR.

I'm looking forward to to using what I've learned in the future.