# specify the node base image with your desired version node:<version>
FROM node:8
# author
MAINTAINER bikai_xidian@163.com

# RUN npm config rm proxy
# RUN npm config rm http-proxy
# RUN npm config rm https-proxy
# RUN npm config set no-proxy .huawei.com
# RUN npm config set registry http://w3cloudnkg-sit1.huawei.com/ccloud/nexus/content/groups/npm-all/

# override the default settings, overwrite at runtime：docker run -e NPM_CONFIG_LOGLEVEL=info node ...
ENV NPM_CONFIG_LOGLEVEL info

# Create app directory to place application, cd into the folder
WORKDIR /server/www/

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied where available (npm@5+)
# Only copy package.json file, aims to use docker layer cache
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm ci --only=production

# Bundle app source, filtered by .dockerignore
COPY . .

# same as your application's port, like a firewall
EXPOSE 3000

# run the application
CMD ["npm", "start"]

