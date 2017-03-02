# Redmine 5115
## Problema em Produção do COMP-DRCI - HML X PRD

**Problema:**

> Por gentileza, emitir parecer técnico para o caso referente ao SATI 143553 e o 144529\. Ao subirmos o deploy para produção através do sati 143553 , o sistema gerou o incidente que gerou sati 144529\.

> Foi aberto o sati 144498 para solicitar o log onde foi verificada a falha. Foi necessário implantar o comp_drci do ambiente de homologação para produção. Porém é muito importante verificar a causa raiz do problema pois nos parece que houve falta de atualização durante o processo de integração contínua, ou por falha de comunicação o falta de passagem do código fonte da fábrica para o nosso fork. Encontramos este merge request com bastantes mudanças que pode ser usado como origem de estudo: <http://git.mj.gov.br/CGTI-DIPROS-LEGADO/COMP-DRCI/merge_requests/33/diffs>

## Análise da Demanda

## 1\. Análise dos SATIS Informados

### 1.1\. Informações das Solicitações:

SATI   | Data Abertura       | Data de Resolvido   | Solicitante                       | Executor                    | Solicitação
------ | ------------------- | ------------------- | --------------------------------- | --------------------------- | -------------------------------------------------
143553 | 01/02/2017 10:52:04 | 13/02/2017 11:47:53 | Emanuel da S. Nascimento, Walbert | da Silva Ribeiro, Alan      | Deploy de aplicação e alteração de banco de dados
144498 | 07/02/2017 10:18:44 | 07/02/2017 10:30:36 | Aparecido Santana Rosa, Gabriel   | Sousa Figueredo, Nayara     | Solicitação de logs
144529 | 07/02/2017 11:35:44 | 14/02/2017 11:57:35 | Emanuel da S. Nascimento, Walbert | Alves Romão Neto, Francisco | Deploy de componente

#### 1.1.1\. Entendimento da Solicitação:

- SATI 143553: Solicitação de Deploy da aplicação em ambiente de Produção com execução de Alteração em banco de dados:

  - DocumentoDiligencia.sql : Alteração da Tabela DocumentoDiligencia para adição de 2 campos(TipoDocumentoSei e DestinatarioRemetente)
  - 01-InsertPais.sql: Insert do País 'Curaçao'

- SATI 144529: Solicitação de Deploy do Componente MJCompDRCI.jar no diretório do Servidor.

#### 1.1.2\. Análise das solicitações:

- SATI 143553: O prenchimento de informações se encontram fora do padrão. No mesmo SATI existe a solicitação de deploy em produção e alteração de banco de dados, mas não está claro o deploy a ser feito em produção, apenas o pedido para preenchimento da configuração do job no java.jenkins.mj.gov.br

- SATI 144498: Solicitação de log de produção sem especificação do período necessário para análise

- SATI 144529: O preenchimento de informações se encontram fora do padrão. No SATI é requerido que se faça o deploy do componente MJCompDRCI.jar em diretório específico(/opt/jboss-4.2.3.GA/server/sgdrci/deploy/mj/03comp/). Essa solicitação no resumo aponta o ambiente de Produção e ao indicar o diretório informa os ambientes de homologação e produção

#### 1.1.3\. Análise das soluções:

- SATI 143553: Existe a evidência de que os scripts foram executados com sucesso e no anexo existe a evidência que sustenta tal execução. Não há evidência da execução de deploy da aplicação e nem relacionamento com outros SATIS

- SATI 144498: Disponibilizado o log dos dois servidores de aplicação.

- SATI 144529: Existe a evidência de que o arquivo solicitado para o componente foi realizado deploy nas máquinas de homologação e produção e no anexo existe a evidência que sustenta tal execução. Não há relacionamento com outros SATIS

### 1.2\. Análise da atualização de código via git:

Para atualização foram realizados merges para acompanhamento do código via Pipeline Jenkins:

Merge | Data Pedido      | Data Realização  | Origem           | Destino | Status    | Solicitante                      | Executor
----- | ---------------- | ---------------- | ---------------- | ------- | --------- | -------------------------------- | --------------------------------
150   | 11/01/2017 17:08 | 11/01/2017 20:40 | Stefanini/master | GQUAL   | Realizado | Gabriel Aparecido Santana Rosa   | Walbert Emanuel da S. Nascimento
152   | 17/01/2017 21:40 | 17/01/2017 21:41 | GQUAL            | master  | Realizado | Walbert Emanuel da S. Nascimento | Walbert Emanuel da S. Nascimento
153   | 31/01/2017 16:32 | 31/01/2017 18:35 | master           | stable  | Realizado | Walbert Emanuel da S. Nascimento | Allan Carlos Ramalho

### 1.3\. Análise do deploy via Jenkins:

- Deploy Via Pipeline Jenkins: Conforme imagem abaixo, o pipeline que foi executado no dia 06/02/2017 19:28:56 realizando o deploy em ambiente de desenvolvimento eliminou o pipeline que executou o deploy em produção:

  ![](http://projetoscgti.mj.gov.br/system/rich/rich_files/rich_files/000/000/437/original/Evid%C3%AAncia%20131%20-20170223-1826.png)

Com base nessa evidência segue a análise de cada um dos deploy executados manualmente dentro do padrão estabelecido, não inclui o deploy em desenvolvimento por já ter sido excluído o job que iniciou o novo pipeline:

Job # | Ambiente    | Data Execução       | Responsável | Status  | Revison Git                              | Branch
----- | ----------- | ------------------- | ----------- | ------- | ---------------------------------------- | -----------
18    | Teste       | 25/01/2017 17:50:09 | Pipeline 23 | Sucesso | 46dd7b6b445396b0465dab30eafb55db0cc103b8 | CGTI/GQUAL
10    | Homologação | 25/01/2017 17:53:11 | Pipeline 23 | Sucesso | 784ef0791a9e9ab4a3afd8bd99644b8373402f0a | CGTI/master
9     | Produção    | 06/02/2017 18:55:37 | Pipeline 23 | Sucesso | 34d6d1a1d3e89f8f64ef56561d5d4027d8e002a8 | CGTI/stable

De acordo com a imagem abaixo o deploy em produção, realizado em 06/02/2017, contém as alterações realziadas em teste e homologação, de acordo com o commit git expresso na tabela da anterior.

![](http://projetoscgti.mj.gov.br/system/rich/rich_files/rich_files/000/000/439/original/Evid%C3%AAncia%20133%20-20170223-1906.png)

# Conclusão

De acordo com as evidências o deploy da aplicação em produção aconteceu em 06/02/2017 as 18:55:37 e foi executado pelo Job 09 do Jenkins levando as alterações até o commit `34d6d1a`. Essa data se encontra no período de atendimento do SATI 143553, onde a configuração, mesmo não evidenciada, foi efetiva conforme log na aplicação Jenkins(<http://java.jenkins.mj.gov.br/view/SGDRCI-Legado/job/drci-web-deploy-prd/9/console>):

![](http://projetoscgti.mj.gov.br/system/rich/rich_files/rich_files/000/000/441/original/Evid%C3%AAncia%20135%20-20170223-1919.png)

Portanto o Deploy da aplicação WEB(WAR) ocorreu conforme o esperado e definido nos padrões de GCM, mesmo como desencontro de informações nos SATIs. Visto que o SATI 144529 que resolveu o problema, trata do deploy do componente MJCompDRCI.jar e que este componente não possui job Jenkins, a solução foi realizada por meio de um deploy manual, ou seja, não foi criado o pipeline para deploy do componente e não houve solicitação para criação do ambiente ou job jenkins, nem de aplicação e nem de componente. No momento será iniciada o redmine 5111 que trata da criação dos jbos e adequação do componente citado.
