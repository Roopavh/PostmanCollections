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
COPY "GoRest_APIWorkflow.postman_collection.json" .
COPY GoRestEnv.json .

# Set the command to run Newman and execute your Postman collection
CMD ["newman", "run", "GoRest_APIWorkflow.postman_collection.json", "-e", "GoRestEnv.json", "-r", "cli,json,html,htmlextra"]
