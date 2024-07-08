# Use an official Node.js runtime as a parent image
FROM node:16-alpine as build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the application
RUN npm run build

# Verify that the dist directory exists
RUN ls -la /app/dist

# Use a lightweight web server to serve the static files
FROM nginx:alpine

# Copy the build output to the nginx html folder
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Command to run the nginx server
CMD ["nginx", "-g", "daemon off;"]
