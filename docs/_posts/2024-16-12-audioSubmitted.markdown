---
layout: post
title:  "Unity and Audio"
date:   2024-12-16 04:09:57 +0100
categories: jekyll update
---
Today, I uploaded my final submission for the audio module at university.<br>
While I'm very pleased at how it ended up, it had a rough start.<br>
Basically, I didn't read the assessment brief, and tried to recreate Abe's Oddysee, assets and all!<br>
Because of this, I had to start over in the middle of the project.<br>
In the end, I created a similar project with free-to-use assets.<br><br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/V0fn0oI1Bas?si=APUykjPe3xNPQY18" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br><br>
The project contains spatial localisation, attenuation, reverb and many other interesting audio buzzwords.<br>
The core design principle for the game was "simplicity". Basically, I wanted to see how effective Unity's built-in audio handler was at processing audio for a simple project.<br>
While this meshed well with the scope of this project, if it were to be any bigger, I would have implemented third-party audio software, like Wwise or Fmod.

<h1 style="font-size:200%;"> A brief overview of the project </h1>
<img src="/assets/CMP407system.png" alt="System architecture" style = "width:750px;height:400px;"><br><br>
The core of the project is a dynamic music system, which plays music based on the player's position relative to the enemy.<br>
It's based on a state-machine, and looks like this:<br><br>
<b>Calm</b><br>
There are no enemies near the player. The music player will play short pieces of music every 10-15 seconds.<br>
<b>Danger</b><br>
There is an enemy one screen away. The music fades to a very ominous track, and footsteps can be heard from the next screen over.<br>
<b>Imminent danger</b><br>
There is an enemy on screen. The music fades to an oppressive track, which will loop as long as the player remains. In the background, a timer is started - more on that later.<br>
<b>Hunted!</b><br>
An enemy has seen the player, and is actively hunting the player. The music switches to a frantic track which will override any other state, until either the enemy or player is dead.<br>
<b>Dead</b><br>
The player has died. A short, disappointing track plays.<br>

<h1 style="font-size:200%;"> A word on music transition </h1>

The singular most challenging part of this project was to seamlessly transition between the "imminent danger" and "hunted" tracks.<br>
While you can ask Unity to wait until an audio piece has ended to play another, it's a bit more difficult to get it to play an audio track exactly at a specific time.<br>
For this project, I wanted the music to be played at the end of the current bar* of music.<br>
In order to calculate the length of a bar, I had to do a few rudimentary calculations.<br><br>

First, I calculated the tempo of the track via Garage Band on my iPhone, which turned out to be 110 BPM.<br>
Then, I divided this number by 60, in order to get the beats per second.<br>
With the beats per second calculated, I simply had to multiply by 4, in order to get the duration of a bar.<br>
I then started a timer when the player enters the "danger" state, and when this timer reaches the calculated duration, it can change to the "hunted" track.<br>
<i> * A bar of music is the amount of beats indicated by a time signature. For 4/4 time signature, this is 4 beats, while for 3/4, it would be 3 beats.</i><br><br>

And that concludes my project!<br>
Thanks for reading.

