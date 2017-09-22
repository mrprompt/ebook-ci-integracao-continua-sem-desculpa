# <a name="configurando-php"></a> PHP

Abaixo um exemplo básico, de um projeto feito em PHP, testando a compatibilidade com várias versões e permitindo a falha
do build em versões específicas.

```
language: php

php:
  - 7.0
  - 5.6
  - nightly
  - hhvm
  - hhvm-nightly

matrix:
  allow_failures:
    - php: nightly
    - php: hhvm
    - php: hhvm-nightly

before_script:
  - composer selfupdate
  - composer install --dev --prefer-dist

script:
  - ./vendor/bin/phpunit
```
