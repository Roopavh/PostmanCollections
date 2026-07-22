# Use the official Node.js image
FROM node:26

# Working directory
WORKDIR /app

# Install Newman and reporters
RUN npm install -g newman newman-reporter-html newman-reporter-htmlextra newman-reporter-junitfull

# Copy files
COPY DataDrivenAPICollection.json .
COPY GoRestEnv.json .
COPY userdata.csv .

# Execute Newman
CMD ["sh", "-c", "\
TIMESTAMP=$(date +%Y%m%d%H%M%S); \
mkdir -p /app/results; \
newman run /app/DataDrivenAPICollection.json \
-e /app/GoRestEnv.json \
-d /app/userdata.csv \
-r cli,htmlextra \
--reporter-htmlextra-export /app/results/gorest-$TIMESTAMP.html \
--disable-unicode \
--verbose; \
LATEST=$(ls -t /app/results/gorest-*.html | head -n 1); \
if [ -n \"$LATEST\" ]; then cp \"$LATEST\" /app/results/NewmanReport.html; fi"]