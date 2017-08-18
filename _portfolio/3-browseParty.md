---
layout: page
title: Feature Build
thumbnail-path: "https://cldup.com/SEd1MOUqmK.gif"
short-description: Add a tracking feature to a finance app.
short-description-line2: ""
short-description-line3: "View Project Details"
---


# Finimize Challenge

## **Challenge:** Come up with a way for users to track progress towards their goals.


## Outline
1. Organizing Persona and Creating User [Job] Story.
2. Wireframing
3. Graphing & Sketch
4. Discoveries and Alterations
5. Framer Animation
6. Next Steps

## Organizing Persona and Creating User [Job] Story.

Our persona is Jason, a 26 year old, male, consultant, from London. He makes a "good" salary and his financial level is intermediate. This means "he’s never invested but he understands the basics of things and has been reading Finimize for some time."

I've organized Josan into a User Story using As a..., When..., I Want..., So...
Below is a preview of the story, but click [here](https://airtable.com/shriib91ZPRXZPMLf/tblCpRmyH2pHx5oiI/viwkChBkmkV4NldO1) to view the full document.

![](https://cldup.com/Ikl4oNQFvJ.png)

## Wireframing

After establishing what Jason's story might look like to track progress towards his goal, I began putting pen to paper. Bellow are a couple of my initial sketches. However, be sure to open the above 👆 Airtable User Story document to reference the sketches with each story line.

![](https://cldup.com/-vFGBQebfu.png)

While putting together some ideas, I immediately realized how useful [HighCharts](https://www.highcharts.com/) would be for this feature.

I began playing around with the HighCharts API to see if something could be created in line with my initial wireframing. Check out the JsFiddle [here](http://jsfiddle.net/cwgeg9r3/).

## Graphing & Sketch

Once I had an idea of how to layout the UI, I dove into Sketch. The starter template greatly helped to match Finimize's design.

This is where I brought together my wireframes, JsFiddle graph, and Finimize's design to show off a potential full package.

![](https://cldup.com/WwnYCBZVi7.png)
![](https://cldup.com/2Tmo5JuCBp.png)

## Discoveries and Alterations

While wireframing, I came to a discovery that allowed me to eliminate a step for the user in the tracking process.

You can see these steps in the "Deprecated" section of my AirTable User Story document.

I first asked the user if they had made any new savings in one modal screen, then asking them to enter the savings amounts in a second screen.

I decided to eliminate the first step and simply have the user click update with pre-filled ￡0 if they have not made any savings.

![](https://cldup.com/65zFp-jKn6.png)

## Framer Animation

To implement a more attractive input screen, I want to give the user a small feeling of reward for simply inputting a number. I do this by creating a wealth generation feeling in a coin collecting animation.

I created this animation using [Framer](https://framer.com/) connected to Sketch.  

![](https://cldup.com/SEd1MOUqmK.gif)

You can interact with the animation [here](https://framer.cloud/ZUeZj/).

## Next Steps

### Feature Role Out

🔴 Notification on the goal should allow for the majority of feature discovery and interaction. It also might be nice to have an Intercom notification of the visual tracking feature once a user hits the /goals page.

### Adding To The Feature

The current tracking feature doesn't allow a "reminder to save money" button. I like this feature in the /goals page as it allows a user to continue with the product but encourages them to come back at a later date. I would explore adding this to the feature.

![](https://cldup.com/UryOoGq8Eu.png)

This would email the user encouraging them to transfer the money and come to the app to update/review their results.

### User Follow-Up On Feature

Once in the hands of users, these are questions I'd like to see answered:

* When did you notice the feature? What did you think? Did you use it straight away?
* What attracted you to it?
* Were there any barriers to you using it?
* Have you told anyone about it? What did you say?
* What would you change to make this feature more enjoyable to use?

See how I worked with React + Redux in my [ride sharing discovery app 👉](http://www.forgeon.info/portfolio/1-myTopStop/)
