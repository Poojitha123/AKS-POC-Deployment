# Use the official Node.js 16.15.0 image as a base for building
FROM node:16.15.0 as build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React app
RUN npm run build

# Use node http-server to serve the static files
FROM node:16.15.0

# Set the working directory
WORKDIR /app

# Copy the built React app from the build stage to the working directory
COPY --from=build /app/build ./build

# Expose port 80 to allow external access (if necessary)
EXPOSE 80

# Install http-server globally to serve the static files
RUN npm install -g http-server

# Command to start serving the React app
CMD ["http-server", "./build"]
