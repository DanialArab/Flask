# Flask

This repo documents my understanding of Flask. Here is the strcture of my notes:

1. [Introduction](#1)
2. [Building a simple Flask app on Linux](#2)
   1. [Setting up our environment and dependencies](#3)
   2. [Running the flask app](#4)
      1. [Running the flask app in the debug mode](#5)
      2. [Adding another route](#6)



<a name="1"></a>
## Introduction

Flask is a micro web framework specially designed for Python. The term ‘micro’ aims to indicate that the framework leverages Python's simplicity, extensibility, and readability to create a lightweight and flexible framework for building web applications. It aims to prevent imposing too much structure or unnecessary dependencies.

<a name="2"></a>
## Building a simple Flask app on Linux

In this section, a simple flask app will be built on ubuntu (an ubuntu distro can be installed on Windows Subsystem for Linux (WSL)).

<a name="3"></a>
### Setting up our environment and dependencies

As a best practice, we create a separate Conda environment for each project or application. This approach helps in managing dependencies and isolating the environment specific to a particular project. 

conda create --name flask
conda activate flask
pip install flask 

<a name="4"></a>
### Running the flask app 

    mkdir Flask_Blog
    cd Flask_Blog
    code .

In the project directory, I create a flaskblog.py:

    from flask import Flask 
    app = Flask(__name__)
    
    @app.route("/")
    def hello():
        return "<h1>Home page</h1>"

To run the flask app using an environment variable:

    export FLASK_APP=flaskblog.py
    flask run

Now our app is up and running on http://127.0.0.1:5000 where 127.0.0.1 is the IP address of our local machine and the port number is 5000. The alias for the IP address of the local machine is localhost meaning http://localhost:5000/ gets me the same result.  

<a name="5"></a>
#### Running the flask app in the debug mode

When we are making a website, most likely we make a lot of changes to our application and if each time we make a small changes we have to shut down and restart the web server to see the changes it would be not too handy. One way to get around this is to have the server show the changes without restarting our application just by running our application in the debug mode. One way to this is to by having another environment variable as follows:

    export FLASK_DEBUG=1
    flask run

Now we don’t need to restart the server to see the changes we make to the application. 

Rather than relying on the environment variables, we can also modify the flaskblog.py file as follows: 

    from flask import Flask 
    app = Flask(__name__)
    
    @app.route("/")
    def hello():
        return "<h1>Home page</h1>" 
    
    if __name__ == '__main__':
        app.run(debug=True)

now  instead of running flask run which uses the environment variable, I can call the script directly by Python:

    python3 flaskblog.py

<a name="6"></a>
### Adding another route

I modify my python script to have a route to the about page of the website:

    from flask import Flask 
    app = Flask(__name__)
    
    @app.route("/")
    def hello():
        return "<h1>Home page</h1>" 
    
    @app.route("/about")
    def about():
        return "<h1>About page</h1>" 
    
    if __name__ == '__main__':
        app.run(debug=True)


We can have multiple routes being handled by the same function, we just need to have another decorator. Like if we want to have the route of / and  /home to go to the home page:

    @app.route("/")
    @app.route("/home")
    def home():
        return "<h1>Home page</h1>"

not both http://127.0.0.1:5000/home and http://127.0.0.1:5000/ routes get me to the home page.


Reference: https://www.youtube.com/watch?v=MwZwr5Tvyxo&list=PL-osiE80TeTs4UjLw5MM6OjgkjFeUxCYH
