### Building stage ###

# base image
FROM node:12.3.1-alpine as builder

# set working dir
WORKDIR /app

# optional
#ARG APP_ENV
#ENV PATH /app/node_modules/.bin:$PATH

# install all dependencies
COPY package.json /app/package.json
RUN npm install

# add application
COPY . /app

# build
RUN npm run ng build --prod --output-path=/app/dist


### Setup ###

# base image
FROM nginx:1.15.12-alpine as setup

# optional
#COPY ./nginx.conf /etc/nginx/conf.d/
#RUN rm -rf /usr/share/nginx/html/*

# copy built application
COPY --from=builder /app/dist/AngularApp /usr/share/nginx/html

# expose port
EXPOSE 80

# run nginx
CMD ["nginx", "-g", "daemon off;"]