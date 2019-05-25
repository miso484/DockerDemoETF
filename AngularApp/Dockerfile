### Building stage ###

# base image
FROM node:12.2.0-alpine as builder

# set working dir
WORKDIR /app

#ARG APP_ENV

# install all dependencies
COPY package.json package-lock.json ./
RUN npm ci

# add application
COPY . ./app

# build
#RUN npm run ng build -- --prod --output-path=dist
RUN ./node_modules/.bin/ng build --prod --output-path=dist

### Setup ###

# base image
FROM nginx:1.15.12-alpine

#COPY ./nginx.conf /etc/nginx/conf.d/
#RUN rm -rf /usr/share/nginx/html/*

# copy built application
COPY --from=builder /dist /usr/share/nginx/html

CMD ["nginx", "-g", "daemon off;"]