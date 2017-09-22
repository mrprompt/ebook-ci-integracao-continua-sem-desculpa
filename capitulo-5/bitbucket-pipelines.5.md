#### <a name="configurando-nodejs"></a> Nodejs

```
image: node:6.0.0

pipelines:
  default:
    - step:
        script:
          - npm install --silent --progress=false
          - npm test
```
Meu bloco **scripts** do package.json:

```
...
"scripts": {
  "start": "node app.js",
  "test": "mocha test/**/*Test.js",
  "coverage": "istanbul cover _mocha -- -R spec"
},
...
```
