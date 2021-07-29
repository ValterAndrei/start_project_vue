### Starting a new Vue project using docker-compose

1. Create _docker-compose.yml_ file

```
$ touch docker-compose.yml
```

```yml
version: '3.7'

services:
  app:
    image: node
    ports:
      - '8080:8080'
    volumes:
      - ./:/srv/app
    working_dir: /srv/app
    command: 'npm run serve'
```

2. Access the container
```
$ docker-compose run --rm app bash
```

3. Install _vue/cli_ and create the project

```
$ npm install -g @vue/cli

$ vue create .
```

4. Changing file permission

```
$ sudo chown -R $USER:$USER .
```

5. Up server

```
$ docker-compose up web
```

> `localhost:8080`
