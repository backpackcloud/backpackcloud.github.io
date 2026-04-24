---
layout: post
title:  "The Loo(π)narium"
tags:
  - music
  - pedalboard
  - loop station
  - raspberry pi
  - midi
  - chaos
category: unbelievable-exception
intro: >
  This is how software engineering principles like state machines and
  convention-over-configuration can transform traditional instruments 
  into a programmable creative platform.
audio:
  url: https://f000.backblazeb2.com/file/ataxexe/the-loopinarium.mp3
image: 
  file: loopinarium.png
  caption: The Loo(π)narium
---

## Before You Begin

I've generated a conversation between two hosts regarding this article using (pretend surprise) AI. I've chopped some parts and added a bonus to the ones who will be brave enough to follow it to the end.

## Talk is cheap... show me the rig!

[Here you go](https://youtu.be/9s396Tet8J8)!

---

## Intro

I’m a programmer. Which means two things:

1. I’m lazy.
2. I take that very seriously.

If something can be automated, it will be. If it can’t… well.. it’s probably because I haven’t over-engineered it yet.

Now, most people pick up a guitar to express emotion. I picked up a guitar and immediately thought: "This could use a control plane."

So instead of just playing music, I built... whatever this is.

A looper that acts like a scheduler.
A drummer that never complains about tempo changes.
An amp modeler which I spend more time adjusting than playing through it.
A chaotic synthesizer that always transports me to the nearest worm whole.
And somewhere in the middle of all this... a Raspberry Pi quietly making decisions I may or may not understand or regret.

This is not a setup. This is an unstable molecule. Every button is a MIDI message. Every loop is a state machine. Every song is basically an unpredictable runtime environment that somehow hasn’t crashed yet.

And today, I’m going to show you how I turned a perfectly reasonable guitar rig into a chaotic creative platform.

Welcome to the Loo(π)narium: an orchestration problem with strings attached.

## Setting the Stage

The ubiquitous way of connecting audio devices is through MIDI, so the little sanity inside me didn't let this slip out. I assigned each device to a unique MIDI channel and thought about the best route to connect them. Physically speaking, there's a MIDI chain that goes like this:

> Looper (Boss RC-600) → Modeler (Helix LT) → Drum Machine (BeatBuddy) → Looper (again)

Because the RC-600 acts as a metronome, it has to go first in the line, otherwise the rest of the rig wouldn't be aware of the tempo. The Helix has dedicated footswitches to slightly control the BeatBuddy, so it has to go before the drummer. The synthesizer is not part of the MIDI chain.

The Looper is then plugged to the Raspberry Pi via a USB cable, from where the MIDI messages flow in and out. The MIDI chain starts and ends in the Looper, passing through all the rig, but without creating the so called MIDI echo, where messages are relayed to each component in an infinite loop, teleporting the rig right into a Black Friday opening in a department store. In this rig, the loop is just in the music.

Inside the Raspberry Pi lives a software called Companion, responsible for dealing with that MIDI chain. It not only receives the messages, but also sends messages whenever it needs to coordinate things in the rig.

The Raspberry Pi is also attached to a StreamDeck XL, which doubles as a dashboard and a user interface. While the dashboard raise awareness of the rig's current state, the user input wraps a bunch of tedious steps into a dedicated button that's ready to be pushed by my greasy fingers.

Of course, this wouldn't have a purpose if there was no audio flowing through the rig. Audio input happens through the Helix, which receives input from my guitar and my synth. The audio is routed to the looper, which receives the following inputs:

- Stereo sound from the Helix (using the XLR inputs)
- Stereo sound from the BeatBuddy
- Stereo sound from a bluetooth adapter

The bluetooth adapter is there so I can hook up external resources, like guitar course materials that I don't really need to store inside the looper.

The sound gets out if this madness via a stereo output from the looper itself. There are three different outputs and each of them can have different mix configurations. I save two exact copies, one for the output to my interface and another to attach to my recorder.

As the last piece of this convoluted puzzle, I've plugged a portable router for emergency situations. The Raspberry Pi is configured to access my home router, but if I'm on the go and need to tweak something in the Companion app, I can just connect to the portable router and make the adjustments without too much hassle.

## Describing Chaos

Let me walk you through the architecture, because calling this thing a “pedalboard” at this point feels legally inaccurate.

### The User Interface

Let's start with the control surface: the StreamDeck.  This is where I pretend I’m not just playing, I’m deploying changes to production, choosing the set list moments before the show. Every button is a high-level command: “change the pattern,” “go to my backing tracks,” “make this sound expensive.”

The Companion app is straightforward. It recognized the StreamDeck and configured it automatically. I had to spend some time to populate a couple of pages with useful information and actions. My approach is to use the top row as a kind of status bar. The top left button switches to a debug page and the two top right buttons switch to a Helix and a BeatBuddy controller.

The main page is a mix of things I use to create loops: the loop templates and my favorite drum patterns.

There are three special buttons in the top row that act as the current state of the whole thing. One gives me the current Helix snapshot, the next one tells me where the guitar is located in the sound stage and the third tells me the time signature for the current drum pattern.

I've probably spent more hours messing around the Companion software and testing ideas for the user interface than actually playing through the rig. I burned countless hours just to decide the colors to use for each segment.

Like any piece of software, this thing will never be complete, but will always be ready.

### The Looper

Let's move to the boss (pun intended). At the center of the system, we have the brain… or at least the thing that thinks it’s in charge: the Boss RC-600. This is the scheduler, the timeline, the keeper of loops. It speaks in MIDI clock, which is basically its way of saying “trust me bro”.

I've divided its 99 memory blocks into three separate categories:

1. Loop templates
2. Loop songs
3. Backing tracks

The templates are there to store basic loop settings (like no rhythm sound) and the time signature, since the RC-600 doesn't expose this setting for external modification via MIDI messages. The idea is to use any of the templates to create the tracks and then store the result in one of the blocks for the Loop songs.

Wait a minute. Did I say I don't have rhythm sound coming from the looper? Yeah, that's true. While the RC-600 has pretty capable rhythm features, its sound is not as good as the BeatBuddy. Plus, the BeatBuddy has a really well designed interface that allows me to not have to deal with adjusting every single preset on my looper if I decided to change how it reacts to MIDI messages... yes, this configuration can't be stored as global (like the rest of the settings). I don't like wrestling with my pedals, so I hired a drummer that helps me keeping my sanity check.

Actually, let's go to the BeatBuddy.

### The Drummer

On the drums, we’ve got the BeatBuddy.  Think of it as a deterministic drummer. It never rushes, never drags, never shows up late, and never asks to play a jazz version of your song mid-performance. It just executes. Honestly, a bit intimidating. (Maybe that's why Singular Sound added a drunk mode to it.)

I added two particular folders to my BeatBuddy, one for the favorite patterns, so the process of activating and organizing them gets easier. I choose 16 and mapped them in the StreamDeck XL. Every time I push a button, the Raspberry Pi sends the MIDI messages required to change the pattern.

The second folder is where I store the patterns for the songs I create. Since I'm not using the native sounds of my looper, I had to store this information elsewhere. The problem with mapping each song to a pattern is that I would need to manually do the mapping each time I create a song, and this process requires access to the Raspberry Pi from a web browser. It's time to use some of my poorly acquired programming skills.

When programming software, using conventions over configurations is almost always a better choice. Since I adopted a range of memory banks for the songs, I correlated them to a particular folder of patterns inside the BeatBuddy.

The process now gets way easier. After I select a pattern for a new song, I just need to open the BeatBuddy manager on my local machine, copy the pattern to the position in the folder that matches the position of the song in the specific range of the looper, and sync the changes with the BeatBuddy's SD card.

With the sync in place, I just need to select a song in the looper and the respective drum pattern will be selected right after. Of course, some component needs to apply the convention and send the correct MIDI messages to trigger the change in the BeatBuddy.

But how to calculate and send the correct MIDI messages? It's time for the middleware layer.

### The Middleware

Now, things start getting weird.

Because sitting quietly underneath it, pretending to be harmless, is a Raspberry Pi. This is not a pedal. This is a middleware layer. It listens, translates, orchestrates, and occasionally makes executive decisions that may break things and cause unrepairable embarrassments. It’s the reason pressing one button can trigger the entire rig like a well-coordinated flash mob.

Under the hood, it’s just firing off messages and trusting the rest of this crazy distributed system will receive them and behave accordingly.

It's a known fact that distributed systems only have two challenges:

2- Sending the message just once  
1- Sending the messages in order  
2- Sending the messages just once

Inside the Raspberry Pi, there's a software from Bitfocus called Companion. If everything else in this setup is a collection of instruments and devices, then Companion is the translation layer between what I want and what actually happens. Because, let's be honest, none of these devices were designed to talk to each other like this. They all speak MIDI... but with accents. Strong ones.

Companion is the diplomat. From a programming perspective, this is the control plane. It's also where things get opinionated. Because once you have variables, triggers and conditional logic, your pedalboard becomes programmable. And once that happens... there's no going back.

For example, every time a song is selected in the looper, Companion decides whether that should trigger a change in the BeatBuddy and changes the internal state of the rig, marking which segment of the looper is active (templates, songs, backing tracks) and letting this information available to the user interface. Companion also receives user intent and translates that intent in MIDI messages, like the intent to change the template to a "4/4", which gets translated to a MIDI Program Change that will be (hopefully) received (just once) by the looper.

Installing and using the Companion app was easier than falling off a skateboard. After a couple of adjustments, I developed a set of guidelines that helped me be more productive and deal with potential issues around the road:

- No magic numbers, everything (or at least the majority of it) is defined as custom variables.
- Use local variables for the buttons to decouple logic and value. This makes it easier to copy the buttons and change what they trigger, but not how they trigger.
- Use a small wait between multiple MIDI messages. I made that waiting time configurable via custom variable too.
- For more complex logic, use a state variable that triggers actions in the trigger section. That allows for maximum flexibility, as buttons can now just populate parameters and send them as arguments to a function call, but in an even-driven fashion.

This is where I put most of my energy. Companion is flexible and has a variety of plugins, and luckily there's one for MIDI capabilities. It relies on the ID assigned to a MIDI device at the moment it's plugged. For Linux, this ID can change.

There are some ways of making sure you have a fixed way of referring to the MIDI device, but the plugin doesn't support them. I then open its source code and found a particular line that I could change and use just the name of the device. There's a ":" in the device name which separates the name and its id. I just used the name to lookup the first device with a similar name in the list of recognized devices. This could cause issues if there were multiple similar devices, but for my use case it's not going to be a problem.

And that's Open Source in a nutshell: it's free of cost, but not free of effort. The key part hidden in the effort is the freedom to modify anything to suit your own need, and that alone dwarfs any possible paid solution for a crazy guy like me.

Now I'm realizing something: what's a guitar rig with no guitar sound? Let's move to the tone.

### The Modeler

Alleviating the deterministic jailing aspects of those previous components, let's take it easy and talk about something that, apparently, has more freedom to go: the tone.

Ah yes… tone. I love that crazy controversy where people say "it's in the wood".

Right! Because when you plug into a fully digital signal chain, run through converters, DSP, impulse responses, stereo routing, and enough processing power to simulate a weather system... the real bottleneck is the tree.

Tone is everything happening after the cable leaves the guitar. In other words: tone is in the system. Especially inside MIDI CC values which control how a bunch of DSP blocks will process my guitar signal after I pluck the strings.

I'll be honest here. I'm quite far from being a sound expert, but I did my best at making 3 solid snapshots that sounds good to my taste:

- A clean sound
- A crunchy sound that's suitable for rhythms and general solos
- A lead sound that makes me think I can shred

The forth snapshot is always an experimental one. Right now I'm having fun with the acoustic simulator while I don't fix my real acoustic guitar.

I've setup the preset in a way that I can alter the level and pan using MIDI messages. This allows me to place the sound exactly where I want for maximum disturbance in the force. This plays nice when I'm designing loops, as I can easily construct the layers without delving into multiple knobs. I have a fully setup 6-track template for my loops, but it's always nice to prove you're wrong, and having a super flexible way of challenging my own choices is definitely a good start.

The Helix can also trigger the BeatBuddy for additional time control. I can trigger the Half, Double and Normal time, which allows for some crazy changes depending on the pattern and the tempo I'm using. I still suck at making something useful out of it, but I have hopes that I will suck less over the time.

Another interesting piece of my preset is the extra input with its own set of blocks for my chaotic synthesizer. I plug it straight on my Helix and mix it with my guitar sound applying the opposite pan of the guitar. That untangles the sound when I (try to) play both at the same time.

And now that I mentioned the synth, we're approaching the chaotic part of this rig, at least in terms of sound. Leaving pretty much all the cold and predictable aspects of a looping system, where order matters and has to be strictly followed, there's a little device sitting in the corner... ready to break any rules of time.

### The Chaos

I'm only proficient with a keyboard when I'm writing software, not music. The Arturia MicroFreak was able to put me in a comfortable place with its unique design that looks like someone tried to build a mini piano using a touchscreen and then stopped halfway to ship the beta because it was already killing.

This is not just a synth. In system terms, this is the chaos engine. While everything else in the rig is busy being deterministic, synchronized, and emotionally stable... the MicroFreak is out here exploring alternate timelines.

It doesn’t just generate sound, it negotiates with it. One moment it’s a delicate pad, the next it’s speaking in tongues, and somehow it’s still technically in key... most of the time.

From a programming perspective, it's thatr rogue service in your architecture that:

- nobody fully understands
- does things no other component can do
- and if you remove it, everything else still works… but feels suspiciously boring

It’s also the only instrument here that feels like it’s collaborating instead of obeying. You don’t control the MicroFreak, you make suggestions and hope it agrees.

And yet, when it locks in, the absolute weirdness of it all lines up with the rest of the system. That’s when things stop sounding like a setup and start sounding like something alive.

Every system needs structure. But sometimes, you also need a little bit of beautifully contained chaos.

Its output is a tad lower than the regular rig volume, so I gave it a little boost in the Helix before applying the effects: just a chorus and a delay. I'm yet to find a situation where I need to turn them off, so they're always on. Sometimes I explore alternating the time parameters of both delays, so both guitar and synth get interlaced in the stereo spectrum.

As I mentioned, the MicroFreak isn't tied to the MIDI chain. It acts as a disconnected system to preserve it's unique function: asynchronously generating controlled chaos without being disturbed by MIDI messages it doesn't care about. This forces me to become the bridge between the cold deterministic system and the wild chaos engine.

And if I need to use an arpeggiator with some temporal constraints... well... the looper can figure out the tempo if it's the first track I record.

What I'm really enjoying in the MicroFreak is it's organic nature outside of the deterministic grid imposed by the looper-drummer couple. Its aftertouch made by how much flesh you have in the proto-keyboard and how many parameters you can change in the matrix creates a whole new world of exploration. While my guitar tone is in the system, the MicroFreak tone is almost in the randomness. That feeling of knowing things might land a bit different, but that variance will add that beautifully contained chaos, makes me willing to defy the rules set by the time couple. If something is slightly out of beat or tune, a flesh-accent is all you need to increase the tension and hook everything back.

This is insanely fun. I can spend hours tweaking and having a great time trying to not destroy my hearing. I love that thing and hope I can become proficient enough to introduce it more in my playing. This chaos should be earned, not a result of a sloppy moment.

## The End

This isn’t just gear. This is:

- a loop engine
- a rhythm engine
- a tone engine
- a chaos engine
- a middleware layer
- and a user interface

All loosely coupled, mildly synchronized, and held together by duck tape, cable ties, MIDI messages and questionable confidence.

In other words: it’s a perfectly normal setup for a guy like me.

Hope it compiles.
