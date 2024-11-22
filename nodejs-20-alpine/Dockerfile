# Build stage
FROM node:20-alpine AS build

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .

# Production stage
FROM node:20-alpine

WORKDIR /usr/src/app

COPY --from=build /usr/src/app /usr/src/app
RUN npm install --production

EXPOSE 3000
CMD ["node", "index.js"]
