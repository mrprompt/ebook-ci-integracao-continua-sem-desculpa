# <a name="configurando-java"></a> Java

Não possuo experiência com **Java**, então, o exemplo a seguir eu busquei na documentação do próprio
**Travis-CI**. Abaixo, a configuração básica de um projeto utilizando o **Ant** e sendo compilado em
diversas versões do JDK.

```
language: java

jdk:
  - oraclejdk8
  - oraclejdk7
  - openjdk6

install: ant deps

script:
    - ant test
```
