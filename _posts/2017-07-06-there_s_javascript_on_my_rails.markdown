---
layout: post
title:  "There’s JavaScript on my Rails!"
date:   2017-07-06 18:03:12 +0000
---


After months of writing Ruby, there comes a time when a young programmer must venture into the land of front-end development. While HTML takes care of the basics, JavaScript allows for a quicker, more dynamic user experience. Enter: Asynchronous JavaScript and XML, or Ajax for short.

The Ajax request allows for the browser and server to communicate and update without reloading the page. For our purposes here, the request requires only three things: a url, a method for accessing the url (i.e. post, get), and a function with instructions on how to load the response. The complex idea and fairly straightforward application allow a few additional features on top of Ruby on Rails projects. 

My project called Move, described in greater detail [here](https://jennafrancis.github.io/2017/05/23/life_on_rails/), allows users to view and review fitness classes in their metro areas. Formerly I nested the routes for group class show pages within each studio they belonged to. Now, I was able to render a similar show page without refreshing or displaying the nested route. Hovering the mouse over a group class may show a link to `/studios/2/group_classes/5`, but when you click the link something else occurs. 

When the page originally loaded, it loaded JavaScript in the asset pipeline. Within the pipeline there was a function that, on document ready, attached a listener to the click event for the mentioned link. When this event occurs, the function sets a url based on the event’s data attributes, performs an Ajax get request, and prevents the event’s default action of redirecting the page to the group class show page at `/studios/2/group_classes/5`.  The Ajax request returns a response in JSON format, which is then placed in a specified div within the DOM. That’s a lot of action without a page refresh!

Similar functionality allows the user to click “Next Group Class” and return the show page for the adjacent class at that studio without the page refresh. You can also go to a user’s show page and render a list of that user’s reviews. One level cooler – you can even add a new group class to a studio’s show page without causing a page refresh. Don’t believe me? Check out the action in your console or in your terminal’s server window.  

