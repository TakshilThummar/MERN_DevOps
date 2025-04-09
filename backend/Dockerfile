# Step 1: Use official Node.js 22 LTS image to build the app
FROM node:22-alpine AS build

# Set the working directory
WORKDIR /app

# Copy the package.json and package-lock.json to install dependencies first
COPY package*.json ./

# Install dependencies
RUN npm install

# Step 2: Copy the application code
COPY . .

# Step 3: Install PM2 globally
RUN npm install pm2 -g

# Step 4: Install NGINX
RUN apk add --no-cache nginx

# Step 5: Expose ports for both Node.js and NGINX
EXPOSE 8000

# Step 6: Configure NGINX
COPY nginx.conf /etc/nginx/nginx.conf

# Step 7: Run both Node.js (with PM2) and NGINX using a script
CMD /bin/sh -c "pm2 start index.js --no-daemon && nginx -g 'daemon off;'"
