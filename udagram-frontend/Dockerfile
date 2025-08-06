FROM node:18-alpine AS ionic

WORKDIR /usr/src/app

# Install Ionic CLI globally
RUN npm install -g @ionic/cli

COPY package*.json ./

RUN npm install

COPY . .

RUN ionic build --prod

FROM nginx:alpine

# Copy the built app from the ionic stage
COPY --from=ionic /usr/src/app/www /usr/share/nginx/html

# # Copy nginx configuration if you have one
# # COPY nginx.conf /etc/nginx/nginx.conf

# EXPOSE 80

# CMD ["nginx", "-g", "daemon off;"]