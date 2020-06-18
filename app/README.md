# App & MySQL

## Getting Started

Start: docker-compose up -d
Stop: docker-compose down

Use DB
`docker exec -it bef3f9435a98 mysql -p todos`
    msql> 

### Logs

app: `docker-compose logs -f app`

mysql: `docker-compose logs -f mysql`

## Multi-Stage builds

#### React Example

**When building React applications, we need a Node environment to compile the JS code (typically JSX), SASS stylesheets, and more into static HTML, JS, and CSS. If we aren't doing server-side rendering, we don't even need a Node environment for our production build. Why not ship the static resources in a static nginx container?**

Copied to clipboard
FROM node:12 AS build
WORKDIR /app
COPY package* yarn.lock ./
RUN yarn install
COPY public ./public
COPY src ./src
RUN yarn run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
Here, we are using a node:12 image to perform the build (maximizing layer caching) and then copying the output into an nginx container. Cool, huh?