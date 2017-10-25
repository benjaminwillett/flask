## Welcome to my Flask Pages

Flask is a microframework for Python based on Werkzeug, Jinja 2 and good intentions.

## Prerequisites
You will need Flask, gunicorn, a Heroku account and the HerokuCLI. 
Using pip, Python’s recommended tool for installing packages you can install them using:

`pip install flask gunicorn`

## Create App
In a new folder create a file called app.py and put the following code inside of it:

`// ./app.py

from flask import Flask

app = Flask(__name__)

@app.route('/')
  def index(): 
   return 'Yo, it's working!'

if __name__ == "__main__":
  app.run()`
