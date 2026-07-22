# Use the official Node.js 20 image as the base image
FROM node:20

# Set the working directory in the container
WORKDIR /app

# Install Newman and required reporters
RUN npm install -g newman newman-reporter-html newman-reporter-htmlextra

# Ensure the results directory exists
RUN mkdir -p /app/results

# Copy your Postman collection, environment, and data files
COPY DataDrivenAPICollection.json .
COPY GoRestEnv.json .
COPY userdata.csv .

# Set the command to run Newman with data-driven testing

# Execute Newman
CMD sh -c '\
TIMESTAMP=$(date +%Y%m%d%H%M%S); \
newman run DataDrivenAPICollection.json \
-e GoRestEnv.json \
-d userdata.csv \
-r cli,json,html,htmlextra,junitfull \
--reporter-htmlextra-export /app/results/gorest-$TIMESTAMP.html \
LATEST=$(ls -t /app/results/gorest-*.html | head -n 1); \
cp "$LATEST" /app/results/NewmanReport.html'