FROM wordpress:5.1-php7.3

# pcov setup for code coverage generation
RUN pecl install pcov \
  && docker-php-ext-enable pcov

# Composer setup
RUN curl -sS https://getcomposer.org/installer | php \
  && chmod +x composer.phar && mv composer.phar /usr/local/bin/composer

# Node setup
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - \
  && apt-get install -yq nodejs build-essential

# Install npm
RUN npm install -g npm

# Install requirements for wp-cli support
RUN apt-get update \
  && apt-get install -y sudo less mariadb-client \
  && rm -rf /var/lib/apt/lists/*

# Install wp-cli
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
  && php wp-cli.phar --info \
  && chmod +x wp-cli.phar \
  && mv wp-cli.phar /usr/local/bin/wp

COPY entrypoint.sh /entrypoint.sh

WORKDIR /usr/src/wordpress

ENTRYPOINT ["/entrypoint.sh"]
