# Step 1: Build the React app using Node.js
FROM node:22-alpine AS build

# Set the working directory
WORKDIR /app

# Copy the package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application
COPY . .

# Build the React app for production
RUN npm run build

# Step 2: Use NGINX to serve the built React app
FROM nginx:alpine

# Copy the build output from the previous stage to the NGINX container
COPY --from=build /app/build /usr/share/nginx/html

# Expose the port NGINX will listen on
EXPOSE 3000

# Start NGINX (default config will work for static files)
CMD ["nginx", "-g", "daemon off;"]
