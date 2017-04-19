# Portal Aberta

# Etapa 1 - Levantamento das Informações

- Conforme Plano de Implantação anexo a demanda:
  - Ambiente de desenvolvimento externo:  www.dev.nute.ufsc.br
  - Versão do PHP: 7.0.14
  - Banco de dados> MySQL 5.7.16
  - SO Atual: Ubutntu 16.04.1 LTS
  - Informações Adicionais:
    - Apache 2.4.x + módulos:
      - mod_headers
      - mod_deflate
      - mod_setenvif
      - mod_headers
      - mod_filter
      - mod_expires
      - mod_rewrite
      - mod_negotiation
    - PHP 7.0.x + módulos:
      - ctype
      - dom
      - exif
      - fileinfo
      - gd
      - gettext
      - iconv
      - json
      - mbstring
      - mysqli
      - pdo
      - pdo_mysqli
      - phar
      - simplexml
      - tokenizer
      - zip
      - openssl

  - Alterações para cada ambiente:
    - Arquivo .env:
    ``` conf
        APP_ENV=production
        APP_KEY=base64:OefnwLUDAfunD7VyjkHr0wLAG8DIcNOralJ8M+GOPSA=
        APP_DEBUG=false
        APP_DEBUG_SQL=false
        APP_LOG=daily
        APP_LOG_LEVEL=warning
        APP_URL=http://www.aberta.senad.gov.br

        DB_HOST=10.10.28.11
        DB_PORT=3306
        DB_DATABASE=porta_senad_dev
        DB_USERNAME=sisportalsenad
        DB_PASSWORD=mj1234

        BROADCAST_DRIVER=log
        CACHE_DRIVER=file
        SESSION_DRIVER=file
        QUEUE_DRIVER=sync

        REDIS_HOST=127.0.0.1
        REDIS_PASSWORD=null
        REDIS_PORT=6379

        MAIL_DRIVER=smtp
        MAIL_HOST=
        MAIL_PORT=587
        MAIL_USERNAME=
        MAIL_PASSWORD=
        MAIL_ENCRYPTION=tls
        MAIL_FROM_ADDRESS=aberta.senad@mj.gov.br
        MAIL_FROM_NAME="Portal Aberta"

        SESSION_COOKIE=senad_aberta
        SESSION_DOMAIN=www.aberta.senad.gov.br
    ```
    - Executar "php composer.phar install --no-dev" a partir da raiz do projeto
    - Extrair o arquivo "medias.zip" (https://www.dropbox.com/s/v7heijcjkzpzqok/medias.zip?dl=0) em "public/medias/
    - Verificar se o DocumentRoot do Virtual Host esta configurado para  "Build/codigos_fonte/public e reiniciar o apache

## Ações por parte de GCM

### Aguardando Infraestrutura
- ✔ SATI [152598][27-03-2017]Consolidação das informações em repositórios externos @paralyzed(2017-03-27 15:24) @done(2017-03-29 11:56)
![Compartilhamento DropBox](images/2017/03/Evidência - 2017-03-27-151619-MJ-135483.png)
- ✔ SATI[152583][27-03-2017]Levantamento das informações do ambiente de produção @paralyzed(2017-03-27 15:01) @done(2017-03-29 11:56)
- ❄ SATI 153000  para replicação ou criação do ambiente de desenvolvimento @paralyzed(2017-03-29 12:04)

# Etapa 2 - Replicação de ambiente

Será necessário a validação da equipe de infra para execução do PHP 7 e PHP 5 no mesmo ambiente.

- ☐ Criação de Job's Jenkins para execução em ambiente de desenvolvimento
- ☐ Ajustes da aplicação para deploy via Jenkins e teste do ambiente
- ☐ Finalização do Pipeline Jenkins
