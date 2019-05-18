ARG PHP_IMAGE

# <Container[php]>

FROM ${PHP_IMAGE} AS php

LABEL maintainer="Vladyslav Shykanov <v.shykanov@gmail.com>" \
	  service="php"

RUN apk add --no-cache --virtual .build-deps \
	$PHPIZE_DEPS \
	autoconf \
	ca-certificates \
	icu-dev \
    libzip-dev \
    zip

RUN docker-php-ext-install mbstring zip pcntl bcmath opcache ctype pdo_mysql


RUN addgroup -g 1000 -S user && \
    adduser -u 1000 -S user -G user

ENV COMPOSER_HOME /home/user/.composer

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN chown user:user /home/user/.composer

WORKDIR /application

# </Container>

# <Container[dev]>

FROM php AS dev

LABEL service="dev"

COPY . /application

# </Container>

# <Container[local]>

FROM dev AS local

LABEL service="local"

ARG COMPOSER_GLOBAL_PACKAGES

USER root

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

COPY ./docker/php/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN apk add --no-cache zsh \
    vim \
	git

RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER user

RUN composer global require ${COMPOSER_GLOBAL_PACKAGES}

ENV PATH="./vendor/bin:/home/user/.composer/vendor/bin/:${PATH}"
ENV LANG C
ENV TERM xterm

RUN sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

COPY ./docker/workspace/.zshrc /home/user/.zshrc

# </Container>
