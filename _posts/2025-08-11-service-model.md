---
title: "Service Model by Adrian Tchaikovsky - High Level System Design"
layout: post
date: 2025-08-11
image: https://upload.wikimedia.org/wikipedia/en/2/25/Service_Model_by_Adrian_Tchaikovsky.png
headerImage: true
tag:
- robotics
- machine learning
- science fiction
- technical
- architecture
- fictional
- fictional system designs
star: false
hidden: false
category: blog
author: varunmehta
description: Envision a robotics architecture for Service Model
---

> [**Service Model**](https://en.wikipedia.org/wiki/Service_Model) is a 2024 satirical science fiction novel by British author Adrian Tchaikovsky. The novel tells the story of a robotic valet who murders his own master, and further explores the robot's journey to discover a reason for existence during the collapse of human society.

I started [listening](https://share.libbyapp.com/title/10250315) to [Service Model](https://en.wikipedia.org/wiki/Service_Model) by [Adrian Tchaikovsky](https://en.wikipedia.org/wiki/Adrian_Tchaikovsky) a couple of days ago. The premise is not new, but follows an interesting trajectory from a robot's view point. The story reminded me of [Three Robots from Love, Death & Robots](https://www.imdb.com/title/tt9788484/). Science fiction stories are always a good place to look for ideas. [Star Trek](https://en.wikipedia.org/wiki/Technology_in_Star_Trek) has and will always be one of the poster children for futuristic inventions. This post is a fun little exercise, performing a design overview on how we can build a system, so we don't run into the problems in the future as described in the book.

Service Model explores a future where robots continue to follow ingrained service protocols long after the collapse of human civilization. If you're a robot in that universe, imagine needing to manage a never deleted and always growing task list with no central server and full autonomy. Every robot’s task management is built for a human-robot ecosystem, not for an autonomous survival scenario. Once humans start to slowly vanish and the central servers start going offline, the task management systems keep running as designed, and that is the problem.

> ***Warning***: Potential spoilers from the book ahead. I've tried to keep things as abstract as possible without revealing too much of the plot. 

## Tasks Management
One of the biggest common challenge in the story is persistent, uncleared task queues. This behavior is exhibited by the police and doctor bots at the start of the story, and later by a lot of different types of bots when waiting at Diagnostics. There are high-priority tasks which have been open for over a 1000+ days. Tasks are never deleted but then again, not all are equal. 

Real world challenges faced by the robots in the book
 * Tasks persist indefinitely, even after the context is irrelevant.
 * Ambiguous tasks, without clear goals and directive, ex: preserve the knowledge and library.
 * Decision paralysis when confronted with conflicting ideas, with no central authority (human to override).
 * No task hierarchy or priority.
 * Duplication of tasks across different robots.
 * Lack of inter robot communication compatibility. Different protocols prevent standard communication.

 ### High Level Engineering Principles to Avoid Failure. 
  1. Tasks should have a lifecycle and follow TTL rules. 
  1. Context awareness when executing tasks.
  1. Consider storage limitation, archiving policy 
  1. Shared cooperation and coordination.

#### Metadata
Adding some additional metadata to the tasks. Old tasks stay in the system, but get de-prioritized unless flagged as critical to avoid starvation of new tasks.
 * Timestamp
 * Priority scoring, decay over time, unless refreshed
 * Completion state: [`open`, `in-progress`, `stalled`, `obsolete`, `done`, etc...]
 * TLL (Time-to-Live) of a task after which its priority can reduce
 * Energy cost estimate (based off historical consumption patterns)
 * Always bind tasks to specific, measurable outcomes (SMART goal principle).

#### Storage Structure (similar to git)
 * Append only tasks, no deletes 
 * Indexed on priority and timestamp
 * Compression of old tasks
 * Implemented tiered storage (similar to S3) active vs cold storage
 
#### Queue Maintenance
 * Deduplicate recurring tasks 
 * Review list of open tasks and update priority score
 * Archive low priority tasks into summaries 
 > Think of compressing all the HTTP `/info` logs captured every minute, over 1 month (43,200 statements), compressed to 1 log statement. ~ *Battery maintenance check was logged 800 times between date1 and date2* 
 * Monitor resource (memory and power consumption) of itself, the queue.

#### Self-Care  
 * Prioritize self-maintenance tasks over any high priority tasks in the queue.
 * Pick up new tasks or interrupt current task to address self-maintenance. 
 * Ensures it doesn’t prioritize external service over its own self-care.

#### Model Context Protocol 
During communication between robots, the same robot responds with different response times, based on how they are processing the response. Having an MCP to manage requests can be helpful. 
 * Tasks are interpreted and executed per the operational context.
 * Multiple models (perception, planning, behavior) can co-exist and be activated or deactivated depending on environment, mode, or goal state.
 * If one model fails or behaves erratically, MCP can isolate it, revert to fallbacks, or switch operational modes as needed.
 * Pause tasks if preconditions to execute tasks are not met (this has potential to never execute a task also).

#### Other Task Solutions
  * Use consensus algorithms when conflicting tasks are provisioned. 
  * Use deduplication protocol when performing tasks across robots. This can get a lot more convoluted, if the bots are trying to be independent, and don't readily share information. Can also cause oversharing and cause bottlenecks.

This is not a fool proof solution. There are other places where a lot of other issues can pop-up. Overall, the book is showing a grim reality, of what will happen if AI/Robots take over jobs without people having any tasks or source of income to manage. It is [Weapons of Math Destruction](https://en.wikipedia.org/wiki/Weapons_of_Math_Destruction) meets [Fallout](https://en.wikipedia.org/wiki/Fallout_(American_TV_series)).