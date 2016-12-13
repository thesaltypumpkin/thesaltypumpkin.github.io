---
layout: post
title:  "Building The Forge: Database"
date:   2016-11-30 
categories: jekyll update
---

The database for The Forge was created using postgresql. 
   If you would like to create your own database 
   you can follow these basic steps on how I created mine and adapt
   information as needed to fit your own needs. 

   
The first I needed to create the database it's self. I did that as follows:
  
{% highlight postgresql%}
CREATE DATABASE The_forge
{% endhighlight %}

Now I needed tables in my database. 
   For the first version of this webapp I decided to keep things
   pretty simple. 
   As the database gets more complex you will see follow up posts describing
   the changes I made. 

I started things with just one table. 
   This table will store all of my information for a rosary that I have made. 
   As time goes on and we develop The Forge we will begin to Normalize our tables. 
   Naturlly, once we begin the process of Normalization will will see more tables emerge. 

creating the table looked like this: 
{% highlight postgresql%} 
CREATE TABLE rosaries( 
   r_id serial primary key
   rosary_name varchar(30) NOT NULL, 
   our_father_bead varchar(30) NOT NULL, 
   hail_Mary_bead varchar(30) NOT NULL, 
   hope_bead varchar(30) NOT NULL, 
   center_piece varchar(30) NOT NULL, 
   crucifix varchar(30) NOT NULL, 
   color carchar(30) NOT NULL
   recipiant varchar(30) NOT NULL
 );
{% endhighlight %}

To give a little context for those columns in the chart: 
* rosary_name is the name given to the rosary, usually adapted from the saint prayed with. 
* our_father_bead, hail_mary_bead, and hope_bead are the colors for the three types of beads on the rosary.
* center_piece and crucifix are the type of centerpiece and crucifix that I used. 
* color is the color of the rosary findings (gold, silver, ect.). 
* recipient is who I gave the rosary to. 
   
Once the table was created I could start adding things to it. 
A basic insert statement looked like this: 
{% highlight postgresql %}
INSERT into rosaries (rosary_name, our_father_bead, hail_mary_bead, hope_bead, center_piece, crucifix, color, recipiant)
   VALUES (Albert, blue, redswirl, red, miraculous medal, standard crucifix, silver, maddie)
{% endhighlight %}

You will see the types of quires that I used to acsess the table 
   when I talk about how I set up the actual web-app using flask, so stay tuned for that. 
   



   


