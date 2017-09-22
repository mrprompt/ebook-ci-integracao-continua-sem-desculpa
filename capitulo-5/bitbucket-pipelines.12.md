### <a name="pros-e-contras"></a> Prós & Contras

A favor do Pipelines, tem muita coisa, apesar de ser uma ferramenta nova e ainda em sua versão beta, ela cumpre o que promete e reconhece [suas limitações](https://confluence.atlassian.com/bitbucket/limitations-of-bitbucket-pipelines-827106051.html).

Os builds rodam muito rápido e fazer parte do Bitbucket, e não como uma ferramenta a parte, conta muitos pontos.

Rodar sobre o docker também é muito bom, porque permite um controle maior de todo o ambiente, sem a necessidade de ficar dando manutenção em servidores.

Como não podia faltar em nenhuma ferramenta de CI, existem [várias integrações](https://confluence.atlassian.com/bitbucket/bitbucket-pipelines-integrations-826868162.html) prontas para utilizar, como Deploy para S3, Heroku, Azure e etc.

Contra, por enquanto, é que o Pipelines ainda é um pouco problemático com o arquivo de configuração - talvez isso seja problema do próprio yaml - mas as vezes incomoda e fica difícil de debugar sem sujar o repositório com vários commits. Talvez um validador online facilitasse as coisas.
