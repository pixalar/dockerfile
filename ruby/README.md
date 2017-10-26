# Ruby 2.4.2 with dependences on Alpine 3.6

This will build the base image needed to run any rails app that uses

* Postgres Database
* Ruby 2.4.2
* NodeJS
* Imagemagic

## How to Use

### Create Dockerfile

Create a `Dockerfile` with the following content

**Development version**

```
FROM pixalar/ruby:latest

RUN apk --no-cache add \
  build-base \
  libxml2-dev \
  libxslt-dev \
  postgresql-dev \
  git

WORKDIR /usr/src/app

VOLUME /usr/src/app

EXPOSE 3000

CMD ["bin/rails", "s", "-b", "0.0.0.0"]
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

COPY . /usr/src/app

RUN bundle install --system --jobs=4 --no-cache --without development test --clean \
&& apk del .build-dependencies

```

### Build the docker image

Once you've added the docker file you can build the base image of your app using
