#### <a name="configurando-php"></a> PHP

```
## Tests Config
# Set php version through phpenv. 5.3, 5.4, 5.5 & 5.6 available
phpenv local 7.0

# Install extensions through Pecl

# yes yes | pecl install memcache

# Install dependencies through Composer
composer install --prefer-source --quiet --dev --optimize-autoloader --no-interaction
```
```
### Pipeline
./vendor/phpunit
```
