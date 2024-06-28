# JSON Server Docker Setup

This repository contains a Dockerfile to set up a JSON Server using Docker. JSON Server is a full fake REST API that you can use to create a quick backend for prototyping and mocking.

## Dockerfile Explanation

Below is the Dockerfile with comments explaining each step:

```dockerfile
# Use the latest Node.js image from Docker Hub as the base image
FROM node:latest

# Set the working directory inside the container to /home/server
WORKDIR /home/server

# Install JSON Server globally using npm
RUN npm install -g json-server

# Copy the db.json file from the host to the container's working directory
COPY db.json /home/server/db.json

# Copy the alt.json file from the host to the container's working directory
COPY alt.json /home/server/alt.json

# Expose port 3000 to make the JSON Server accessible from outside the container
EXPOSE 3000

# Set the entry point to start the JSON Server with the --host 0.0.0.0 option
# This makes the server accessible from all network interfaces inside the container
ENTRYPOINT [ "json-server", "--host", "0.0.0.0" ]

# Set the default command to serve the db.json file
# This can be overridden to serve alt.json or any other JSON file when running the container
CMD [ "db.json" ]

## Running Commands

#building
docker build -t sample-docker .

#running
docker run -d -p 4000:3000 sample-docker
