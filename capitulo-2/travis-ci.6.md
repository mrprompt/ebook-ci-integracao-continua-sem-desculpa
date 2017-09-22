# <a name="configurando-angularjs"></a> Angularjs

Para os projetos em **Angular**, gosto muito de utilizar o **Protractor** pela sua praticidade de configuração.

```
language: node_js
node_js:
  - "0.12"

before_script:
  - export DISPLAY=:99.0
  - sh -e /etc/init.d/xvfb start
  - npm start > /dev/null &
  - npm run update-webdriver
  - sleep 1 # give server time to start

script:
  - npm run test-single-run
  - npm run protractor
```
