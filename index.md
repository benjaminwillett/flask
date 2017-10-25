## Welcome to my Flask Pages

Flask is a microframework for Python based on Werkzeug, Jinja 2 and good intentions.

## Prerequisites
You will need Flask, gunicorn, a Heroku account and the HerokuCLI. 
Using pip, Python’s recommended tool for installing packages you can install them using:

`pip install flask gunicorn`

## Create App
In a new folder create a file called app.py and put the following code inside of it:

```
// ./app.py

from flask import Flask

app = Flask(__name__)

@app.route('/')
  def index(): 
   return 'Yo, it's working!'

if __name__ == "__main__":
  app.run()

```
We need to list the dependencies that are required for the Heroku environtment. To list them we can run `pip freeze` from a terminal window:

We need to put those dependencies in a file called `requirements.txt`. We can do that with one command:`pip freeze > requirements.txt`

The last thing that we need is a Procfile. In it’s simplest form you put one process per line that you want to be ran on your Heroku environment.

In our case we want to run our Flask application and we will use gunicorn to do this. Create a file named `Procfile` and put the following in it:`web: gunicorn app:app`

We can verify that our application works by running `python app.py` and then go to `127.0.0.1:5000` in the browser to see it in action:

Lastly, we need to create a new app in Heroku. Please see [Heroku page](https://benjaminwillett.github.io/heroku/) for details.
