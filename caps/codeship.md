---
layout: post
author: mrprompt
comments: true
date: 2016-04-02 12:21:01+00:00
slug: integracao-continua-codeship
title: Integração Contínua com CodeShip
---

<img src="{{ site.baseurl }}/upload/ci/codeship/codeship.png" class="img img-responsive pull-right" alt="Codeship Logo" title="Codeship" width="250">
Continuando a [série sobre Integração Contínua]({% post_url 2016-03-25-falando-sobre-integracao-continua-e-qualidade-de-desenvolvimento %}), partimos
agora para o [CodeShip](http://www.codeship.com), que assim como o [Travis-CI]({% post_url 2016-03-26-integracao-continua-travis-ci %}), também é uma
ótima ferramenta online para implantar Integração Contínua em seus projetos.

Mas ao contrário do [Travis-CI](https://www.travis-ci.org), o **CodeShip** nos permite adicionar repositórios privados sem custo algum - mas o limite
é de 5 repositórios - assim como ilimitados repositórios de projetos de código fonte aberto.

Assim como no último post, vamos dividir este também em algumas partes, para facilitar a leitura e o entendimento da ferramenta.

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

Conheço a relativamente pouco tempo o **CodeShip**, mas sua facilidade de uso e simplicidade me convenceram logo de cara a
utilizá-lo no projeto de um cliente, e logo tomei-o também para alguns [projetos pessoais](https://github.com/mrprompt), como
alternativa ao **Travis-CI**.

Claro que a primeira coisa que me chamou a atenção, foi a possibilidade de utilizá-lo gratuitamente para projetos privados,
mesmo com um número limitado de builds mensais para estes - no momento em que escrevo este artigo, o limite é de 100 builds.

Uma funcionalidade muito interessante é a possibilidade de rodar testes em paralelo, para agilizar o processo de build, porém, esta
somente está disponível para contas pagas - mas você pode testar por duas semanas sem compromisso ;)

<img src="{{ site.baseurl }}/upload/ci/codeship/codeship-parallelci.png" class="img img-responsive" alt="Codeship - Paralell Build" title="Codeship - Parallel">

### <a name="cadastro"></a> Cadastro

O cadastro é simples, com poucos campos - bastando você informar seu nome, email, senha e pronto - ou conectar-se diretamente
com sua conta do [Bitbucket](https://www.Bitbucket.com) ou [GitHub](https://www.github.com). No caso dos dois sites, você
também pode conectá-los depois do cadastro, facilmente.

Eu preferi conectar diretamente com minha conta do **Bitbucket** e fiz a integração com o **GitHub** posteriormente, sem problema
algum.

Após efetuar o cadastro, você cai direto na DashBoard, onde ficam listados os últimos builds - claro que no caso de novos cadastros,
somente é apresentada uma tela de boas vindas e adição de projeto.

Na imagem abaixo, mostro a tela inicial, com builds com sucesso e outros com falhas para você ver:
<img src="{{ site.baseurl }}/upload/ci/codeship/shot-codeship-dashboard.png" class="img img-responsive" alt="Codeship - DashBoard" title="Codeship - DashBoard">
<small>Nenhum projeto foi sacrificado ou sofreu crueldades para produzir esta imagem.</small>

### <a name="configurando"></a> Configurando

A configuração do **CodeShip** é toda por sua interface, que aliás, é muito simples e resumida, sem muitas surpresas.
O primeiro passo, é selecionar o ambiente a ser utilizado, basicamente, você seleciona a plataforma e ele te da algum exemplo de código, como abaixo.
<img src="{{ site.baseurl }}/upload/ci/codeship/shot-codeship-environments.png"  class="img img-responsive" alt="Codeship - Configurando 1" title="Codeship - Environment">

Após a escolha, é possível editar e dar uma melhorada no ambiente. Nas contas pagas, é possível definir diversos "pipelines", ou seja, rodar diversas métricas em
paralelo, para melhorar a performance. Testei em um projeto e não tive um ganho muito significativo pra compensar o uso pra falar a verdade, mas creio que isso
seja um problema na minha arquitetura.
<img src="{{ site.baseurl }}/upload/ci/codeship/shot-codeship-tests.png"  class="img img-responsive" alt="Codeship - Configurando 2" title="Codeship - Environment">
<small>É possível utilizar algumas variáveis de ambiente pré-definidas</small>

Existem ainda as diversas integrações para configurar o deploy automatizado, como **AWS**, **Digital Ocean** e etc., assim como também é possível você
rodar seu próprio script, ou mesmo o **Curl** para enviar uma chamada a outro serviço, como é o meu caso com o **DeployBot** - esse eu prentendo falar em um outro
artigo futuro.
<img src="{{ site.baseurl }}/upload/ci/codeship/shot-codeship-deploy.png"  class="img img-responsive" alt="Codeship - Configurando 3" title="Codeship - Environment">

Finalizando a configuração do **Deploy**, você também pode configurar notificações:
<div class="row">
    <div class="col-sm-12 col-lg-6">
        <img src="{{ site.baseurl }}/upload/ci/codeship/shot-codeship-hooks.png"  class="img img-responsive" alt="Codeship - Configurando 3" title="Codeship - Environment">
    </div>
    <div class="col-sm-12 col-lg-6">
        <img src="{{ site.baseurl }}/upload/ci/codeship/shot-codeship-hooks-2.png"  class="img img-responsive" alt="Codeship - Configurando 3" title="Codeship - Environment">
    </div>
</div>

Assim como o **Travis-CI** e outros serviços, também é possível configurar as próprias variáveis de ambiente, para serem utilizadas durante o processo:
<img src="{{ site.baseurl }}/upload/ci/codeship/shot-codeship-config-environment.png" class="img img-responsive" alt="Codeship - Configurando 3" title="Codeship - Environment">

E se tudo der certo - ou mesmo se der tudo errado -, você pode conferir os detalhes do build:
<img src="{{ site.baseurl }}/upload/ci/codeship/shot-codeship-success.png" class="img img-responsive" alt="Codeship - Configurando 3" title="Codeship - Environment">

#### Bônus Track - Exemplos de Configuração

Como não poderia deixar de faltar, vou mostrar alguns exemplos de configuração para algumas linguagens comumente usadas

#### <a name="configurando-php"></a> PHP

```
## Tests Config
# Set php version through phpenv. 5.3, 5.4, 5.5 & 5.6 available
phpenv local 7.0

# Install extensions through Pecl

# yes yes | pecl install memcache

# Install dependencies through Composer
composer install --prefer-source --quiet --dev --optimize-autoloader --no-interaction
```
```
### Pipeline
./vendor/phpunit
```

#### <a name="configurando-nodejs"></a> Nodejs

```
# Tests
nvm install 0.10
npm install
```

```
# Pipeline
npm run test-single-run
```

#### <a name="configurando-angularjs"></a> Angularjs

```
# Tests
nvm install 0.10
npm install
```

```
# Pipeline
npm run protractor
```

#### <a name="configurando-ruby"></a> Ruby

```
# Tests
rvm use 2.2.0 --install
bundle install
```
```
# Pipeline
bundle exec jekyll build
bundle exec htmlproof --allow-hash-href --disable-external --empty-alt-ignore ./_site
```

#### <a name="configurando-java"></a> Java

```
# Tests
ant deps
```

```
# Pipeline
ant test
```

### <a name="pros-e-contras"></a> Prós & Contras

O **CodeShip** é simples e prático de configurar por isso mesmo tornou-se rapidamente uma das minhas ferramentas de uso constante nos
projetos.
Seu processo de build é relativamente rápido e com suas diversas integrações, você pode, de forma simples e direta, configurar um
deploy automatizado ao final dos testes.
O suporte a processos paralelos é um grande atrativo, porém, em meus testes não obtive um resultado que compensasse a troca de plano.

O valor não é um grande atrativo para nós reles mortais brasileiros, o plano mais barato fica em torno de **$49** no momento em que escrevo
esse artigo, com suporte a dois "Pipelines" e um número ilimitado de projetos, tanto privados quanto públicos.

Também existe um plano intermediário, recente, com suporte a **Docker**, que parece ser muito interessante, porém, não tive a chance de
testar ainda, então, não tenho muito o que dizer.

O suporte a times também é um diferencial, possibilitar que você crie um ambiente compartilhado com a equipe para que todos possam
acompanhar de perto todo o processo é excelente ao meu ver, e se você puder fazê-lo, faça!

### <a name="conclusao"></a> Conclusão

Logo a primeira vista, o **CodeShip** demonstra ser uma excelente ferramenta, e no decorrer do uso, ela prova isso.
Sua documentação é simples e vai direto ao ponto, durante meus testes, foi realmente tranquilo obter as informações necessárias para
definir o ambiente de testes e o processo de publicação.

Como não poderia deixar, ele também possibilita o uso dos **Badges** - todo programador gosta de colocar um frufru no *README*, admita.
<img src="{{ site.baseurl }}/upload/ci/codeship/shot-codeship-badge.png" class="img img-responsive" alt="Codeship - Badge" title="Codeship - Badge">

Então é isso, o **CodeShip** é mais que recomendado para você que quer iniciar um processo de Integração ou Entrega contínua em seus
projetos, mas não quer perder tempo com arquivos de configuração, configuração de servidores ou longos processos.

Sua configuração simplificada e integração direta com o **BitBucket** e **GitHub** facilitam e muito o uso por grande parte das equipes
e facilita sua implantação. Poder utilizar a ferramenta gratuitamente para projetos OpenSource também é um grande diferencial, claro.

### <a name="mais-informacoes"></a> Mais Informações

- [Documentação](https://codeship.com/documentation)
- [Suporte a Docker](http://pages.codeship.com/docker)
- [Integração Contínua](https://codeship.com/documentation/continuous-integration/)
- [Deploy Contínuo](https://codeship.com/documentation/continuous-deployment/)

O próximo da lista é [Jenkins](https://jenkins.io/), prepare-se e até lá ;)