# Use Node.js 14 as required
FROM node:14

WORKDIR /app

# Copy package.json and package-lock.json before running npm install
COPY package*.json ./

# Clear npm cache and install dependencies
RUN npm cache clean --force && npm install

# Copy the rest of the application code
COPY . .

# Expose the port
EXPOSE 8080

# Start the application
CMD ["npm", "run", "dev"]