---
title: "Road to Demo"
description: "Showing off some new enemy designs, and talking about steps towards a public demo."
date: "2025-07-30"
image: "/images/title/scyther.png"
---

I have began a thorough refactor of This is My Temple. Reason being: The code was disgusting, and preventing me from scaling the game.

**Refactor Goals**
- KISS (Keep it simple stupid)
- Improve scalability of game
- Achieve a fun playable demo by 2026.

### New Enemy Designs
Sharing some new art, before I talk about the fun programming stuff.
I bought a drawing pad to help, and that has been pretty awesome. It's taking some getting used to, but will be worth it in the long run.

![sneaky boi](/images/sneaky-boi.png "sneaky boi")
First up, is sneaky boi!!! He is so sneaky, and greedy.
It disgusts me.
He is totally animated by the way, but I am writing this blog post at work, so the gif version is not available to me.

I might add in the gif here later, but I am extremely lazy, so that will likely just appear in another post.

*WITNESS HIM.*

![scyther](/images/gifs/scyther.gif "scyther guy")
Scyther guy!!!!!!!!! 
This is probably the first animation that I am actually proud of.
I wanted to really take my time with this, and add lots of details like shadowing.

Currently this guy is fully animated, with a walk, and attack animation. I'll add a hurt and dying animation later.

### Programming Stuff
So yeah, I'm doing a pretty large refactor. I'm tossing out most of the old code, and just trying to get something up that is simple
readable and easy to build upon.

I'm glad that I built my game how I originally did, because it taught me a ton. But the code straight up isn't good. It's way too overengineered, and hard to understand.

So, I have started with the very core mechanics of the game.
- Roguelike Pause Mechanic
- Player Controller
- Mover Component (used by anything that requires a change in velocity)
- Enemy Class
- Enemy State Machine
  - Idle State
  - Chase State
- Game Sprite Class that obeys Roguelike Mechanic

So far so good. Next up, I'm working on one of the main mechanics of the game. *The ability system*.

This is a system that has needed to be taken back to the drawing board since the very beginning.
I've gone over several strategies to achieve my goals.

Goals of Ability System
- Create a robust but simple Ability System that is shareable by any game object.
- Drag and Drop Ability Creation, where the behavior is defined by its child components.
- Format abilities in a way where they can be easily imported on a whim.
- Allow friends to come up with abilities, and have an ability editor for them to create and submit ability ideas.
- Dynamically add abilities to game objects, based on skill point spending, inherited, or equipment.

### Other shit
I am participating in a game jam this week, Game Makers Toolkit Game Jam.

I joined a pretty large team of programmers, artists, and writers. The jam starts in a few hours, from this blog post.
So the theme of the jam hasn't been announced yet. But I am very excited to see what we come up with. That's what I'll be working on most of this weekend, and hopefully will find time to write about my experiences.

Also my TikTok page has gained some traction, This is My Temple does very well there. It's almost scary. Need to get my stuff up and working, and then put out a Steam page. I feel like everytime I have a successful post without a store page, I am missing a mega opportunity.

Also started climbing regularly again, which has been freaking awesome. And also started a new TTRPG campaign, which has also been freaking awesome.

>> End Transmission
