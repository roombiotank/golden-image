# Step 1: Build stage
FROM node:18-alpine AS builder

# Set the working directory in the container
WORKDIR /app

# Install build dependencies (for compiling native modules)
RUN apk add --no-cache python3 make g++

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install --frozen-lockfile

# Copy the rest of the application
COPY . .

# Build the Next.js app
RUN npm run build

# Step 2: Production stage
FROM node:18-alpine

# Set the working directory in the container
WORKDIR /app

# Install only runtime dependencies (you don't need build tools here)
RUN apk add --no-cache bash

# Copy the build artifacts from the builder stage
COPY --from=builder /app ./

# Expose the port Next.js runs on (default is 3000)
EXPOSE 3000

# Set environment variables for production
ENV NODE_ENV=production

# Start the Next.js app in production mode
CMD ["npm", "start"]
