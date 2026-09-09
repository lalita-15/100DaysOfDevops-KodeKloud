# Task 40: Dockerize Python Application and Deploy

## Task Requirements

Create a Dockerfile under /python_app

Use a Python base image

Install dependencies from /python_app/src/requirements.txt

Expose port 3000

Run server.py using CMD

Build image: nautilus/python-app

Create container: pythonapp_nautilus

Map host port 8099 to container port 3000

Test the application using curl

## Step 1: Login to App Server 2

ssh steve@stapp02

## Step 2: Go to the Application Directory

cd /python_app

## Check the files:

ls -R

Expected structure:

/python_app
├── Dockerfile
└── src
    ├── requirements.txt
    └── server.py

## Step 3: Create the Dockerfile

Add the following content:

FROM python

COPY src/ .

RUN pip install -r requirements.txt

EXPOSE 3000

CMD ["python", "server.py"]


## Step 4: Build the Docker Image

Build the image:

docker build -t nautilus/python-app .

## Verify the image:

docker images

## Step 5: Create and Run the Container

Run the container with the required name and port mapping:

docker run -d --name pythonapp_nautilus -p 8099:3000 nautilus/python-app

Port Mapping Format

-p HOST_PORT:CONTAINER_PORT

For this task:

Host Port      = 8099
Container Port = 3000


## Step 6: Verify the Container

Check running containers:

docker ps


## Step 7: Test the Application

Run:

curl http://localhost:8099

