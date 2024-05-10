# Install Guide

install node manager

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash
```

install newer version

```sh
nvm install 18.0.0
nvm use 18.0.0
```

create new app

```sh
npx create-strapi-app@latest app --quickstart
```

cd to new diretory

```sh
cd app
```

ad Dockerfile

```sh
FROM node:18
# Installing libvips-dev for sharp Compatibility
RUN apt-get update && apt-get install libvips-dev -y
ARG NODE_ENV=development
ENV NODE_ENV=${NODE_ENV}
WORKDIR /opt/
COPY ./package.json ./package-lock.json ./
ENV PATH /opt/node_modules/.bin:$PATH
RUN npm install
WORKDIR /opt/app
COPY ./ .
RUN npm run build
EXPOSE 1337
CMD ["npm", "run", "develop"]
```

if the npm-lock file is missing run this in the app diretory

```sh
npm install --package-lock-only
```

add .dockerignore

```sh
.tmp/
.cache/
.git/
build/
node_modules/
data/   
```

build container

```sh
docker build -t mystarpi:latest .
```

run it:

```sh
docker run -d -p 1337:1337 mystrapi
```

or create a compose file

```yaml
version: '3'
services:
  strapi:
    image: mystrapi
    container_name: strapi
    ports:
      - 1337:1337
    networks:
      - podman
networks:
  podman:
    external: true
```

start it

```sh
podman-compose up -d
```
