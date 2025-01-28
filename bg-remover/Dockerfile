# Stage 1: Build
FROM node:18 AS build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the application
RUN npm run build

# Stage 2: Serve
FROM nginx:alpine

# Copy custom Nginx configuration file
COPY nginx.conf /etc/nginx/nginx.conf

# Copy the build output to Nginx's html directory
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 83
EXPOSE 83

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]
