---
title: "Pickleball Referee - Part 1"
layout: post
date: 2026-08-20
image: https://usapickleball.org/wp-content/uploads/2025/10/in-or-out1.jpg
headerImage: true
tag:
- computer vision
- technical
- machine learning
- yolo
star: false
hidden: false
category: blog
author: varunmehta
description: Pickleball Referee
---

Started playing Pickleball, I always thought, pickleball was an old person sport, but after the first day of playing close to 2 hours, I had aches and soreness in muscles I did not know existed in my lower half of the body. 

The most common problem with the game is everyone arguing over whether the ball was in the court or out.

## Enter Pickleball Referee

![/assets/images/projects/pickleball/screenshot-with-players.png](/assets/images/projects/pickleball/screenshot-with-players.png)

The idea is to connect 2 Raspberry Pi5 at either ends of the court, attach an AI HAT on top, with a V2 RPi camera, and see if they can act as a referee. I've started with CVAT annotations for the video, and converted a 350 frame video to an annotated dataset for YOLO. 

### train.txt
```
data/images/train/frame_000000.png
data/images/train/frame_000001.png
data/images/train/frame_000002.png
data/images/train/frame_000003.png
...
...
data/images/train/frame_000350.png
data/images/train/frame_000351.png
```

### data.yaml

```
names:
  0: ball
  1: player_1
  2: net
  3: court
  4: kitchen
  5: center-line
  6: out-of-bounds-line
  7: racquet
  8: player_2
  9: player_3
  10: player_4
  11: service_area_1
  12: service_area_2
  13: service_area_3
  14: service_area_4
path: .
train: train.txt
``` 

### labels

#### frame_000000.txt
```
0 0.440346 0.643528 0.007526 0.013389 0
1 0.377003 0.686065 0.072901 0.382796 1
8 0.605026 0.612417 0.083594 0.332019 2
9 0.472115 0.463144 0.018073 0.081657 3
10 0.563219 0.481194 0.040646 0.115167 4
```

#### frame_000143.txt
```
0 0.371982 0.462579 0.007526 0.013380 0
1 0.372630 0.618773 0.079396 0.298120 1
8 0.527065 0.553847 0.067703 0.267380 2
9 0.396521 0.471745 0.039052 0.081657 3
10 0.551924 0.466981 0.040641 0.118500 4
```

After I've got the data annotated, I started to look into court mapping and hit upon Homography.
> A homography is a geometric transformation that maps points on one flat plane to corresponding points on another flat plane while keeping straight lines straight.

The project is paused for now, need to spend some time finishing the court mapping, before I get back to it. The other challenge is getting the camera with Pi setup and installed at the court! 