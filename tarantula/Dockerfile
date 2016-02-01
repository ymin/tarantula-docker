FROM ubuntu:14.04

ENV PATH /usr/local/rvm/bin:$PATH

RUN apt-get update && apt-get -y upgrade && apt-get -y install ruby 1.9.3

RUN ln -sf /usr/bin/ruby1.9.3 /etc/alternatives/ruby

# see update.sh for why all "apt-get install"s have to stay as one long line
RUN apt-get update && apt-get install -y nodejs --no-install-recommends && rm -rf /var/lib/apt/lists/*

# see http://guides.rubyonrails.org/command_line.html#rails-dbconsole
RUN apt-get update && apt-get install -y mysql-client postgresql-client sqlite3 --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y \
        build-essential libmysqlclient-dev libpcre3 libssl-dev libxml2-dev \
        memcached mysql-server\
        zlib1g-dev openssl git-core \
        libcurl4-openssl-dev zlib1g-dev \
        libapr1-dev libaprutil1-dev

ENV RAILS_VERSION 3.2.11

RUN gem install rails --version "$RAILS_VERSION"

# install bundler
RUN gem install bundler

RUN git clone https://github.com/ymin/tarantula.git

WORKDIR /tarantula

# install all dependances
RUN bundle install