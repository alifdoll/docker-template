FROM node:18

WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY . .

# Comment these if you dont use pnpm on your project
RUN npm install -g pnpm

# Install app dependencies
RUN npm install

# Copy the rest of the application files
COPY . .

# Expose the port your application runs on
EXPOSE 3002

# Start the application
CMD ["npm", "run", "start"]

