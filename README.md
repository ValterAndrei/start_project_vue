### Starting a new Vue project using docker and docker-compose

1. Create files
```
touch Dockerfile docker-compose.yml .dockerignore
```

* Dockerfile
```dockerfile
# Yarn manager
FROM node:16-alpine3.12
RUN yarn global add @vue/cli
RUN mkdir /my_app
WORKDIR /my_app
COPY . /my_app
CMD [ "yarn", "serve" ]


# NPM manager
# FROM node:16-alpine3.12
# RUN npm install -g @vue/cli
# RUN mkdir /my_app
# WORKDIR /my_app
# COPY . /my_app
# CMD [ "npm", "rum", "serve" ]
```

* docker-compose.yml
```yml
version: '3.7'

services:
  app:
    image: vue_application
    container_name: vue_app_container
    ports:
      - '8080:8080'
    volumes:
      - ./:/my_app
    command: 'yarn serve'
    # command: 'npm run serve' # for NPM manager
```

* .dockerignore
```
node_modules
.git
.gitignore
```

2. Buid image from `Dockerfile`
```
docker build -t vue_application .
```

3. Access the container
```
docker-compose run --rm app sh

# or:
docker container run --rm -v $(pwd):/my_app -it vue_application sh
```

4. Create the project
```
vue create .
```

5. Changing file permission

```
sudo chown -R $USER:$USER .
```

6. Up server

```
docker-compose up app

# or:
docker container run --rm -v $(pwd):/my_app -it -p 8080:8080 vue_application
```

> `localhost:8080`


---


### If your project already exists:

1. Buid image from `Dockerfile`
```
docker build -t vue_application .
```

2. Up server

```
docker-compose up app

# or:
docker container run --rm -v $(pwd):/my_app -it -p 8080:8080 vue_application
```
