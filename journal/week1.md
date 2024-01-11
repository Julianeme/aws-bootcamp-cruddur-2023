# Week 1 — App Containerization

### Container creation:

```FROM python:3.10-slim-buster

# Inside Container
# make a new folder inside container
WORKDIR /backend-flask
# WORKDIR is used to let the container know where are we going to start working
# when it starts, is kind for typing CD /destination-folder and run the app from it
# its kind of the home directory.

# Outside Container -> Inside Container
# this contains the libraries want to install to run the app
COPY requirements.txt requirements.txt

# Inside Container
# Install the python libraries used for the app
RUN pip3 install -r requirements.txt

# Outside Container -> Inside Container
# . means everything in the current directory 
# first period . - /backend-flask (outside container)
# second period . /backend-flask (inside container)
COPY . .

# Set Enviroment Variables (Env Vars)
# Inside Container and wil remain set when the container is running
ENV FLASK_ENV=development

EXPOSE ${PORT}

# CMD (Command)
# python3 -m flask run --host=0.0.0.0 --port=4567
# -m flask: run the flask module
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]```


### To start the server it is necessary to export the ENV variables:

Run Python
```cd backend-flask
export FRONTEND_URL="*"
export BACKEND_URL="*"
python3 -m flask run --host=0.0.0.0 --port=4567
cd ..```

make sure to unlock the port on the port tab
open the link for 4567 in your browser
append to the url to /api/activities/home
you should get back json