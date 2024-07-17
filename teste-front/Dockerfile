# Use an oficial Node.js base image
FROM node:14

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json files
COPY package*.json ./

# Install dependencies of the project
RUN npm install

# Copy all remaining application files
COPY . .

# Compile the aplication (if needed)
RUN npm run build

# Expose the port the application runs on
EXPOSE 3000

# Run the application
CMD ["npm", "run", "serve"]