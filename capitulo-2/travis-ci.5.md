# <a name="configurando-nodejs"></a> Nodejs

Neste exemplo, mostro como faço para rodar um projeto, que utiliza algumas bibliotecas específicas e necessitam de
configurações adicionais do ambiente para efetuar a instalação das mesmas, como a versão dos compiladores e etc, o
**Travis-CI** permite essas configurações "obscuras".

```
language: node_js

env:
  - CXX=g++-4.8

addons:
  apt:
    sources:
      - ubuntu-toolchain-r-test
    packages:
      - g++-4.8

node_js:
  - "5.1.1"
```
