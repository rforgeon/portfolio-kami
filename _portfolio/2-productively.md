---
layout: page
title: Productively
thumbnail-path: "images/ProductivelyOnDesktop.png"
short-description: Pomodoro inspired time tracker.

---



<div style="text-align:center; "><img src ="https://cldup.com/xgdRPXmNUo.png" /></div>

The Productively timer helps users sustain a productive, 9 hour work day while following [Pomodoro](https://en.wikipedia.org/wiki/Pomodoro_Technique) time management.


<h3 style="color:blue; text-align:center;"><a href="http://bit.ly/productivelyDL" download="">⬇️ Download for Mac!</a></h3>
<p style='margin-top:-25px;font-size:10px;text-align:center'>then: ctrl click > open </p>

<br>
<br>
<br>
<br>



## Problems ➡️ Solutions

<div style="text-align:center; -webkit-mask-image:-webkit-gradient(linear, left top, left bottom, from(rgba(0,0,0,1)), to(rgba(0,0,0,0))); "><img style="width:40vw" src ="https://cldup.com/i_g1wzXF3l.gif" /></div>

## Problem (A): Organizing My Reducers

I started with one **Timer** reducer, used to control multiple types of timers (i.e. a **work timer**, **short break timer**, and **long break timer**).

I was initially switching between these timers in a long conditional statement in the **Timer** component. However, this code had a poor [smell](https://en.wikipedia.org/wiki/Code_smell).

<div style="text-align:center; -webkit-mask-image:-webkit-gradient(linear, left top, left bottom, from(rgba(0,0,0,1)), to(rgba(0,0,0,0))); "><img style="width:25vw;" src ="http://i.giphy.com/mpxvACn6oda7e.gif" /></div>
<br>

My reducer was very long, and included many actions that would be repetitive to each timer.


```javascript
var defaultSate ={
  seconds: 1500,
  isRunning: false,
  cycleIndex: 0,
  initTimer: false,
  currentTimer: 0,
  onBreak: false,
  totalTime: 0,
  timeSinceInit: 0
}

function timer(state = defaultState, action){

  const i = action.currentTimer;

  switch(action.type){


    case 'INIT_WORK_TIMER' :

      return {
        ...
      }

    case 'INIT_SHORT_BREAK_TIMER' :

      return {
        ...
      }

    case 'INIT_LONG_BREAK_TIMER' :

      return {
        ...
      }

    case 'INIT_TIMER' :

      return {
        ...
      }

    case 'INCREMENT_TOTAL_TIME' :

      return {
        ...
      }

    case 'INCREMENT_TIME_SINCE_INIT' :

      return {
        ...
      }

    case 'RESET_TOTAL_TIME' :

      return {
        ...
      }

    case 'DECREMENT_TIMER':
      return [
      ...
      ]

    case 'PAUSE_TIMER' :

      return [
      ...
      ]

    case 'RESET_TIMER' :

      return [
        ...
      ]

    case 'INCREMENT_CYCLE_INDEX':

      return [
        ...
      ]

    default:
      return state;
  }
}

```  

## Solution (A): Organizing My Reducers

I proceeded to create a Master Timer that includes an array of "timerItem" objects.

```javascript
var workTimerItem = {
  seconds: 1500,
  isRunning: false,
  cycleIndex: 0,
  id: 0
}

var shortBreakTimerItem = {
  seconds: 300,
  isRunning: false,
  cycleIndex: 0,
  id: 1
}

var longBreakTimerItem = {
  seconds: 1800,
  isRunning: false,
  cycleIndex: 0,
  id: 2
}

var timer = {
  timerItems: [workTimerItem, shortBreakTimerItem, longBreakTimerItem]
}
```

This has allowed me to more easily move between my different timers. The new reducers are now split into a **"timerItem"** Reducer and **"timer"** Reducer.


**"timerItem" Reducer 👇**

```javascript
var workTimerItem = {
  seconds: 1500,
  isRunning: false,
  cycleIndex: 0,
  id: 0
}

var shortBreakTimerItem = {
  seconds: 300,
  isRunning: false,
  cycleIndex: 0,
  id: 1
}

var longBreakTimerItem = {
  seconds: 1800,
  isRunning: false,
  cycleIndex: 0,
  id: 2
}

var timer = {
  timerItems: [workTimerItem, shortBreakTimerItem, longBreakTimerItem]
}

function timerItem(state = timer.timerItems,action){
  const i = action.id;

  switch(action.type){

    case 'DECREMENT_TIMER':
      return [
        ...
      ]

    case 'PAUSE_TIMER' :

      return [
        ...
      ]

    case 'RESET_TIMER' :

      return [
        ...
      ]

    case 'INCREMENT_CYCLE_INDEX':

      return [
        ...
      ]

    default:
      return state;
  }
}
```  


**"timer" Reducer 👇**

```javascript
var defaultState = {
  initTimer: false,
  currentTimer: 0,
  onBreak: false,
  totalTime: 0,
  timeSinceInit: 0
}

function timer(state = defaultState, action){

  const i = action.currentTimer;

  switch(action.type){


    case 'INIT_WORK_TIMER' :

      return {
        ...
      }

    case 'INIT_SHORT_BREAK_TIMER' :

      return {
        ...
      }

    case 'INIT_LONG_BREAK_TIMER' :

      return {
        ...
      }

    case 'INIT_TIMER' :

      return {
        ...
      }

    case 'INCREMENT_TOTAL_TIME' :

      return {
        ...
      }

    case 'INCREMENT_TIME_SINCE_INIT' :

      return {
        ...
      }

    case 'RESET_TOTAL_TIME' :

      return {
        ...
      }

    default:
      return state;
  }
}
```

## Results

This refactoring has made my code much more logical and organized.

<br>
<br>

## Project Design

<div style="text-align:center; -webkit-mask-image:-webkit-gradient(linear, left top, left bottom, from(rgba(0,0,0,1)), to(rgba(0,0,0,0))); "><img src ="http://i.giphy.com/3o6ZteZyWPqKgynJGU.gif" /></div>

<br>

## 🔎 UX

I took a [Job Story](https://jtbd.info/replacing-the-user-story-with-the-job-story-af7cdee10c27#.gbjooeabd) approach to my user experience.


![](https://cldup.com/zbM_T4eLmh.png)


## 👀 Visual

My first quick sketch was very simple and only implemented the final main timer with ring.

![](https://cldup.com/7RcdTyz2cF.png)

I then took this concept in addition to my job story and created a Sketch with material design.

I used Google's material [color guides](https://material.io/guidelines/style/color.html#).

![](https://cldup.com/7g3IP04vLD.png)

In addition to their material [shadow guides](https://material.io/guidelines/material-design/elevation-shadows.html#elevation-shadows-elevation-android).

![](https://cldup.com/68Q_50WcsM.png)

The original Sketch came out as the following...

![](https://cldup.com/sJEO3XmCk4.png)

and the final outcome (actual app)...

![](https://cldup.com/7wl4LYoilo.png)

The bottom timeline arch is a visual representation of your day. Each small circle is a twenty five minute work timers, each followed by a five minute break timer (not represented on the arch timeline). The arch also includes three, thirty minute long break timers. A long break occurs after four consecutive work timers.

The top timer is used to visually represent your current timer. This time is represented both in minutes:seconds and by a deprecating ring.

<h1 style="color:blue; text-align:center;"><a href="http://bit.ly/productivelyDL" download="">⬇️ Download for Mac!</a></h1>
<p style='margin-top:-10px;font-size:12px;text-align:center'>then: ctrl click > open </p>


## Conclusion

**What Worked?**
<br>
Redux state proved to be a very nice way to keep time and move between multiple timers.


**What were your doubts going into the project?**
<br>
Timeline for project completion.

**What surprised you the most?**
<br>
How quickly the styling came together.

**What would you have done differently?**
<br>
Further imbed the timer into the mac tray allowing for less upfront UI and a more streamlined user experience.

**What did you learn while doing this project?**
<br>
I learned how to create electron desktop apps and how to implement material design while improving my knowledge of Redux.

**How will you use that information in the future?**
<br>
I will further my Redux development and use both material design and desktop development.

## More

See how I worked with React + Redux in my [ride sharing discovery app 👉](http://www.forgeon.info/portfolio/1-myTopStop/)
