FROM ruby:2.4.1-alpine
MAINTAINER Sergey Shkarupa <s.shkarupa@gmail.com>

ENV SYSTEM_DEPS \
  postgresql-client \
  nodejs \
  imagemagick \
  file \
  tzdata

RUN apk --no-cache add $SYSTEM_DEPS

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
