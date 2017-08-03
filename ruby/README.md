# Ruby with dependences on Alpine 2.4.1

This will build the base image needed to run any rails app that uses

* Postgres Database
* Ruby 2.4.1
* NodeJS

## How to Use

### Create Dockerfile

Create a `Dockerfile` with the following content

**Development version**

```
FROM pixalar/ruby:latest

ENV BUILD_DEPS \
  build-base \
  libxml2-dev \
  libxslt-dev \
  postgresql-dev \
  git

RUN apk --no-cache add $BUILD_DEPS

ADD . /usr/src/app
```

**Production version**

```
FROM pixalar/ruby:latest

RUN apk --no-cache add --virtual .build-dependencies \
  build-base \
  libxml2-dev \
  libxslt-dev \
  postgresql-dev \
  git

RUN bundle install --system --jobs=4 --no-cache --without development test --clean \
&& apk del .build-dependencies

ADD . /usr/src/app
```

### Build the docker image

Once you've added the docker file you can build the base image of your app using
