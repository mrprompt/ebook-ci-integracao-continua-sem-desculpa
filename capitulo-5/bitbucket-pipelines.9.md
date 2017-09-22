#### <a name="configurando-multiplos-branchs"></a> Trabalhando com múltiplos branchs

```
image: node:6.0.0

pipelines:
  default:
    - step:
        script:
          - npm install
          - npm test

  branches:
    develop:
      - step:
          script:
            - npm install
            - npm test
            - npm run deploy:develop

    homolog:
      - step:
          script:
            - npm install
            - npm test
            - npm run deploy:homolog

    master:
      - step:
          script:
            - npm install
            - npm test
            - npm run deploy:production
```
