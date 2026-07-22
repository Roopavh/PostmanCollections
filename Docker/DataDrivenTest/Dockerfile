# Use the official Node.js 20 image as the base image
FROM node:20

# Set the working directory in the container
WORKDIR /app

# Install Newman and required reporters
RUN npm install -g newman newman-reporter-html newman-reporter-htmlextra

# Ensure the results directory exists
RUN mkdir -p /app/results

# Copy your Postman collection, environment, and data files
COPY DataDrivenAPICollection.json /app/
COPY GoRestEnv.json /app/
COPY userdata.csv /app

# Set the command to run Newman with data-driven testing
CMD sh -c 'mkdir -p /app/results && \
newman run /app/DataDrivenAPICollection.json \
-e /app/GoRestEnv.json \
-d /app/userdata.csv \
-r cli,json,html,htmlextra \
--reporter-htmlextra-export /app/results/gorest-$(date +%Y%m%d%H%M%S).html && \
LATEST=$(ls -t /app/results/gorest-*.html | head -n 1) && \
cp "$LATEST" /app/results/NewmanReport.html'
