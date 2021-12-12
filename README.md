### Starting a new Vue project using docker-compose

1. Create files
```
touch Dockerfile docker-compose.yml
```

* Dockerfile
```dockerfile
FROM node:16-alpine3.12

RUN npm install -g @vue/cli

RUN mkdir /my_app

WORKDIR /my_app

COPY . /my_app

CMD [ "npm", "rum", "serve" ]
```

* docker-compose
```yml
version: '3.7'

services:
  app:
    image: vue_application
    ports:
      - '8080:8080'
    volumes:
      - ./:/my_app
    working_dir: /my_app
    command: 'npm run serve'

# docker run --name vue_app_container --rm -v $(pwd):/my_app -it -p 8080:8080 vue_application
```

2. Create image from `Dockerfile`
```
docker build -t vue_application .
```

3. Access the container
```
docker container run --rm -v $(pwd):/my_app -it vue_application sh
```

4. Create the project
```
vue create .
```

5. Ignoring files, `touch .dockerignore`
```
node_modules
.git
.gitignore
```

6. Changing file permission

```
$ sudo chown -R $USER:$USER .
```

7. Up server

```
$ docker-compose up app
```

> `localhost:8080`
