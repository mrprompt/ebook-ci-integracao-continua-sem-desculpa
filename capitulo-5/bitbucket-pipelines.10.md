## Containers auxiliares

Deu de notar que to completamente viciado no Bitbucket Pipelines? Pois é, como disse, tenho utilizado ele todos os dias
na [BeeTech](https://www.beetech.global), então, nada mais natural do que ir acompanhando - e aplicando - as novidades 
que vão aparecendo.

Um pouco antes do [Cache](/2017/07/21/integracao-continua-pipelines-cache/), foi implementado o recurso de containers paralelos,
ou auxiliares, como queira chamar, que nada são que container que rodam junto com seu fluxo de CI. Como um banco de
dados por exemplo.

Você não precisa instalar o PostgreSQL no seu container ou outros serviços "pesados" que precisem estar a postos antes
de rodar seus testes, você pode facilmente chamar um container auxiliar eu seu fluxo e pronto, o Pipelines vai subir 
esta instância, e deixa-la disponível para seus testes.

A sintaxe é bem simples, vou mostrara abaixo, como subir um container contendo o PostgreSQL:

```
image: node

pipelines:
  default:
    - step:
        caches:
          - node
        script:
          - npm install --progress=false
          - npm test
        services:
          - database

definitions:
  services:
    database:
      image: sameersbn/postgresql:9.6-2
      environment:
        DB_USER: 'foooooo'
        DB_PASS: 'baaaaar'
        DB_NAME: 'foobaar
```

Como disse, a sintaxe é simples, basta você setar um alias para o serviço, em nosso caso "database", e nas suas "definitions" 
configurar o serviço, que pode ser qualquer imagem Docker, seguido dos parâmetros que você utilizaria para rodar o container
normalmente.

Simples não? Com isso, com certeza seu fluxo de CI ficará bem mais rápido e cada vez menos engessado - ou no mínimo, seu container 
diminuirá drasticamente de tamanho.

Até a próxima!