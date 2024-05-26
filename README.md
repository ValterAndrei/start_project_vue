### Starting a new Vue project using docker-compose

1. Create files
```
touch Dockerfile docker-compose.yml .dockerignore
```

* Dockerfile
```dockerfile
FROM node:20-alpine3.19
RUN npm install -g @vue/cli
RUN mkdir /app
WORKDIR /app
COPY . /app
RUN yarn install
EXPOSE 8080
CMD ['yarn', 'serve']
```

* docker-compose.yml
```yml
services:
  app:
    build: .
    container_name: vue_app_container
    ports:
      - '8080:8080'
    volumes:
      - ./:/app
    command: yarn serve
```

* .dockerignore
```
node_modules
.git
.gitignore
```

2. Access the container
```bash
docker-compose run --rm app sh
```

3. Create the project
```bash
vue create .
```

4. Changing file permission

```bash
sudo chown -R $USER:$USER .
```

5. Up server

```bash
docker-compose up app
```
> `localhost:8080`


---


### If your project already exists:

1. Buid image from `Dockerfile`
```bash
docker-compose build
```

2. Up server

```bash
docker-compose up app
```

---

### Only Docker example
- [Tutorial](/only_docker.md)

### Deploying at Heroku
- [Tutorial](https://cli.vuejs.org/guide/deployment.html#heroku)
