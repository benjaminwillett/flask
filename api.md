### flask app that serves this data as a REST API.

Create a new app

```
$ virtualenv rest-api
$ source rest-api/bin/activate
$ mkdir ~/rest-app
$ cd ~/rest-app
```

Now we are in the main folder of app.Create a file called app.py in that folder.We need few libraries to finish our task.Install them by typing below commands.

```
$ pip install flask
$ pip install flask-restful
$ pip install sqlalchemy
```

That’s it. We are ready to build a cool salary API that can even be accessed through mobile. Let us recall the REST API design .It has 4 options. GET,PUT,POST,DELETE here we are  dealing with an open data which can be accessed by multiple applications. So we implement GET here and remaining REST options becomes quite obvious. 

```
from flask import Flask, request
from flask_restful import Resource, Api
from sqlalchemy import create_engine
from json import dumps
```

#Create a engine for connecting to SQLite3.
#Assuming salaries.db is in your app root folder

```
e = create_engine('sqlite:///salaries.db')

app = Flask(__name__)
api = Api(app)

class Departments_Meta(Resource):
    def get(self):
        #Connect to databse
        conn = e.connect()
        #Perform query and return JSON data
        query = conn.execute("select distinct DEPARTMENT from salaries")
        return {'departments': [i[0] for i in query.cursor.fetchall()]}

class Departmental_Salary(Resource):
    def get(self, department_name):
        conn = e.connect()
        query = conn.execute("select * from salaries where Department='%s'"%department_name.upper())
        #Query the result and get cursor.Dumping that data to a JSON is looked by extension
        result = {'data': [dict(zip(tuple (query.keys()) ,i)) for i in query.cursor]}
        return result
        #We can have PUT,DELETE,POST here. But in our API GET implementation is sufficient
 
api.add_resource(Departmental_Salary, '/dept/<string:department_name>')
api.add_resource(Departments_Meta, '/departments')

if __name__ == '__main__':
     app.run()
```

Your salary API is up and running now on localhost , port 5000. There are two rules we defined in the API. One is to get details of all departments available and second is to get employee full detail, who is working in a particular department.So now go tohttp://localhost:5000/departments


See how flask is serving database data into JSON through the REST API we defined. Next modify URL to peek all employees who are working in Police department.http://localhost:5000/dept/police

code walk-through is as follows
*  Used SQLAlchemy to connect to database and do select operations.
*  Created Flask-Restful classes to map functions with API URL
*  Returned the queried data as JSON ,which can be used universally.

See how simple it is to create a data API. We can also add support to PUT,POST and DELETE on data too.We can also have an authentication system for fetching data through API.
