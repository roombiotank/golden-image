# Step 1: Build Stage
FROM node:18-alpine AS builder

# Set the working directory
WORKDIR /app

# Install dependencies (for building Nuxt.js app)
RUN apk add --no-cache python3 make g++

# Copy package.json and package-lock.json first to leverage Docker caching
COPY package*.json ./

# Install app dependencies
RUN npm install --frozen-lockfile

# Copy the rest of the Nuxt.js app source code
COPY . .

# Build the Nuxt.js app
RUN npm run build

# Step 2: Production Stage (for SSR)
FROM node:18-alpine

# Set the working directory
WORKDIR /app

# Install runtime dependencies (only needed for SSR)
RUN apk add --no-cache bash

# Copy the build artifacts from the builder stage
COPY --from=builder /app ./

# Expose the default Nuxt.js SSR port (3000)
EXPOSE 3000

# Set environment variable to production
ENV NODE_ENV=production

# Start the Nuxt.js server
CMD ["npm", "start"]
