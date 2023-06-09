# FROMはベースとなるイメージを指定する
FROM php:8.0-fpm
# 作成したユーザーの情報
COPY php.ini /usr/local/etc/php/

# 必要なパッケージのインストール
RUN apt-get update \
  && apt-get install -y zlib1g-dev mariadb-client vim libzip-dev \
  && docker-php-ext-install zip pdo_mysql

#Composer install
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
# Composerとは、PHPのパッケージ管理ツールです。
# これを使うことで、PHPのライブラリを簡単にインストールすることができます。
# また、Laravelのインストールにも必要になります。


ENV COMPOSER_ALLOW_SUPERUSER 1

ENV COMPOSER_HOME /composer

ENV PATH $PATH:/composer/vendor/bin


WORKDIR /var/www

# RUNコマンドで、コンテナ内で実行するコマンドを指定する
RUN composer global require "laravel/installer"

