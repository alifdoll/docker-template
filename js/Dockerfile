FROM node:latest

WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY . .

# Comment these if you dont use pnpm on your project
RUN npm install -g pnpm

# Install app dependencies (USE NPM OR PNPM!!!)
RUN pnpm install

# Copy the rest of the application files
COPY . .

# Expose the port your application runs on
EXPOSE 3002

# Adjust based on your projects needs, this is optional!!!
# Generate Prisma client 
RUN npx prisma generate

# Start the application
RUN pnpm run build

CMD ["pnpm", "run", "dev"]

