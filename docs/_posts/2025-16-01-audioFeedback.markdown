---
layout: post
title:  "Audio Project Feedback"
date:   2025-01-16 04:09:57 +0100
categories: jekyll update
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/V0fn0oI1Bas?si=APUykjPe3xNPQY18" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br><br>

I just received my grade for my audio project.<br>
I was hoping to receive a B for the project, to inch closer to graduating with a 2:1 GPA, and I'm very pleased to say that a B is what I received! <br><br>

Overall, the instructor thought it was a very good project. However, it had some glaring flaws, and I received a bunch of very helpful feedback, which I'll be discussing in this post.

<h1 style="font-size:300%;"> Feedback </h1>

<b>Point 1:<br>
<i>No evidence that you've engaged with your audio engine's build process for audio files. Modern audio engines have specific build processes that dictate how sound files are packaged for your game. This is where knowledge of compressed file formats is vital for modern game audio implementation. Your project appears to use the default settings for all of its audio assets. (in Unity, these settings are defined in the Import Settings for audio assets)</i><br><br></b>
Okay, alright, you got me. I'll be completely honest; I forgot. As a result, all of the audio files ended being converted to the same format, which completely undermines any optimisation done outside Unity. Which leads to the second point...<br><br>
<b>Point 2:<br>
<i>Original sound files stored in a compressed format. This means those sounds will have been compressed twice; once when originally rendered, and a second time when you build the game.</i><br><br></b>
Like above, this could have been avoided by engaging with Unity's build process for audio files.<br><br>
<b>Point 3:<br>
<i>One or more spatialised sounds are stereo files. Applying audio engine spatialisation to a file that is already in stereo will usually cause problems, as stereo files usually have their own stereo information baked into the file. Attempting to apply audio engine spatialisation to a file that is already hard panned left (for example) in the file itself will result in the game spatialisation not working correctly. (specifically the enemy sounds)</i><br><br></b>
What I'm gathering from this feedback is that I should have made the hard panned enemy sound a mono file, which makes sense, since there's no need for stereo capability for that particular file. Playing devil's advocate, though, it gave the desired effect in my game.<br><br>
<b>Point 4:<br>
<i>The background music does not loop cleanly. Either it has clicks or glitches at the loop point or (more commonly) the music is left to fade out before the loop restarts. (specifically m_danger has a short section of silence at the start, which is very noticeable when the sound loops)</i><br><br></b>
m_danger is the one, ominous tone heard on the second screen of the game. In this case, the fadeout is intentional; I tried to have it play continuously, but this ended up being incredibly annoying to listen to, so I changed it to be this way. The other music pieces may have problems too, which could have been solved by cutting them properly; I'm not an audio engineer, though, so I did the best I could.<br><br>
<b>Point 5:<br>
<i>Code elements do not appear to be designed with scalability in mind. (a lot of the code relies on hard-coded values, which would make it very hard to scale this approach up to a larger project. Some examples are CameraPositioner's hard-coded enemies, and the movementClips and voiceClips in AudioTester.cs; not only does the code expect these arrays to be a set size (e.g. line 71, voiceClips[Random.Range(0,2)]), but the arrays actually contain a variety of different sounds, used in different contexts)</i><br><br></b>
This specific point represents a crossroads I faced during development. One thing I haven't mentioned is that I had to start over from scratch halfway through the project, as I wanted to utilize trademarked assets under Fair Use; this wasn't allowed. This meant I didn't have as much time to clean and optimize code as I'd have liked. So, I was left with a choice: Should I spend the extra time making the code scalable and expandable, or just go for something that works? In the end, I went with something that works for this particular project. That being said, scalability should always be a priority in any software project. I'd like to write a future blog post on scalability, so stay tuned for that!<br><br>
<b>Point 6:<br>
<i>Reverb is applied individually to multiple game objects using the Audio Reverb Filter Component. This is a very inefficient way of implementing reverb. If you have multiple audio sources that you want to apply the same reverb settings to, the correct solution is to add a Reverb group in the Audio Mixer, and route those sounds to that group. This means you can run a single reverb process instead of individual processes for each sound, and can significantly save on CPU usage. (specifically the enemy and player game objects; this approach also makes it hard to cope with different environments, were you to expand the game in future)</i><br><br></b>
This one's on me again, as I did not do much work with Audio Mixers, apart from applying a low-pass filter.

<br><br>

Anyway, that's all the feedback I got. Most of it was oversight on my part, a few points were due to choices I'd made. Hopefully, this post is useful in some way to you!