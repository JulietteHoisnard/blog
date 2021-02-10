---
layout: post
title: "How to build a Ruby-On-Rails and React app from scratch"
subtitle: ""
date: 2021-02-09 15:26:56 +0100
related_image: https://images.unsplash.com/photo-1589652717406-1c69efaf1ff8?ixid=MXwxMjA3fDB8MHxzZWFyY2h8Mzl8fGNhdCUyMGNvbXB1dGVyfGVufDB8fDB8&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
tags: [coding]
---

1. Create a repo in Github
1. Install last version of ruby:

   ```shell
   rbenv install 3.0.0
   rbenv global 3.0.0
   ```

1. Install last version of node.js:
   nvm is equivalent to rbenv: allow to manage several versions of node.js on the same computer. Versions are set on a per-project basis.

   ```shell
   nvm install node
   nvm alias default node
   nvm use
   node --version
   ```

1. Install [rails](https://guides.rubyonrails.org/getting_started.html)

   ```shell
   gem install rails
   ```

1. Bootstrap a new app.

   ```shell
   rails new my-app \
    --database=postgresql \
    --api \
   ```

1. Set the NodeJS version in our new app.

   ```shell
   cd my-app
   echo "15.8.0" > .nvmrc
   ```

1. Let's check the used ruby version.

   ```shell
   cat .ruby-version
   ```

1. Push to Github

   ```shell
   git remote add origin git@github.com:<USER>/<REPO>.git
   git commit -m "first commit"
   ```

1. Test run the app

   ```shell
   bundle exec rails s
   ```

1. I want to use PostgreSQL and avoid manually installing the database by using Docker-Compose.
   Create and configure Docker:

   ```yml
   version: "3.7"
   services:
     database:
       image: "postgres" # use latest official postgres version
       ports:
         - "127.0.0.1:5432:5432"
       environment:
         POSTGRES_USER: ${USER}
         POSTGRES_HOST_AUTH_METHOD: "trust"
       volumes:
         - ${PWD}/db:${PWD}/db # persist data even if container shuts downvolumes:
       healthcheck:
         test: ["CMD", "pg_isready", "-U", "${USER}"]
       container_name: quiz_postgres
   ```

1. Install postgresql and disable it.

   ```shell
   sudo apt install postgresql
   sudo systemctl disable postgresql
   sudo systemctl stop postgresql
   ```

1. Launch docker and connect to the DB:

   ```shell
   docker-compose up -d
   psql -h 127.0.0.1 -U <USER> # Connect to the DB directly
   docker-compose run database bash # Or connect inside the docker container...
   psql -h database -U <USER> # ...and then to the DB
   ```

1. Next time you want to start or stop docker, don't do `up` but instead do:

   ```shell
   docker-compose stop
   docker-compose start
   ```

1. Edit database.yml:

```yml
default: &default
  adapter: postgresql
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

development:
  <<: *default
  url: <%= "postgres://#{ENV['USER']}:@localhost:5432/quiz-development" %>

test:
  <<: *default
  url: <%= "postgres://#{ENV['USER']}:@localhost:5432/quiz-test" %>
```

1. Start rails and create a db:

   ```shell
   bundle exec rails db:create
   bundle exec rails db:migrate
   bundle exec rails s
   ```
