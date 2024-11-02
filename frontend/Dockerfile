# Use an official Node runtime as a parent image
FROM node:18

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY /portfolio-app/package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of your application code
COPY /portfolio-app .

# Build the SvelteKit application
RUN npm run build

# Expose the port that the app will run on
EXPOSE 3000

# Start the application
CMD ["node", "build"]
