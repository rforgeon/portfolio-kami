---
layout: page
title: My Top Stop
thumbnail-path: "https://cldup.com/52lKD4DvF8.gif"
short-description: Explore and share your top Lyft destinations.

---



<div style="text-align:center"><img style="width:30vw" src ="https://cldup.com/52lKD4DvF8.gif" /></div>

Explore and share your top Lyft destinations from the past year. Receive recommendations for similar destinations you might like.

🔥 Try it now at [mytopstop.com](http://mytopstop.com/)!

<br>

<div style="text-align:center; -webkit-mask-image:-webkit-gradient(linear, left top, left bottom, from(rgba(0,0,0,1)), to(rgba(0,0,0,0))); "><img style="width:25vw" src ="http://i.giphy.com/WAFNKlENoOcPC.gif" /></div>




## Problems ➡️ Solutions

<br>
<br>
<br>

<div style="text-align:center; font-size:200px ">A</div>

<br>
<br>
<br>
<br>

## Problem (A): Pivot

I learned a valuable lesson to fully understand the abilities and limitations of an external API before building an app around it.

My initial idea for this project was to create a dashboard that informed a user of their Lyft ride's estimated ride time vs. actual ride time.

![](https://cldup.com/2DFrQIg_qi.png)

Lyft does not save the estimated ride time, it is only accessible at the beginning of a ride. My workaround for this was to create a webhook on my API that would save the estimated ride time when a ride was started. I had saved authentication tokens for Lyft, so I assumed that once a user connects with my app, I could receive webhooks of their estimated ride time when they started a ride through the Lyft app...

**Wrong.**

![](https://cldup.com/bv1PcLII2w.png)

I would only have access to this data if the user requested a ride through my app rather than the Lyft app. This drastically altered my concept for a passive app and I decided to rethink my approach.

## Solution (A): Pivot

I landed on the idea of my current app, My Top Stop. With a user's historic Lyft rides, I could still create some value in combining additional API's - Google maps and Yelp.

## Results (A): Pivot

I'm actually much happier with the new design of the app. My Top Stop is much more interactive and social than my original design. This was a good lesson in implementing your design due diligence before building.

<div style="text-align:center; ">•••••••••••••••••••</div>

<br>

<div style="text-align:center; font-size:200px; ">B</div>

<br>
<br>
<br>
<br>

## Problem (B): Multiple Middleware: Automation and Sequencing

The challenge here was to implement multiple different API calls through middleware when loading the app.

## Solution (B): Multiple Middleware: Automation and Sequencing

Once you login through Lyft, what needs to happen?

* Fetch the past year of Lyft rides
* Sort your Lyft rides by most duplicates first, followed by most recent
* Fetch three Yelp locations near your Lyft destination
* Fetch recommendations based on your top three destinations

This all happens during the load screen:

![](https://cldup.com/sFSK5D-7U1.png)

There is a nice way to implement multiple middleware at once. This can be done by using [redux-multi](https://github.com/ashaffer/redux-multi) to create an action that dispatches an array of actions.

```javascript
function initDashboard () {
  return [
    fetchLyftRides(),
    sortLyftRides(),
    fetchYelpLocations(),
    fetchYelpRecommendations()
  ]
}
```

This is a good start for automating multiple middleware scripts at once, however, we run into a new problem.

When calling the action **initDashboard()**, we will fire a dispatch for each action in the array. **fetchLyftRides()** will begin, and immediately after, **sortLyftRides()** will begin. While **fetchLyftRides()** is calling the Lyft API, the **sortLyftRides()** middleware will begin trying to sort the fetched rides. If **fetchLyftRides()** has not completed yet, we will return an incomplete, inaccurate sorted list of rides.

To avoid this problem using multiple middleware, we need to make sure they complete in order:

1. Fetch the past year of Lyft rides
2. Sort your Lyft rides by most duplicates first, followed by most recent
3. Fetch three Yelp locations near your Lyft destination
4. Fetch recommendations based on your top three destinations

In order to sequence my middleware, I have my middleware listen for when the previous middleware is successfully completed:

```javascript
const recommendationMiddleware = store => next => action => {

  if (action.type === 'FETCH_YELP_SUCCESS') {
    if(!store.getState().fetcher.isFetchingRecommendations) {
      fetchResultsRequest(store, action);
    }
  }
  next(action);
  return action;
}
```

Okay, so this works for dispatching multiple middleware sequentially, but what if I want to call this middleware individually?

That is also possible by creating the middleware's own action and also listen for it in the fetch logic:

```javascript
const recommendationMiddleware = store => next => action => {

    if (action.type === 'FETCH_RECOMMENDATION_REQUEST' || action.type === 'FETCH_YELP_SUCCESS') {
      if(!store.getState().fetcher.isFetchingRecommendations) {
        fetchResultsRequest(store, action);
      }
    }
    next(action);
    return action;
  }

```  

## Results (B): Multiple Middleware: Automation and Sequencing

By implementing this form a sequencing through my middleware, I'm able to organize and separate my middleware, and at the same time, assure that they fetch in the correct order.

<br>

<div style="text-align:center; ">•••••••••••••••••••</div>

<br>

<div style="text-align:center; margin-left:-17px; font-size:200px; ">C</div>

<br>
<br>
<br>
<br>

## Problem (C): Decoupled API & Client

The challenge here was to create a modern decoupled app - Rails backend and React/Redux frontend.

The difficulties that arose were:
* 0Auth2
* User login and security
* Communicating params between client and API

## Solution (C): Decoupled API & Client

### 0Auth2

When connecting users to their Lyft account, Lyft requires an [0Auth2](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2) authentication. This is a common authentication method these days and can be implemented well with rails using [Omniauth](https://github.com/omniauth/omniauth).

Some common services even have specialized Omniauth "strategies" bundled into gems such as [Facebook](https://github.com/mkdynamic/omniauth-facebook).

Unfortunately, I could not find an open source Lyft Omniauth strategy. This forced me to create my own Omniauth strategy for Lyft.

This was a great learning experience in itself as Omniauth is a great middleware service to learn for Rails.

### User Login and Security

When creating a Ruby on Rails app, it is very easy to implement a fairly secure login. This is because your frontend is directly connected with your backend, allowing the app to know your current session at all times.

However, when your client is decoupled from your backend, and you must access it via an API, you must persist a login user token on your client side, and check it against your backend each time you communicate with your API.

Thankfully, there are some good tools out there for this exact problem.
I used these:

* Backend: [Devise Token Auth](https://github.com/lynndylanhurley/devise_token_auth)
* Frontend: [j-Toker](https://github.com/lynndylanhurley/j-toker)

I was surprised how much work has to be done to secure communication between API's and clients.

### Communicating Params Between Client and API

There are times when you need to communicate information back and forth between your client and API without creating an individual API call.

A good way to implement this is through URL parameters. I use URL parameters, "params," in two ways.

The first is by providing user identification params to my Lyft authentication callback. This allows me to match the correct user to the Lyft authentication token (In the my current build, this is deprecated).

The second is to communicate the Lyft authentication token to my client without saving it in my backend. I could increase security further by saving the Lyft token to my backend and masking it behind a separate ID. However, under the app's current permissions, the provided Lyft token only provides ride history information and expires after one hour.

Using params is a fast, useful, and light weight way to move information.

## Results (C): Decoupled API & Client

Having a decoupled API and Client is very valuable for scaling an app. In today's environment, an app has to come out the box almost immediately supporting multiple clients - whether web, mobile, desktop, or more.

Starting out with a decoupled API and client allows for an easier implementation of multiple clients. However, if speed of initial go to market is required, it's possible that decoupling is not the best route - that being said, decoupling will take more time later.

<div style="text-align:center; ">•••••••••••••••••••</div>

<br>

# Project Design

<div style="text-align:center; -webkit-mask-image:-webkit-gradient(linear, left top, left bottom, from(rgba(0,0,0,1)), to(rgba(0,0,0,0))); "><img src ="http://i.giphy.com/3o6ZteZyWPqKgynJGU.gif" /></div>

<br>

## 🔎 UX

I took a [Job Story](https://jtbd.info/replacing-the-user-story-with-the-job-story-af7cdee10c27#.gbjooeabd) approach to my user experience.


![](https://cldup.com/7zL2C03bC2.png)


## 👀 Visual

My first sketch laid out the material tiles.

![](https://cldup.com/oXBB9WILmE.png)

Most of the app was built with simple buttons before adding any styling.

![](https://cldup.com/t-p0fBtU48.png)

The original design had a persisted "Connect Lyft" button once the user connected.

![](https://cldup.com/F1J4Az4_Eq.png)

The final design provides a much clearer connection flow for intuitive use.

![](https://cldup.com/cLeW8oYAGs.png)

The "Connect Lyft" button is now only visible at initial entry and once the Lyft token expires (after 60 minutes).

![](https://cldup.com/SH96shWwXZ.png)

<div style="text-align:center; ">•••••••••••••••••••</div>


## Conclusion

**What Worked?**
I enjoyed the challenge of providing added value by creating an API mashup (Lyft, Google, and Yelp).
<br>


**What were your doubts going into the project?**
Successfully implementing a decoupled API and client.
<br>

**What surprised you the most?**
How much must be done to secure communication between API's and clients.
<br>

**What would you have done differently?**
Further due diligence before starting to build. On each project I develop, I learn new requirements I need to research before I start writing code.  

**What did you learn while doing this project?**
I learned how to create a decoupled API and client app, including security practices that go along with decoupling. I also learned a lot about working with API's - how to build them and how to implement them with a client.
<br>


**How will you use that information in the future?**
I'm confident I will use this information for future projects as many apps are becoming more decoupled. Additionally, most apps either use or provide API's.
<br>

## More

See how I worked with React + Redux to create a [Mac Desktop App  👉](http://www.forgeon.info/portfolio/2-productively/)
