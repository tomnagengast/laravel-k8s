ARG PHP_EXTENSIONS="apcu bcmath pdo_mysql redis imagick gd"
FROM thecodingmachine/php:8.1-v4-fpm-node16 as php_base
ENV TEMPLATE_PHP_INI=production

# copy our laravel application to html
COPY --chown=docker:docker . /var/www/html
RUN composer install --quiet --no-dev # --optimize-autoloader
FROM node:16 as node_dependencies
WORKDIR /var/www/html
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=false

# bring in the laravel application from the php_base to our node js container
COPY --from=php_base /var/www/html /var/www/html
RUN npm set progress=false && \
    npm config set depth 0 && \
    npm install && \
    npm run build && \
    rm -rf node_modules
FROM php_base

# bring the finished build back into the php container
COPY --from=node_dependencies --chown=docker:docker /var/www/html /var/www/html
