### Starting a new Vue project using docker

1. Create files
```
touch Dockerfile .dockerignore
```

* Dockerfile
```dockerfile
# Yarn manager
FROM node:16-alpine3.12
RUN yarn global add @vue/cli
RUN mkdir /app
WORKDIR /app
COPY . /app
CMD [ "yarn", "serve" ]

# NPM manager
# FROM node:16-alpine3.12
# RUN npm install -g @vue/cli
# RUN mkdir /app
# WORKDIR /app
# COPY . /app
# CMD [ "npm", "rum", "serve" ]
```

* .dockerignore
```
node_modules
.git
.gitignore
```

2. Buid image from `Dockerfile`
```bash
docker build -t vue_application .
```

3. Access the container
```bash
docker container run --rm -v $(pwd):/app -it vue_application sh
```

4. Create the project
```bash
vue create .
```

5. Changing file permission

```bash
sudo chown -R $USER:$USER .
```

6. Up server

```bash
docker container run --rm -v $(pwd):/app -it -p 8080:8080 vue_application
```
> `localhost:8080`


---


### If your project already exists:

1. Buid image from `Dockerfile`
```bash
docker build -t vue_application .
```

2. Up server

```bash
docker container run --rm -v $(pwd):/app -it -p 8080:8080 vue_application
```

### Deploying at Heroku
- [Tutorial](https://cli.vuejs.org/guide/deployment.html#heroku)
