ARG PHP_VERSION=8.4.27-fpm
# --------------------------------------------------
# Stage 1: PHP extensions
# --------------------------------------------------
FROM php:${PHP_VERSION} AS ext-builder

RUN apt-get update && apt-get install -y --no-install-recommends \
    libpq-dev \
    libzip-dev \
    $PHPIZE_DEPS \
    && docker-php-ext-install -j"$(nproc)" pdo_pgsql pgsql zip \
    && pecl install apcu \
    && docker-php-ext-enable apcu


#--------------------------------------------------
# Stage 2: Build PHP base image
#--------------------------------------------------
FROM php:${PHP_VERSION} AS php-base

RUN apt-get update && apt-get install -y --no-install-recommends \
    tzdata \
    libpq5 \
    libzip5 \
    bash \
    && rm -rf /var/lib/apt/lists/*

COPY --from=ext-builder /usr/local/lib/php/extensions/ /usr/local/lib/php/extensions/
COPY --from=ext-builder /usr/local/etc/php/conf.d/ /usr/local/etc/php/conf.d/

COPY ./conf/php/fpm-www.conf /usr/local/etc/php-fpm.d/www.conf
COPY ./conf/php/php.ini-production /usr/local/etc/php/php.ini

WORKDIR /var/www/html


# --------------------------------------------------
# Stage 3: Composer dependencies
# --------------------------------------------------
FROM php-base AS vendor-prod

COPY --from=composer:2 /usr/bin/composer /usr/local/bin/composer
COPY ./src/composer.json ./src/composer.lock ./

RUN apt-get update && apt-get install -y --no-install-recommends \
    unzip \
    && rm -rf /var/lib/apt/lists/*

RUN composer install \
    --no-dev \
    --no-scripts \
    --prefer-dist \
    --no-interaction \
    --no-progress

COPY ./src/app ./app

RUN composer dump-autoload \
    --no-dev \
    --optimize \
    --no-interaction


# --------------------------------------------------
# Stage 4: Production runtime
# --------------------------------------------------
FROM php-base AS production

ARG APP_VERSION=dev
ENV APP_VERSION=${APP_VERSION}

COPY ./src/app ./app
COPY ./src/public ./public
COPY --from=vendor-prod /var/www/html/vendor ./vendor

EXPOSE 9000

CMD ["php-fpm"]


# --------------------------------------------------
# Stage 5: Development runtime
# --------------------------------------------------
FROM php-base AS development

COPY --from=composer:2 /usr/bin/composer /usr/local/bin/composer

RUN apt-get update && apt-get install -y --no-install-recommends \
    unzip \
    && rm -rf /var/lib/apt/lists/*

RUN useradd -m -u 1000 -s /bin/bash developer

ENV HOME=/home/developer

USER developer

EXPOSE 9000

CMD ["php-fpm"]