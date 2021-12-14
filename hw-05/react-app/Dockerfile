# Build
FROM node:16.13.1-alpine3.14 as build-stage

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

RUN npm run build

# Production
FROM nginx:1.21.4-alpine

COPY --from=build-stage /app/build /usr/share/nginx/html
EXPOSE 80

ENTRYPOINT [ "nginx","-g", "daemon off;" ]