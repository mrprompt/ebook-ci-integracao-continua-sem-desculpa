#### <a name="configurando-angularjs"></a> Angularjs

```
image: node:6.0.0

pipelines:
  default:
    - step:
        script:
          - npm install --silent --progress=false
          - npm run bower
          - npm run build
          - nohup bash -c "npm run webdriver-start 2>&1 &" && sleep 9
          - npm run start 2>&1  &
          - npm test
```

Meu bloco **scripts** do package.json:

```
...
"scripts": {
  "bower": "bower install",
  "build": "gulp build",
  "start": "gulp serve",
  "webdriver-start": "webdriver-manager update && webdriver-manager start",
  "test": "protractor protractor.conf.js"
},
...
```
