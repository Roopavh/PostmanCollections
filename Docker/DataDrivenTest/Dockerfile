# Use the official Node.js image
FROM node:26

# Working directory
WORKDIR /app

# Install Newman and reporters
RUN npm install -g newman newman-reporter-html newman-reporter-htmlextra

# Create results folder
RUN mkdir -p /app/results

# Copy files
COPY DataDrivenAPICollection.json .
COPY GoRestEnv.json .
COPY userdata.csv .

# Execute Newman
CMD sh -c '
mkdir -p /app/results

TIMESTAMP=$(date +%Y%m%d%H%M%S)

newman run /app/DataDrivenAPICollection.json \
-e /app/GoRestEnv.json \
-d /app/userdata.csv \
-r cli,json,html,htmlextra \
--reporter-htmlextra-export /app/results/gorest-$TIMESTAMP.html \
--disable-unicode \
--verbose

echo "====== Generated Reports ======"
ls -l /app/results

LATEST=$(find /app/results -name "gorest-*.html" | head -n 1)

if [ -n "$LATEST" ]; then
    cp "$LATEST" /app/results/NewmanReport.html
    echo "Latest report copied to NewmanReport.html"
else
    echo "No report found!"
fi
'