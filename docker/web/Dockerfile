FROM ruby:2.5.1-slim
RUN apt-get update -qq && \
  apt-get install -y build-essential libpq-dev default-libmysqlclient-dev git curl && \
  curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
  apt-get install -y nodejs npm
RUN mkdir /app

ADD Gemfile /tmp/Gemfile
ADD Gemfile.lock /tmp/Gemfile.lock
RUN cd /tmp && bundle install -j5

ADD vendor/assets/package.json /tmp/vendor/assets/package.json
RUN cd /tmp/vendor/assets && npm install && rm -rf node_modules/jquery

WORKDIR /app
RUN mv /tmp/vendor /app
ADD . /app
