# Use an existing docker image as a base
# alpine means a small as possible
FROM node:alpine as builder

WORKDIR '/app'

# A wildcard is used to ensure both package.json AND package-lock.json are copied
# Copy package.json before other files to cache npm install step, because node_modules most of the time the same
COPY package*.json ./

# Download and install a dependency
# Every run create image with installed dependency from current container
RUN npm install

# Copy build files
COPY . .

RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./nginx/static/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build  /usr/share/nginx/html

# docker build -t akr/my-app .