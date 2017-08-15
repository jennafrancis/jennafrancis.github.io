---
layout: post
title:  "A Simple Static Webpage on Rails"
date:   2017-08-15 13:58:10 +0000
---


So you want to create a simple static site on Rails? Do it! If you’re comfortable using Ruby on Rails and aren’t too worried about memory storage, it can be a great, secure, testable platform to create a site.

I recently did this for my personal branding webpage, and would absolutely recommend it if you want to get something up and running rather quickly.

## Getting Started

If you know rails, you know the drill. Create a new app via the command line by running

``` $ rails new your_app```

If you’re planning on deploying to Heroku, make your life easier upon initialization by specifying PostgreSQL as your database.  The command for Rails 5 is

``` $ rails new your_app --database=postgresql ```

Look at that, you have a new app. Go ahead and create a static controller for your routes. If you use the `rails generate` command, Rails will go ahead and create files for tests and stylesheets as well.

``` $ rails g controller static ```

In terms of routes, f you’re looking for a one-page site, this is easily accomplished with one index route in your controller. Go ahead and set your root page in `config/routes.rb`. Mine looked like this

```Rails.application.routes.draw do
root 'static#index'
end ```

Lastly, create that `index.html.erb` file under your views in a directory called Static, i.e. `app/views/static/index.html.erb`.

## Pick a Theme

If you want a beautiful, dynamic design – and fast – try browsing through the templates at HTML5UP (https://html5up.net/). They’re fully responsive for any device, built on HTML5 and CSS3, customizable for personal and commercial use, and 100% free under the Creative Commons (https://creativecommons.org/licenses/by/3.0/).

For my project, I picked Big Picture (https://html5up.net/big-picture).  Simply press ‘Download’ and the fun begins! 

## Install Your Theme

Open the zip file and duplicate it. You’ll want the backup version if you make a mistake or just want to reference the original.

Move all Javascript, CSS, Fonts, and SASS into the corresponding directories in the asset pipeline.  Create a new directory for images and place only the ones you really want in there. Images are memory heavy, so be sparing when committing to Git. 

Move the static pages from the theme into your views directory, and rename the file extensions from `my_file.html` to `my_file.html.erb` so that you can use the ruby helpers. Two useful ways of doing this are through asset paths and image tags as shown below.

``` <%= asset_path(‘my_file.pdf’) %> ```

This will return the full url path for the file with the name you specify, whereas 

``` <%= image_tag(‘my_image.jpg’) %> ```

will return the image itself rather than the url. These helpers are also available for your CSS in any file with the extension `.scss` .  The only difference is in syntax, where the `_` becomes a `-` . 

``` <%= asset-path(‘my_file.pdf’) %> 
<%= image-tag(‘my_image.jpg’) %> ```

## Finishing Up

Given that the JS, SASS, and CSS has been loaded properly, your static pages should be up and running under your beautiful new theme! You may need to do some updating of file routes, for example `assets/js/main.js` referenced in `index.html.erb` is now `assets/javascripts/main.js` in your rails app. 

Now add your own unique content and deploy to your favorite web service, like Heroku or AWS. You made it! Check out next week’s blog for a walkthrough of hosting your app on Heroku.

