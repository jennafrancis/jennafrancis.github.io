---
layout: post
title:  "Have you jumped out of a perfectly good airplane lately? Post it!"
date:   2017-04-07 19:34:12 +0000
---


I recently took my second skydiving adventure, and I must admit- I’m addicted! There’s nothing better than the rush of adrenaline as you fall from 13,000 feet with a man strapped to your back trying to get you to look at the camera for a photo op. Well okay, maybe not that last part. But hey, you have to start somewhere before you can jump solo. Before I get licensed to jump out of a plane on my own, I should probably finish this Sinatra portfolio project. And so we go...

My chosen domain is called Skydive Squadspace. Users can see what others in the skydiving community are up to, check out new locations they may want to go, and log jumps that they’ve made. 

When a user creates their profile, they must give an email, username, and password (which gets secured thanks to the `bcrypt gem`). They also have the option of adding their name and a short bio, but these are not required. 

When the user logs in, they are brought to the Squadspace page, where all members of the community’s jumps are posted with a quick comment and location. From here, the user may click on a username or location to learn more. 

If they click on the username, they are brought to that user’s page, displaying their name, username, bio, and a list of their jumps.  Each jump has a type and a height and belongs to a user and a location.  For example, a jump may be listed as “BASE jump from 828 meters at Skydive Dubai” with the comment “Loved the DreamJump system off The Burj Khalifa!” If that sounds crazy to you, know that it was done, and there is proof [here]( https://www.youtube.com/watch?v=Fhskvloj1gE).

If the current user clicks on a location from the Squadspace page, they are brought to the location’s page. Here, you see the name and address of the location along with a list of jumps that have been made there by previous visitors, displayed with similar format to what was described above. 

To add a new jump, the user simply clicks the `Add a Jump` button found in the header and is brought to a form for a new jump. The jump must have a type, height, and location. Comments are not required, but sure are fun. For a location, the user has the option to click a radio button to select a previously made location or to create a new location. When the jump is successfully created, the user is redirected to their own user page with a flash message at the top confirming the post was successful. 

When looking at a user’s profile, you see links to edit or delete jumps. If you are looking at your own profile, these links take you to the jump’s show page and allow you to update or destroy the selected jump. If you are on any other user’s profile, the link reloads the profile with a flash message stating that you do not have permission to edit or delete this user’s jumps.

Finally, the user has the option to view a list of all locations and their addresses via the `Locations` link at the top of the page. This may be useful if you’re looking to find new places to jump and check out what others did there.

Moving forward, this could become a much more dynamic app where users could connect with other users in the community and create “friend” type relations. Besides the current list of what all people in the community are up to, there may be a second list where you only see where and how your friends have been jumping. With such a small community of people who skydive often around the world, it could be great to get in touch with new people and make the jump together. ;)




