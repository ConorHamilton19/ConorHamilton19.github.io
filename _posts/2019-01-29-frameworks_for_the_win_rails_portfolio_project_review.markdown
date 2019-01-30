---
layout: post
title:      "Frameworks for the win! Rails Portfolio Project Review"
date:       2019-01-30 01:25:31 +0000
permalink:  frameworks_for_the_win_rails_portfolio_project_review
---


It is easy to see why Rails is such a great framework. The work put in to make this possible must be an immense amount. Moving on from Sinatra and designing something in Rails is a big step. Everything to somehow get much simpler but vastly more complicated at the same time. With things like action_helpers to resources it makes it super simple to get an application started but without a deeper knowledge how each of them work things get real fuzzy really quick, especially once you veer off the standard design rails sets out for an app. 

The place this project really got me working was in the use of a join table to store attributes. Man I am glad that is over, hopefully. ActiveRecord has_many, through works like a charm, allowing me to relate two models like a breeze. But the join table was a different story. During my project prep interview the lesson I learned is that the join table attribute should be something that has to do with the relationship between the two models. This helped me a lot. Also the thought that by knowing both of the id's of models the table was joining, then I could access that instance fairly easily. Trying to treat them like any other model was very hard for me to wrap my head around especially with a name like UserWines. 

There is not a lot of info about how to deal with attributes like this and a lot that I have found is that ActiveRecord likes join tables for its purposed but not so much for letting us play with them. After a lot of trial and error I have a small understanding of what it takes to deal with them but I think that there is a lot more to learn. 

Through all the struggles through this app, what came out the other end is something I am fairly proud of. It is simple but serves a purpose that would be very beneficial for Wine lovers everywhere. Intentionally I built it with the idea of being able to expand fairly easily. A few things I would like to add:

1) Only put wines in the database once and allow user to search for them or add new ones if they dont exist. Seems like the right way to accomplish having a list of wines but a little bit too much for completion of this project.
2) Add more authorization. Not wanting to add too many gems in before I knew how to use them I can see that there are a few places that authoriztion may help secure up the app.(hacking urls)
3) Comments on wines that have been drank. The reason for having a space to keep wines that have been opened would be so that you could write your thoughts on them and keep them in mind to buy again. 

Thanks for reading! Check out the app. https://github.com/ConorHamilton19/rails-wine-cellar-project
