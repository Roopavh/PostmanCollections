# Use the official Node.js 26 image as the base image
FROM node:26

# Set the working directory in the container(linux)
WORKDIR /app


# Install Newman globally
RUN npm install -g newman

#Install Newman html report
RUN npm install -g newman-reporter-html

#Install Newman Reporter HTMLExtra
RUN npm install -g newman-reporter-htmlextra


# Copy your Postman collection and environment files to the working directory
COPY GorestDataDrivencollection.json .
COPY GoRestEnv.json .
COPY userdata.csv .

# Set the command to run Newman and execute your Postman collection
CMD ["newman", "run", "GorestDataDrivencollection.json", "-e", "GoRestEnv.json","-d","userdata.csv", "-r", "cli,json,html,htmlextra","--verbose"]
