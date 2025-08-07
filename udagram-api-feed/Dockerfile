FROM node:18-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

# Pre-compile TypeScript during build (without zip)
RUN npm run clean && npm run tsc && cp -rf src/config www/config && cp .npmrc www/.npmrc && cp package.json www/package.json

EXPOSE 8080

# Run the compiled JavaScript instead of compiling at runtime
CMD ["node", "./www/server.js"]