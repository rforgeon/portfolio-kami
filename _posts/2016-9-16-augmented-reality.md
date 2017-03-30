---
layout: page
title: Toying with Augmented Reality
feature-img: "https://cldup.com/yKNshWjCfz.png"

---

<div style="text-align:center; "><img src ="https://cldup.com/yKNshWjCfz.png" /></div>

<br>

I started getting interested in augmented reality when a learned about Magic Leap (or more so the idea for Magic Leap) back in the early 2015.

Magic Leaps founder, Rony Abovitz, had this obscure demo app out. Unfortunately, it no longer exists. The app provided you with a link to a print out (later to find out this is a target). When you point your phone's camera at the target, an animated robot popped up, looked at you, and made some screeching robot noises before disappearing again.

After looking into it further. I found that Qualcomm had developed some software for generating a connection to these targets. This was paired with Unity (a game development software).

Since both a Vuforia and Unity starter account is free, I hopped in and started hacking.

The best beginner resource I recommend is a tutorial found on [Danny Goodayle's blog](http://www.dannygoodayle.com/2013/03/01/making-your-first-project-with-unity-and-augmented-reality/).

From there, I started with **static targets**, played with **dynamic targets**, then got into **facial tracking**. Take a look 👀

## Static Target

<div style="text-align:center;">

  <!-- "Video For Everybody" http://camendesign.com/code/video_for_everybody -->
  <video controls="controls" width="450" height="400">
    <source src="https://instagram.fsnc1-2.fna.fbcdn.net/t50.2886-16/11773027_1477125979265254_973512356_n.mp4" type="video/mp4" />
    <object type="application/x-shockwave-flash" data="http://releases.flowplayer.org/swf/flowplayer-3.2.1.swf" width="450" height="400">
      <param name="movie" value="http://releases.flowplayer.org/swf/flowplayer-3.2.1.swf" />
      <param name="allowFullScreen" value="true" />
      <param name="wmode" value="transparent" />
      <param name="flashVars" value="config={'playlist':[{'url':'https%3A%2F%2Finstagram.fsnc1-2.fna.fbcdn.net%2Ft50.2886-16%2F11773027_1477125979265254_973512356_n.mp4','autoPlay':false}]}" />
      <span title="No video playback capabilities, please download the video below">Coke-a-cola</span>
    </object>
  </video>

    <!-- "Video For Everybody" http://camendesign.com/code/video_for_everybody -->
  <video controls="controls" poster="https://instagram.fsnc1-2.fna.fbcdn.net/t51.2885-15/e15/11881621_506472989517048_1110307166_n.jpg?ig_cache_key=MTA2ODE4NTIxMDMzNDE1NDQ5Mw%3D%3D.2" width="500" height="400">
    <source src="https://instagram.fsnc1-2.fna.fbcdn.net/t50.2886-16/11948815_522770874541941_470873750_n.mp4" type="video/mp4" />
    <object type="application/x-shockwave-flash" data="http://releases.flowplayer.org/swf/flowplayer-3.2.1.swf" width="500" height="400">
      <param name="movie" value="http://releases.flowplayer.org/swf/flowplayer-3.2.1.swf" />
      <param name="allowFullScreen" value="true" />
      <param name="wmode" value="transparent" />
      <param name="flashVars" value="config={'playlist':['https%3A%2F%2Finstagram.fsnc1-2.fna.fbcdn.net%2Ft51.2885-15%2Fe15%2F11881621_506472989517048_1110307166_n.jpg%3Fig_cache_key%3DMTA2ODE4NTIxMDMzNDE1NDQ5Mw%253D%253D.2',{'url':'https%3A%2F%2Finstagram.fsnc1-2.fna.fbcdn.net%2Ft50.2886-16%2F11948815_522770874541941_470873750_n.mp4','autoPlay':false}]}" />
      <img alt="Big Buck Bunny" src="https://instagram.fsnc1-2.fna.fbcdn.net/t51.2885-15/e15/11881621_506472989517048_1110307166_n.jpg?ig_cache_key=MTA2ODE4NTIxMDMzNDE1NDQ5Mw%3D%3D.2" width="500" height="400" title="No video playback capabilities, please download the video below" />
    </object>
  </video>
  <br>

  <!-- "Video For Everybody" http://camendesign.com/code/video_for_everybody -->
  <video controls="controls" poster="https://instagram.fsnc1-2.fna.fbcdn.net/t51.2885-15/e15/12362486_1497196783917591_145230436_n.jpg?ig_cache_key=MTE0MTYyNTc1MzI4MTY5NTMzMg%3D%3D.2" width="500" height="400">
  	<source src="https://instagram.fsnc1-2.fna.fbcdn.net/t50.2886-16/12368959_1017758238282931_1901270271_n.mp4" type="video/mp4" />
  	<img alt="Starbucks AR" src="https://instagram.fsnc1-2.fna.fbcdn.net/t51.2885-15/e15/12362486_1497196783917591_145230436_n.jpg?ig_cache_key=MTE0MTYyNTc1MzI4MTY5NTMzMg%3D%3D.2" width="250" height="300" title="No video playback capabilities, please download the video below" />
  </video>
  <br>


</div>  

## Dynamic Target

<div style="text-align:center;">
  <video controls="controls" width="450" height="400">
  	<source src="https://instagram.fsnc1-2.fna.fbcdn.net/t50.2886-16/12461691_1194397447255757_1386843048_n.mp4" type="video/mp4" />
  	<span title="No video playback capabilities, please download the video below">Coke-a-cola</span>
  </video>
  <br>
  <video controls="controls" width="450" height="400">
  	<source src="https://static.everyplay.com/everyplay/videos/30925389/24898904/m31-1500.mp4" type="video/mp4" />
  	<span title="No video playback capabilities, please download the video below">Coke-a-cola</span>
  </video>
</div>

## Facial Tracking

<div style="text-align:center;">

  <video controls="controls" width="450" height="400">
  	<source src="https://static.everyplay.com/everyplay/videos/30925389/25850467/m31-1500.mp4" type="video/mp4" type="video/mp4" />
  	<span title="No video playback capabilities, please download the video below">Coke-a-cola</span>
  </video>


  <video controls="controls" width="450" height="400">
  	<source src="https://static.everyplay.com/everyplay/videos/30925389/27170009/m31-1500.mp4" type="video/mp4" type="video/mp4" />
  	<span title="No video playback capabilities, please download the video below">Coke-a-cola</span>
  </video>

</div>
