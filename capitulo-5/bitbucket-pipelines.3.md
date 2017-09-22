### <a name="configurando"></a> Configurando

Finalizando os passos, será criado no projeto o arquivo **bitbucket-pipelines.yml**, contendo a configuração do ambiente e dos passos necessários para alcançar o sucesso do nosso build.

Aqui vem a parte chata da configuração, toda modificação que você fizer neste arquivo, é um commit + push que você precisa mandar pro projeto - você também pode rodar os builds localmente, mas [dá trabalho](https://confluence.atlassian.com/bitbucket/debug-your-pipelines-locally-with-docker-838273569.html).  Pessoalmente, acho um pouco chato isso e suja o projeto, mas vamos lá.

O ambiente de integração, utiliza containers do Docker para rodar, então, o nosso primeiro passo na configuração do projeto, e informar a imagem que precisamos utilizar para nosso build. Esta imagem pode ser tanto um container disponível no [Docker Hub](hub.docker.com) quanto um container próprio.

Caso você não especifique uma imagem, será utilizada uma [imagem padrão](https://hub.docker.com/r/atlassian/default-image/), baseada no [Ubuntu 14.04](http://releases.ubuntu.com/14.04/), disponibilizada pelo time da [Atlassian](https://br.atlassian.com/), que contém algumas ferramentas por padrão:

- wget
- xvfb
- curl
- git: 1.9.1
- java: 1.8u66
- maven: 3.0.5
- node: 4.2.1
- npm: 2.14.7
- nvm: 0.29.0
- python: 2.7.6
- gcc: 4.8.4

A configuração do Pipelines é baseado em blocos de passos, chamado no arquivo de configuração de **step**.

Cada **step** possui um **script**, que são os comandos rodados para a conclusão do build. Cada linha, do script, é um comando rodado após o término do anterior.

O bloco **default** irá rodar os passos configurados nele para todos os branchs que receberem uma atualização, como um push ou um merge.

Você também pode criar blocos de configurações para determinados branchs ou tags, e rodar os passos achar necessário. Eu gosto muito desse tipo de configuração, para disparar o evento de deploy, que sempre deixo a cargo de outra ferramenta.

Um exemplo do arquivo de configuração é esse:

```
# This is a sample build configuration for PHP.
# Check our guides at https://confluence.atlassian.com/x/VYk8Lw for more examples.
# Only use spaces to indent your .yml configuration.
# -----
# You can specify a custom docker image from Docker Hub as your build environment.
image: phpunit/phpunit:5.0.3

pipelines:
  default:
    - step:
        script: # Modify the commands below to build your repository.
          - composer install
```

Você pode ter uma referência completa do arquivo de configurações [aqui](https://confluence.atlassian.com/bitbucket/configure-bitbucket-pipelines-yml-792298910.html).
