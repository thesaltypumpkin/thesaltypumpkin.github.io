---
layout: post
title:  "Building The Forge: Creating a User"
date:   2016-12-6
categories: jekyll update
---

Now that we have set up the bassis for are server.py and are html templates we are ready to start 
    writing the code that will accsess our database. 

Almost. 

Before we connect to our database we must first create a user by the principle of least privilage. 
    Basically what we are doing is creating a user to acsess our database with the lowest privlages needed. 
    This is because if we log in with our root acount, not only is it a security hazard, but if we write 
    some sort of bad code we could unintentionally wipe out our entire database. 

So for the purposes of this app we need our user to do two things. 
 
* log on to our database 
* access the database when we search for rosaries. 
* add new rosaries to the database. 

In order ot do this we are going to grant our user two priviliages. 

* login 
* select 
* insert 

Login is pretty self explanitory. It will let us login. The select privlage will allow our user to read the database and select items from it to display in our webapp.
    While the insert privlage will allow are user to add new items to our database. 

Now that we understand what are user will do we can create it. 

Open up postgress with your root account and execute the following command to create the user (For our purposes we will name 
our roll theMasterSmith):

{% highlight postgresql %} 
    create roll theMasterSmith
{% endhighlight %} 

Now that our roll is created we must grant it login privlages with this command: 

{% highlight postgresql %} 
    alter roll theMasterSmith with login 
{% endhighlight %}

we will then be asked ot enter our password. For securit reasons I will keep the password secrert. 
    Take not of "alter roll" we use this command to alter any roll to give it a log in privlage. 

The next step is to grant our user select and insert privlage. For this we will use the grant command: 

{% highlight postgresql %} 
    grant select on rosaries to theMasterSmith 
    grant insert on rosaroes to theMasterSmith
{% endhighlight %}

Our user can now login to our database, select items, and insert them. Now we are finally 
    ready to write some code in server.py that will allow our webapp to work with our databases. 






