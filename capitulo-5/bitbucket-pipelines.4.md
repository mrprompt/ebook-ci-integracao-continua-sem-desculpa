#### <a name="configurando-php"></a> PHP

```
image: phpunit/phpunit:5.0.3

pipelines:
  default:
    - step:
        script:
          - composer --version
          - phpunit --version
          - composer install
          - phpunit --configuration tests/phpunit.xml
```
