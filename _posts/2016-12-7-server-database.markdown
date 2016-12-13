---
layout: post
title:  "Building The Forge: Connecting to the Server"
date:   2016-12-7 
categories: jekyll update
---

In review we have acomplised quite a bit up unitl this point. 

* we created our database 
* set up our html template 
* wrote a basic server.py 
* created a user to access our database from our server 

Now we are ready to write the code to access our server. If you recall our server currently looks like this: 

{% highlight python %} 

    import os
    from flask import Flask, render_template
    app = Flask(__name__)
    
    #render the home page
    @app.route('/')
    def mainIndex():

        return render_template('index.html')

    # render our add rosary page 
    @app.route('/add_rosary')
    def addosary(): 
    
        return render_template('add_rosary.html')

    # start the server
    if __name__ == '__main__':
        app.run(host=os.getenv('IP', '0.0.0.0'), port =int(os.getenv('PORT', 8080)), debug=True)

{% endhighlight %} 

we are going to connect to our database using psycopg2 adapter. In order to use this you must import the psychopg2 
    library and update the package. 

The steps to connect to the databse are as follows, and prepare to execute quires are as follows: 

1. connect with psycopg2.connect 
2. create a cursor object to interact with the database 

To acomplish step one we will create a function to connect to the database. the function is going to look something like this (recall that our database is called The_forge, our user is theMasterSmith, and our password is secret): 

{% highlight python %} 
    def connect_to_rosary(): 
        connectionString = 'dbname = The_forge user = theMasterSmith password = ***** host = localhost'
        print connectionString
        try: 
            return psycopg2.connect(connectionString)
        except: 
            print('nope')
{% endhighlight %} 

In the above function we create our connection string that we will feed to psycopg2.connect. The string tells 
    the server what database we are connecting to, what our user's name is, our password, as well as our host
    As stated above we then feed that string into the function to connect to the database, with an expcept
    statement that will print 'nope' if we screwed something up for debugging purposes. 

Now that our function is complete we can move on to step two. 

Step two takes place inside our functions that render our pages. Because both of are pages are accessing our data
    base we will run this code in both our functions:  

{% highlight python %} 
    con = connect_to_rosary() 
    cur = con.cursor 
{% endhighlight %} 

the first line of code runs the function we just wrote to connect to the database, and the second line of 
    code creates our cursor object. 

our server.py file now looks something like this: 
{% highlight python %} 

    import os
    import psycopg2.extras 

    from flask import Flask, render_template
    app = Flask(__name__)

    def connect_to_rosary(): 
        connectionString = 'dbname = The_forge user = theMasterSmith password = ***** host = localhost'
        print connectionString
        try: 
            return psycopg2.connect(connectionString)
        except: 
            print('nope')#render the home page

    # render the home page 
    @app.route('/')
    def mainIndex():
        con = connect_to_rosary() 
        cur = con.cursor         

        return render_template('index.html')

    # render our add rosary page 
    @app.route('/add_rosary')
    def addosary(): 
        con = connect_to_rosary() 
        cur = con.cursor         

        return render_template('add_rosary.html')

# start the server
if __name__ == '__main__':
app.run(host=os.getenv('IP', '0.0.0.0'), port =int(os.getenv('PORT', 8080)), debug=True)

{% endhighlight %} 

Now that we connected to our database, and created our cursor we have one final step complete the functionality of our web app. 
    That is to write our quires. 
    

