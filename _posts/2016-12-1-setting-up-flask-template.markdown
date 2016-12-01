---
layout: post
title:  "Building The Forge: Flask Template Part 1"
date:   2016-12-1
categories: jekyll update
---

In the last post we talked about how I set up my database for The Forge. 
	In this post we are going to discuss how I set up the flask template 
	using cloud9 as a host for the web app. 
	
I'm not going to go in depth about cloud9. The gist is that it is this developing
	environment in the could. It's really cool. You get a workspace, and you can 
	locally host a web app and it's really super useful. 
	
So to start a flask template, there is some basic setup. 

you go to your terminal and type in this :

{% highlight python %} 
sudo easy_install flask markdown
{% endhighlight python %}

Now flask is installed. We're going to come back to this. 

But first I am going to talk about how I set up my html template. 
	I cruised the web and found a free html template. There are a lot of them out there,
	there are free ones and then there are more fancy ones that you can buy. The free ones 
	are super easy to modify to fit your needs. 

So because I am creating a super simple web app, 
	One with two pages. A page to search my database, and a page to insert things into it. 
	I went with a really simple template, and modified it to make it.. well, simplier. 
	
Once I had the over all template the way I wanted it, it was time to begin to flaskify it. 

There are two folders to be aware of when flaskifying a template. The first is the static folder, 
	and the second is the template folder. 

We are not going to talk much about the static folder, but just be aware that in that folder you 
	putt all your css files and images and other things that remain static to your websight. 

The second folder is the template folder. This is where all the magic happens. 

So I followed these steps to set up the HTML side of my web app, all of these files were placed in 
	the template folder. 

* Take the original file that I modified and rename it layout.html 
	inside the file I find the part of the template that will change from page to page and I add this line of code that puts
	word "block content" with in brackets and percent signs and "end block" within brackets and percent signs.
* The next step I took was to make my search page, which also doubled as my home page. 
	I did this in a file called index.html, the html of the page was inbetween a "block content" and an "end block" for
	formated as described above, and looked like this: 
	
{% highlight html %}
    	<div id="column_w530">
        	
            <div class="header_02">Welcome to The Forge</div>
            <h3>to display all rosarys type "display all", otherwise you can search by name, or recipiant</h3>
            <label for="username">Search:</label>
            <input type="text" id="search" name="search" size="40" />
            <input type="submit" value="go" name="submit" />
            
        </div>
{% endhighlight html %}
    
Now what's cool, is that chunk of html is incerted right into the space in layout.html that we reserved with 
    our block content page. We will see how this is implimented further down in this post. 
    
Now what I created here is a basic search bar where I will be able to display all of the rosaries in my database
    or search by the name of the rosary or the recipiant. 

* The next page I made was my add rosary page. This is not doubling as my home page so I named this file add_rosary.html 
	following the same format as above I added this html code into the file. 
	
{% highlight html %}
    	<div id="column_w530">
        	
            
            <h3>to add a rosary to database</h3>
            <form method="POST" action="/ordercomplete">
            <table>
            <tr><td>Rosary Name:</td><td><input type='text' name='rosary_name'/></td></tr>
            <tr><td>Hail Mary:<td><input type='text' name='hail_mary_color'></td></tr>
            <tr><td>Our Father:</td><td><input type='text' name='our_father_color'></td></tr>
            <tr><td>Hope Bead:</td><td><input type='text' name='hope_color'></td></tr>
            <tr><td>Center Piece:</td><td><input type='text' name='center'></td></tr>
            <tr><td>Crucifix:</td><td><input type='text' name='crucifix'></td></tr>
            <tr><td>Color:</td><td><input type='text' name='color'></td></tr>
            <tr><td>Recipiant:</td><td><input type='text' name='recipiant'></td></tr>
            </table>
            <input type='submit' value='submit'/>
            
            
            
        </div>
    	
{% endhighlight html %}

This created a form page where I could input information about a new rosary to be added to the database. 

* back in the layout.html I added some html to provide a link to both of these pages that I just created in the menue bar.

Once my template as created the next step was to create a server.py file that will tie all of these pages 
	togeather and launch the web app using flask. 
	
We will go over how I made that file in the next update. 
				