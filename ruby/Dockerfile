FROM ruby:2.4.2-alpine3.6
LABEL maintainer: "Sergey Shkarupa <s.shkarupa@gmail.com>"

RUN apk add --no-cache \
  postgresql-client \
  nodejs \
  imagemagick \
  file \
  less \
  tzdata

RUN bundle config build.nokogiri --use-system-libraries

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
