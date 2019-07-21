FROM node:alpine as builder
# this image/container is used to build the react app and output what is built
# so it can be picked up and copied into the nginx image/container that is built below starting with the next FROM
WORKDIR '/app'

COPY ./package.json ./
RUN npm install

COPY . .

# creates a build folder in /app/ direcctory 
RUN npm run build

# to end one phase and start another, you can just type FROM again.

FROM nginx
# second build in this Dockerfile.  
# this takes the build files from above and copies them to this new nginx server to serv up the files

# This is NOT used on local workstaton testing and has no affect
# This IS used in prod deployments and in AWS Deployments
# the routing nginx server will sned trafic to this server on
EXPOSE 3000  

# The default.conf file changes ntinx to liston also on port 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# copy the build files from the top instance
COPY --from=builder /app/build /usr/share/nginx/html 

# default behavior of nginx container is to start nginx automaticly
