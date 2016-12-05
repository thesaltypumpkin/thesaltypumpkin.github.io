---
layout: post
title:  "Building The Forge: Flask Template Part 2"
date:   2016-12-5
categories: jekyll update
---

In our last post we talked about the html set up for our flask template. 
    Today we will talk about the server.py file that launches our website, 
    and ties everything togeather. 

Right now my server.py is pretty short. So get a good look at the code here: 


{% highlight python %} 
    import os
    from flask import Flask, render_template
    app = Flask(__name__)

    @app.route('/')
    def mainIndex():

        return render_template('index.html')

    @app.route('/add_rosary')
    def addrosary(): 

        return render_template('add_rosary.html')

        # start the server
    if __name__ == '__main__':
        app.run(host=os.getenv('IP', '0.0.0.0'), port =int(os.getenv('PORT', 8080)), debug=True)

{% endhighlight %}

Let's break this down a bit. This is a super basic server file. Right now I am just rendering the two HTML pages 
    that we discussed in part one. 


{% highlight python %} 
import os
from flask import Flask, render_template
{% endhighlight %} 

This is importing the necissary packages to make this file work. In terms of flask, rather than importing everything from the package we are just importing what we need. As we make this app more complex 
    we will be adding more things to the list. 

By importign the class 'Flask' we are importing the frame work for our app. Esentially, the app an instance of Flask. render_template is the funtion that we are using to render our HTML pages. 

Moving on, the route decorator is where, I think, all the magic happens. 

{% highlight python %} 
@app.route('/')
def mainIndex():

    return render_template('index.html')

{% endhighlight %} 

The route decorator tells the server what path will run what function. With the above example ('/') the server renders index.html when the user enters the root url. In other words, it's basically rendering the home page. 
    Likewise, with the add rosary page you'd need to attach '/add_rosary' onto the end of the url to tell the
    server to run the addrosary function and render 'add_rosary.html'

The final chunk of code: 

{% highlight python %} 
if __name__ == '__main__':
app.run(host=os.getenv('IP', '0.0.0.0'), port =int(os.getenv('PORT', 8080)), debug=True)
{% endhighlight %} 

actually runs the app. This is the line code that specifies the IP adress the port, and launches the app. 

So here we have a pything file that launches a two page webapp. Rendering the HTML pages that we went over in the last post. 

Right now the web app doesnt actually do anything. As you can see in the code above the functions that render the HTML pages are not actually doing anything other than rendering the templates. In the next post we will write python code that will begin to insert things into the database that we created back in our first post, when we first started this journey. 







