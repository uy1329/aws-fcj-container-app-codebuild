# This is some different here . We are using a different node image
# Beacuse if use node:20.18.0-alpine3.20 image you will get message like this
# 429 Too Many Requests - Server message: toomanyrequests: You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limit
# Stage 1: Build the React app
FROM public.ecr.aws/docker/library/node:20.18.0-slim as build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
COPY ./default.conf /etc/nginx/conf.d/default.conf