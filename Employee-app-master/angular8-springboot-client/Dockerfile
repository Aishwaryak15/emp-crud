# Build stage
FROM node:20.11.1 AS build

WORKDIR /app

# Copy package.json and package-lock.json separately to leverage Docker cache
COPY package*.json ./

RUN npm install -g @angular/cli@ 17.3.0
RUN npm install
# Copy the rest of the application
COPY . .

RUN ng build

# Serve stage
FROM nginx:alpine

# Copy built Angular app from the build stage to Nginx directory
COPY --from=build /app/dist/angular8-springboot-client /usr/share/nginx/html

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

