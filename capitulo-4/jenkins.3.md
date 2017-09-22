### <a name="configurando"></a> Configurando

O Jenkins precisa que as ferramentas que você necessita para rodar o seu build (como a versão correta do PHP, Nodejs ou JDK por exemplo) estejam devidamente configuradas e funcionais na máquina hospedeira, então, fique sempre atento a isso.

Antes de criarmos um trabalho, vamos configurar alguns ítens importantes, clicando em **Gerenciar Jenkins** no menu a direita e após em **Configurar o Sistema**.

Nesta tela, você pode configurar uma mensagem de boas vindas, o número de executores, que define quantos builds você pode fazer em paralelo. Lembre que cada executor é uma thread, então não exagere. O padrão é dois.

<img src="assets/07-config.png" class="img img-responsive img-thumbnail" alt="Config" title="Configuração - Boas vindas e executores">

Outro ítem importante - mas não obrigatório -, são as variáveis de ambiente. Eu gosto muito de utilizar este recurso, para definir qual ambiente, acessos a serviços e etc.

<img src="assets/08-config-envvars.png" class="img img-responsive img-thumbnail" alt="Variáveis de ambiente" title="Configuração - Variáveis de ambiente">

Se você deseja que o resultados dos builds sejam enviados por email, é importante configurar também, um servidor SMTP para o envio das mensagens:

<img src="assets/09-config-smtp.png" class="img img-responsive img-thumbnail" alt="SMTP" title="Configuração - SMTP">

Uma outra sessão muito importante é a de plugins, lá você encontrará muita coisa interessante para deixar o seu Jenkins ainda mais turbinado, é extensa a lista e compensa separar alguns minutos - ou horas - para testar alguns plugins. Alguns que recomendo:

- [Publish Over SSH](https://wiki.jenkins-ci.org/display/JENKINS/Publish+Over+SSH+Plugin)
- [S3 publisher plugin](https://wiki.jenkins-ci.org/display/JENKINS/S3+Plugin)
- [Bitbucket Plugin](https://wiki.jenkins-ci.org/display/JENKINS/BitBucket+Plugin)
- [Ci Skip Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Ci+Skip+Plugin)

A lista é curta, mas isso é diversão e vou deixar por sua conta, apenas tenha em mente que, encher o ambiente de plugins, não é lá uma ótima idéia ;)

Agora precisamos configurar como o Jenkins irá se comunicar com nossos servidores e sistemas de controle de versão. Eu recomendo a criação de uma chave SSH própria para o usuário do Jenkins no servidor onde ele esta rodando, no nosso caso, nosso container. Vamos primeiro acessar o container, e criar a chave manualmente:

```
jenkins@50df04956a9c:~$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/var/jenkins_home/.ssh/id_rsa):
Created directory '/var/jenkins_home/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /var/jenkins_home/.ssh/id_rsa.
Your public key has been saved in /var/jenkins_home/.ssh/id_rsa.pub.
The key fingerprint is:
1f:88:67:90:dd:84:5e:8c:fa:3c:69:b7:c9:e8:02:a1 jenkins@50df04956a9c
The key's randomart image is:
+---[RSA 2048]----+
|         +.      |
|       oooo      |
|      oo...      |
|    . .o..       |
|   . ..oS..      |
|  E .  o*...     |
|     . . =.o     |
|      . . +      |
|       o.        |
+-----------------+
```

Agora, voltando para nossa interface do Jenkins, clicando no menu a direita, vamos em **Credentials**, **System**, **Global credentials** e finalmente em **Add Credentials**. Onde iremos nos deparar com a tela a seguir, que nos permitirá configurar vários meios de autenticação, por hora, ficaremos apenas definindo que o Jenkins utilizará a chave do usuário padrão do container.

<img src="assets/10-credentials.png" class="img img-responsive img-thumbnail" alt="Credenciais" title="Credenciais - Chave SSH">

### <a name="trabalho"></a> Criando o primeiro trabalho

Agora que temos nosso Jenkins configurado, podemos nos aventurar a conhecer a tela de criação de trabalhos do Jenkins, é nela é claro, que vamos configurar todos os passos do nosso build. Aqui, é importante configurar todos os passos necessários, para garantir que todo o fluxo de construção de nossa versão estável rode perfeitamente. A dica é, se você hoje faz todo o processo manual, anote os passos para não esquecer de nenhum, e aí sim, configure os mesmos no Jenkins.

Os passos de build vai de cada aplicação, mas não foge muito do processo:

```
clonar -> dependências -> testes -> build -> publicação
```

Nosso primeiro passo é ao clicar em "Novo job", selecionar o tipo de projeto que vamos configurar, para um primeiro passo, prefiro utilizar o "free-style", que é uma configuração limpa e podemos prosseguir configurando os passos conforme a necessidade de nosso projeto.

<img src="assets/11-novo-job.png" class="img img-responsive img-thumbnail" alt="Tipos" title="Jenkins - Tipos de projetos">

Com o tipo de projeto configurado, vamos nos deparar com a tela de configuração do trabalho em si, onde iremos configurar todos os detalhes do projeto.

Na primeira parte, vemos como configurar além do nome do projeto - procure não mudar aqui, nem utilizar caracteres estranhos, a cópia de trabalho é baseada neste nome - um espaço para preenchermos uma descrição do mesmo. Você pode utilizar este espaço para exibir uma imagem com a sua cobertura de código por exemplo ;)

<img src="assets/12-job-geral.png" class="img img-responsive img-thumbnail" alt="Detalhes" title="Jenkins - Detalhes do projeto">

Em seguida, temos a opção de **Descartar builds antigos**, importante para salvarmos nosso espaço em disco, já que cada build, pode ocupar um espaço considerável em disco, contabilize quanto isso não daria por semana ou mês.

Eu procuro não manter um número muito grande de builds armazenados, já que os mesmos rodam a cada push - e vai por mim, você também não vai querer que seu disco encha rapidamente - mas é importante ter um número suficiente que te permita voltar a um estado anterior a publicação atual.

<img src="assets/13-historico-de-builds.png" class="img img-responsive img-thumbnail" alt="Histórico" title="Jenkins - Número de builds a se manter">

Em seguida, selecionando o nosso controle de versão definimos o endereço do nosso repositório, assim como o branch a ser observado.

<img src="assets/14-codigo-fonte.png" class="img img-responsive img-thumbnail" alt="Código Fonte" title="Controle do Código Fonte">

É também nesta tela que podemos definir qual o tipo de autenticação iremos utilizar para autenticar o Jenkins em nosso repositório, clicando em **Credentials** podemos selecionar a chave criada no início, na tela de configurações, ou mesmo adicionar uma nova. Lembre-se de adicionar o conteúdo da chave pública do Jenkins, como uma chave válida para deploy em seu controle de versão.

Com o acesso ao repositório configurado, podemos definir quando nosso build ocorrerá automaticamente, você possui várias opções, eu gosto muito de habilitar tanto  checagem automática a cada hora, quanto a cada push que o repositório receber.
A checagem periódica usa o mesmo padrão da cron, então, é possível também utilizar valores como @hourly, @daily e etc, dependendo do tamanho do seu projeto e de quanto tempo leve o build, seja uma boa idéia chegar num valor que não atrapalhe a equipe aqui, criando filas de builds desnecessários.

<img src="assets/15-trigger.png" class="img img-responsive img-thumbnail" alt="Periodicidade" title="Jenkins - Checagem do repositório">

O próximo bloco é sobre o ambiente, onde você pode limpar sua área de trabalho, habilitar alguns plugins e etc. Gosto de habilitar um plugin chamado **ci-skip**, para atualizações que não requerem um build, como uma atualização do arquivo README do projeto por exemplo.

<img src="assets/16-ambiente.png" class="img img-responsive img-thumbnail" alt="Ambiente" title="Jenkins - Ambiente">

Os próximos blocos são bem semelhantes, porém, no primeiro, você configura todos os passos necessários até que seu projeto seja definido como entregável, o segundo, são os passos a ser executados após o build ser definido como tal. Lembre-se, que cada passo de build depende do sucesso do seu anterior, então, é uma boa prática não juntar todos os passos num bloco só de build.

<img src="assets/17-build.png" class="img img-responsive img-thumbnail" alt="Builds" title="Passos de builds">

Nos próximos passos, vou mostrar como fazer uma configuração básica para projetos em algumas linguagens comuns no mercado.

