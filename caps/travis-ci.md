# Integração Contínua com Travis-CI

O **Travis-CI**, é um dos queridinhos e escolhido por 9 entre cada 10 dentistas, não péra, vamos de novo...
Senhoras e senhores, apresentando a vocês, o incrível: **Travis-CI**!!!

<img src="/assets/travis/travis-ci.svg" class="img img-responsive pull-right" alt="Travis-CI Logo">

Um boa parte dos projetos que encontramos no **GitHub**, que possuam um mínimo de testes, utilizam
o **Travis-CI** como sua principal ferramenta de integração contínua e testes automatizados; isso porque
ele é totalmente gratuito para projetos de código aberto, e além de suas inúmeras integrações, é muito
fácil e rápido de configurar e integrar ao controle de versão utilizado.

Pra ficar mais fácil de entender e conhecer a ferramenta, vou dividir este post em alguns tópicos. Vamos lá.

- [Apresentação](#apresentacao)
- [Cadastro](#cadastro)
- [Configurando](#configurando)
    - [PHP](#configurando-php)
    - [Nodejs](#configurando-nodejs)
    - [Angularjs](#configurando-angularjs)
    - [Ruby](#configurando-ruby)
    - [Java](#configurando-java)
- [Prós & Contras](#pros-e-contras)
- [Conclusão](#conclusao)
- [Mais Informações](#mais-informacoes)

### <a name="apresentacao"></a> Apresentação

Manter um ambiente de testes e integração contínua, é imprescindível para qualquer projeto ou desenvolvedor
sério, que queira manter sua produtividade em alta e foco na entrega de valor de cada demanda, e não em tarefas
repetitivas e passíveis de erro.

<img src="/assets/travis/travis-ci.png" class="img img-responsive" alt="Travis-CI Screenshot">

Com disse, o Travis é o mais escolhido nos projetos open source, justamente pela sua facilidade para
configurar, quanto para integrar ao CVS utilizado no projeto.

Sua interface é realmente muito simples e sem botões para se perder ou funcionalidades inúteis. O suporte a
múltiplas linguagens também é um grande atrativo.

Com poucas linhas, é possível subir seu ambiente de testes e começar a testar seus projetos, assim como
disparar gatilhos no caso de sucesso ou falhas. Fora o "badge" bacana que tu pode colocar no _README_ do
projeto ;)

### <a name="cadastro"></a> Cadastro

O cadastro é simples e rápido, bastando você se logar com sua conta do **GitHub** e logo você cai na Dashboard,
onde estão seus projetos listados em uma coluna à esquerda e o status detalhado do build do projeto selecionado.
<img src="/assets/travis/shot-travis-dashboard.png" class="img img-responsive" alt="Travis-CI - Dashboard">

Caso seja seu primeiro acesso, você não terá nenhum projeto listado, tendo que habilitar na tela de configurações que
veremos a seguir com detalhes.

### <a name="configurando"></a> Configurando

Tão simples quanto o cadastro é a configuração do **Travis-CI** para cada projeto.
<img src="/assets/travis/shot-travis-settings.png" class="img img-responsive" alt="Travis-CI - Settings">

Nela você pode configurar dentre as variáveis de ambiente - caso seu projeto utilize - se o build ocorrerá somente nos
"pushs" do projeto ou também sobre cada pull request - ótimo e aconselhável.

O arquivo _.travis.yml_ é onde ficam as configurações necessárias para rodar os testes e etc, abaixo, o arquivo de
configuração de um projeto simples em _PHP_:

```
language: php

php:
  - 7.0

before_script:
  - composer install --dev --prefer-dist

script:
  - ./vendor/bin/phpunit
```

Não se assuste com nada, é só um exemplo. Mas você já pode ver que com poucas linhas, você já tem seu projeto sendo
testado automaticamente a cada Push ou <abbr title="Pull Request">PR</abbr>.

No arquivo você também pode configurar ações para cad etapa do build, são elas:

1. before_install
2. install
3. before_script
4. script
5. after_success or after_failure
6. before_deploy *
7. deploy *
8. after_deploy *
9. after_script

As ações marcadas com "*" são opcionais no arquivo de configuração. Na verdade, você também não é obrigado a configurar todos
os passos citados ;)

<img src="/assets/travis/shot-travis-accounts.png" class="img img-thumbnail pull-right" alt="Travis-CI - Accounts">
Também é possível clicar no canto superior direito, acessando o menu _Accounts_ para integrar - ou desligar - outros projetos
que você tenha acesso.

Sua conta e organizações que você esteja vinculado, ficarão listados na coluna a esquerda, bastando clicar sobre, para obter uma
listagem de projetos do qual você possu permissão de acesso.

A direita, temos a listagem de projetos, e também o botão de sincronização. O **Travis-CI** sincroniza sua conta de tempos em tempos,
porém, as vezes é necessário dar uma clicada ali para obter uma listagem mais recente, principalmente se você acabou de criar
o projeto no **GitHub**.

Na listagem, é possível habilitar e desabilitar a integração com o **Travis-CI**, assim como ir direto às configurações do projeto,
como falado anteriormente.

Na imagem abaixo, temos um exemplo de projetos integrados e não integrados com a ferramenta, assim como algumas organizações que
possuo acesso através do [meu **GitHub**](https://github.com/mrprompt).

<img src="/assets/travis/shot-travis-accounts-2.png" class="img img-thumbnail" alt="Travis-CI - Accounts 2">

Com o **Travis** habilitado para seu projeto, você pode ir até a página do projeto no **GitHub** e olhar as configurações do
serviço, na aba _Webhooks & Services_, nela, você verá uma imagem semelhante a abaixo, onde você poderá ver serviço habilitado.

<img src="/assets/travis/shot-github-settings-services.png" class="img img-thumbnail" alt="GitHub - Webhooks & Services">

Clicando no lápis, teremos detalhes da configuração - não se preoupce, você não precisa mexer em nada aqui:

<img src="/assets/travis/shot-github-settings-services-travis.png" class="img img-thumbnail" alt="GitHub - Webhooks & Services - Travis">

Você também pode testar o serviço, sem ter que fazer um push para seu repositório, clicando no botão "Test service" logo no topo.

### Bônus Track - Exemplo de configuração para cada linguagem

Para deixar tudo bem claro e simples, vou listar abaixo, alguns exemplos do arquivo _.travis.yml_ para algumas linguagens.

Com excessão do Java, todos os exemplos são totalmente funcionais e utilizo também em meus projetos. Neles, é possível ver a
simplicidade do arquivo de configuração, e com um pouco de imaginação, é possível criar uma configuração que crie o ambiente de
testes com o máximo de semelhança possível com o ambiente de produção em pouco tempo. Assim como a configuração do
_[deploy](https://pt.wikipedia.org/wiki/Ambiente_de_desenvolvimento_integrado)_ automatizado no caso de sucesso no build.

#### <a name="configurando-php"></a> PHP

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

#### <a name="configurando-nodejs"></a> Nodejs

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

#### <a name="configurando-angularjs"></a> Angularjs

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

#### <a name="configurando-ruby"></a> Ruby

Não possuo experiência com Ruby além de minúsculos projetos de exemplo e alguns sites hospedados no **GitHub**, que
utilizam o **Jekyll** como base. Neste exemplo, mostro como rodar um projeto em **Jekyll** hospedado no próprio
**GitHub**. Nele, rodo o build do **Jekyll** e o **HtmlProofer**, para analisar links e etc. Porém, rodo somente
no branch **master** os testes.

```
language: ruby
rvm:
- 2.1

# Assume bundler is being used, therefore the `install` step will run `bundle install` by default.
script:
    - bundle exec jekyll build
    - bundle exec htmlproof --allow-hash-href --disable-external --empty-alt-ignore ./_site

# branch whitelist, only for GitHub Pages
branches:
  only:
  - master

env:
  global:
  - NOKOGIRI_USE_SYSTEM_LIBRARIES=true # speeds up installation of html-proofer
```

#### <a name="configurando-java"></a> Java

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

### <a name="pros-e-contras"></a> Prós & Contras

O **Travis-CI** na minha opinião é uma ferramenta fantástica e incrivelmente simples de configurar.

Só pelo seu modelo de apoio a projetos de código aberto, pra mim já é suficiente para votar no uso
e incentivar a todos.

Como único ponto contra, é o preço final para projetos privados, que - com o atual valor do dólar -
é um tanto quanto salgado, no momento em que escrevo este post, o plano mais simples gira em torno de
$129.

Para uma grande empresa talvez não seja problema, mas para pequenas empresas ou freelancers - como é
o meu caso - é um serviço bem caro para se manter, deixando como opção, outras ferramentas que
disponibilizam o mesmo uso, mas para um número limitado de projetos privados, ou mesmo instalar outra
ferramenta de CI em um servidor próprio.

### <a name="conclusao"></a> Conclusão

O **Travis-CI** é indiscutivelmente, minha primeira opção para projetos no **GitHub** ou de código
aberto, justamente pela sua simplicidade de configuração e maturidade.

Sua flexibilidade permite a definição perfeita do ambiente de integração contínua, com a segurança
de manter as informações privadas de forma segura e um suporte realmente incrível as mais diversas
linguagens e ambientes - permitindo inclusive a configuração de múltiplos sistemas operacionais.

#### <a name="mais-informacoes"></a> Mais Informações

Se você estiver interessado em obter mais informações sobre o **Travis-CI**, fique a vontade para comentar
ou me enviar um e-mail.

Abaixo, deixo alguns links interessantes para quem deseja começar a utilizar
o **Travis-CI** em seus projetos.

- [Travis-CI - Projetos Open Source](https://www.travis-ci.org)
- [Travis-CI - Projetos Privados](https://travis-ci.com/plans)
- [Travis-CI - Iniciando](https://docs.travis-ci.com/user/getting-started/)
- [Travis-CI - Customizando o Build](https://docs.travis-ci.com/user/customizing-the-build/)

Até mais, e nos vemos no próximo artigo, onde falarei um pouco sobre outra ferramenta incrível, o
**[CodeShip](https://codeship.com/)**.