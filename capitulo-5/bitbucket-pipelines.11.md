## Cache

Um dos maiores problemas na integração contínua, é a instalação de todas as dependências do 
projeto até chegar na produção de artefatos limpos. Rodar um ``composer install`` ou um ``npm install`` 
a cada build pode ser custoso e demorado. Nenhum time quer esperar vários minutos para saber se 
um push é válido ou não, isso atrasa e muito as entregas.

Uma atualização bacanuda é a possibilidade de utilizarmos cache para as dependências dos nossos projetos.

A instação é bem simples, vou colocar um exemplo prático, para cachearmos as dependências administradas 
pelo composer em uma aplicação PHP:

```yml
image: php:7.1.6-cli

pipelines:
  default:
    - step:
        caches:
          - composer
        script:
          - curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
          - composer install
          - ./vendor/bin/phpunit -c phpunit.xml.dist
```

Bem simples não? Como você pode ver, apenas adicionamos o tipo de cache que queremos utilizar, o Pipelines nos dá
várias opções pré-configuradas para diversas linguagens, mas também podemos utilizar o nosso próprio, como mostrarei
abaixo, para aplicações em angular:

```yml
image: node

pipelines:
  default:
    - step:
        caches:
          - node
          - bower
        script:
          - npm install --progress=false
          - ./node_modules/.bin/bower install --allow-root
          - npm test

definitions:
  caches:
    bower: bower_components
```

Como você pode ver, utilizei uma configuração pré-existente (node) e uma customizada (bower) para cache.

Para saber mais, veja a [documentação oficial](https://goo.gl/AwCzxH).
