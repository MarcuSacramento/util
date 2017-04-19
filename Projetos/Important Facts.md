![](http://g.gongshw.com/g?
digraph DEV {
  label="IIS";
  splines=true;
  overlap=prism;
  compound=true;
  labelloc="t";
  rankdir=LR;
  desenvolvimentoapp -> testeapp -> homologacaoapp -> producaoapp [style=invis]
  a [shape=point label="Usuario"]
  a -> DNSMaster
  DNSMaster -> proxyMaster [ltail=cluster_dns,lhead=cluster_proxy]
  proxyMaster -> balanceadorMaster [ltail=cluster_proxy,lhead=cluster_balanceador]
  balanceadorSlave -> producaoapp [ltail=cluster_balanceador,lhead=cluster_producao_app]
    {
    sametail=true
    proxySlave -> desenvolvimentoapp [ltail=cluster_proxy,lhead=cluster_dsv_app]
    proxySlave -> testeapp [ltail=cluster_proxy,lhead=cluster_teste_app]
    proxySlave -> homologacaoapp [ltail=cluster_proxy,lhead=cluster_homologacao_app]
    }
  subgraph cluster_apresentacao {
    label="Apresentacao"
    labelloc="t"
    compound=true
    color=bisque
    fillcolor=bisque
    style=filled
    subgraph cluster_dns {
      label = "DNS"
      node [style=filled];
      color=blue;
      DNSMaster;
      DNSMaster [shape=box3d fillcolor=white style=filled label=<<table border="0" cellpadding="2" cellspacing="0" cellborder="0">
        <tr><td align="center" port="i1">Master</td></tr>
        <tr><td align="center" port="i2">srdflxapp017</td></tr>
        <tr><td align="right" port="i3">10.10.20.17</td></tr>
        </table>>];
    }
    subgraph cluster_proxy {
      label = "Proxy";
      node [style=filled];
      color=blue;
        proxyMaster proxySlave;
      proxyMaster [shape=box3d fillcolor=white style=filled label=<<table border="0" cellpadding="2" cellspacing="0" cellborder="0">
        <tr><td align="center" port="i1">Master</td></tr>
        <tr><td align="center" port="i2">srdflxapp017</td></tr>
        <tr><td align="right" port="i3">10.10.20.17</td></tr>
        </table>>];  
      proxySlave [shape=box3d fillcolor=white style=filled label=<<table border="0" cellpadding="2" cellspacing="0" cellborder="0">
        <tr><td align="center" port="i1">Slave</td></tr>
        <tr><td align="center" port="i2">srdflxapp018</td></tr>
        <tr><td align="right" port="i3">10.10.20.18</td></tr>
        </table>>];
    }
    subgraph cluster_balanceador {
      label = "Balanceadores";
      rankdir=LR;
      node [style=filled];
      color=blue;
        balanceadorMaster balanceadorSlave;
      balanceadorMaster [shape=box3d fillcolor=white style=filled label=<<table border="0" cellpadding="2" cellspacing="0" cellborder="0">
        <tr><td align="center" port="i1">Master</td></tr>
        <tr><td align="center" port="i2">srdflxapp017</td></tr>
        <tr><td align="right" port="i3">10.10.20.17</td></tr>
        </table>>];  
      balanceadorSlave [shape=box3d fillcolor=white style=filled label=<<table border="0" cellpadding="2" cellspacing="0" cellborder="0">
        <tr><td align="center" port="i1">Slave</td></tr>
        <tr><td align="center" port="i2">srdflxapp018</td></tr>
        <tr><td align="right" port="i3">10.10.20.18</td></tr>
        </table>>];
    }
  }
  subgraph cluster_aplicacao {
    label="Aplicacao";
    labelloc="t";
    compound=true;
    color=bisque;
    fillcolor=gray;
    style=filled;
    newrank=true;
    rankdir=LR;  
    subgraph cluster_dsv_app {
      label = "Desenvolvimento";
      node [style=filled];
      color=blue;
        desenvolvimentoapp;
      desenvolvimentoapp [shape=box3d fillcolor=white style=filled label=<<table border="0" cellpadding="2" cellspacing="0" cellborder="0">
        <tr><td align="center" port="i2">srdflxapp017</td></tr>
        <tr><td align="right" port="i3">10.10.20.17</td></tr>
        </table>>];
    }
    subgraph cluster_teste_app {
      label = "Teste";
      node [style=filled];
      color=blue;
      testeapp;
      testeapp [shape=box3d fillcolor=white style=filled label=<<table border="0" cellpadding="2" cellspacing="0" cellborder="0">
        <tr><td align="center" port="i2">srdflxapp017</td></tr>
        <tr><td align="right" port="i3">10.10.20.17</td></tr>
        </table>>];  
    }
      subgraph cluster_homologacao_app {
      label = "Homologacao";
      node [style=filled];
      color=blue;
      homologacaoapp;
      homologacaoapp [shape=box3d fillcolor=white style=filled label=<<table border="0" cellpadding="2" cellspacing="0" cellborder="0">
        <tr><td align="center" port="i2">srdflxapp017</td></tr>
        <tr><td align="right" port="i3">10.10.20.17</td></tr>
        </table>>];  
    }
      subgraph cluster_producao_app {
      label = "Producao";
      node [style=filled];
      color=blue;
      producaoapp;
      producaoapp [shape=box3d fillcolor=white style=filled label=<<table border="0" cellpadding="2" cellspacing="0" cellborder="0">
        <tr><td align="center" port="i2">srdflxapp017</td></tr>
        <tr><td align="right" port="i3">10.10.20.17</td></tr>
        </table>>];  
    }
  }
})

# Banco de Dados MJ

## Desenvolvimento

Banco                    | Owner                       | Tecnologia
------------------------ | --------------------------- | ----------
alfresco                 | sisalfresco                 | PostgreSQL
atlas                    | sisatlas                    | PostgreSQL
atlas                    | sisatlas                    | PostgreSQL
cadupl                   | siscadupl                   | PostgreSQL
caduplcapgemini          | siscaduplcapgemini          | PostgreSQL
caduplmodelodados        | siscaduplmodelodados        | PostgreSQL
caduplweb                | siscaduplweb                | PostgreSQL
carrosweb                | siscarrosweb                | PostgreSQL
cas                      | siscas                      | PostgreSQL
cgti                     | siscgti                     | PostgreSQL
citgrp                   | siscitgrp                   | PostgreSQL
citsmart                 | siscitsmart                 | PostgreSQL
civis                    | siscivis                    | PostgreSQL
conareprod               | sisconareprod               | PostgreSQL
conareweb                | sisconareweb                | PostgreSQL
corpmj                   | siscorpmj                   | PostgreSQL
corpmj030snapshot        | siscorpmj030snapshot        | PostgreSQL
corpmjrest               | siscorpmjrest               | PostgreSQL
drcizaca                 | sisdrcizaca                 | PostgreSQL
fnsp                     | sisfnsp                     | PostgreSQL
gfunad                   | sisgfunad                   | PostgreSQL
gfunadtu                 | sisgfunadtu                 | PostgreSQL
gfunadweb                | sisgfunadweb                | PostgreSQL
ligacoes                 | sisligacoes                 | PostgreSQL
mcai                     | sismcai                     | PostgreSQL
mcaitu                   | sismcaitu                   | PostgreSQL
mciweb                   | sismciweb                   | PostgreSQL
monitoramento            | sismonitoramento            | PostgreSQL
noosfero                 | sisnoosfero                 | PostgreSQL
ojs                      | sisojs                      | PostgreSQL
segurancacapgemini       | sissegurancacapgemini       | PostgreSQL
sgdrci                   | sissgdrci                   | PostgreSQL
sgdrcidevssa             | sissgdrcidevssa             | PostgreSQL
sgdrcifabrica            | sissgdrcifabrica            | PostgreSQL
sgdrciweb                | sissgdrciweb                | PostgreSQL
side                     | sisside                     | PostgreSQL
sidedevantigo            | sissidedevantigo            | PostgreSQL
sidedevtestescript       | sissidedevtestescript       | PostgreSQL
sidetu                   | sissidetu                   | PostgreSQL
sideweb                  | sissideweb                  | PostgreSQL
sidewebold               | sissidewebold               | PostgreSQL
sigenroo                 | sissigenroo                 | PostgreSQL
sinape                   | sissinape                   | PostgreSQL
sinapeweb                | sissinapeweb                | PostgreSQL
sislegis                 | sissislegis                 | PostgreSQL
storagemjrest            | sisstoragemjrest            | PostgreSQL
storagemjtu              | sisstoragemjtu              | PostgreSQL
storagemjweb             | sisstoragemjweb             | PostgreSQL
svcppdev                 | sissvcppdev                 | PostgreSQL
svcppweb                 | sissvcppweb                 | PostgreSQL
Anistia                  | sisanistia                  | SQL Server
Asi                      | sisasi                      | SQL Server
cnpjbrasil               | siscnpjbrasil               | SQL Server
controlevisitantes       | syscontrolevisitantes       | SQL Server
dbaprdjustica            | sisdbaprdjustica            | SQL Server
dbsdrci                  | dbsdrci                     | SQL Server
desarma                  | sisdesarma                  | SQL Server
Justiça                  | sisjustica                  | SQL Server
Mj                       | sismj                       | SQL Server
mjcorporativo            | sismjcorporativo            | SQL Server
mjcorporativo_prod       | sismjcorporativo_prod       | SQL Server
pronasci                 | sispronasci                 | SQL Server
repositoriojboss         | sisrepositoriojboss         | SQL Server
repositoriojbosssocrates | sisrepositoriojbosssocrates | SQL Server
sindecnacionalnovo       | sissindecnacionalnovo       | SQL Server
testeaudit               | sistesteaudit               | SQL Server
unicgsis                 | sisunicgsis                 | SQL Server

## Teste

Banco                    | Owner                       | Tecnologia
------------------------ | --------------------------- | ----------
atlas                    | sisatlas                    | PostgreSQL
caduplweb                | siscaduplweb                | PostgreSQL
carrosweb                | siscarrosweb                | PostgreSQL
cas                      | siscas                      | PostgreSQL
cgti                     | siscgti                     | PostgreSQL
citgrp                   | siscitgrp                   | PostgreSQL
citsmart                 | siscitsmart                 | PostgreSQL
civis                    | siscivis                    | PostgreSQL
conareweb                | sisconareweb                | PostgreSQL
corpmjrest               | siscorpmjrest               | PostgreSQL
gfunadweb                | sisgfunadweb                | PostgreSQL
mciweb                   | sismciweb                   | PostgreSQL
sgdrciweb                | sissgdrciweb                | PostgreSQL
sideweb                  | sissideweb                  | PostgreSQL
sigenroo                 | sissigenroo                 | PostgreSQL
sinapeweb                | sissinapeweb                | PostgreSQL
storagemjrest            | sisstoragemjrest            | PostgreSQL
svcppweb                 | sissvcppweb                 | PostgreSQL
testesg                  | sistestesg                  | PostgreSQL
Anistia                  | sisanistia                  | SQL Server
Asi                      | sisasi                      | SQL Server
cnpjbrasil               | siscnpjbrasil               | SQL Server
controlevisitantes       | syscontrolevisitantes       | SQL Server
dbaprdjustica            | sisdbaprdjustica            | SQL Server
dbsdrci                  | dbsdrci                     | SQL Server
desarma                  | sisdesarma                  | SQL Server
Justiça                  | sisjustica                  | SQL Server
Mj                       | sismj                       | SQL Server
mjcorporativo            | sismjcorporativo            | SQL Server
mjcorporativo_prod       | sismjcorporativo_prod       | SQL Server
pronasci                 | sispronasci                 | SQL Server
repositoriojboss         | sisrepositoriojboss         | SQL Server
repositoriojbosssocrates | sisrepositoriojbosssocrates | SQL Server
sindecnacionalnovo       | sissindecnacionalnovo       | SQL Server
testeaudit               | sistesteaudit               | SQL Server
unicgsis                 | sisunicgsis                 | SQL Server

## Homologação

Banco                    | Owner                       | Tecnologia
------------------------ | --------------------------- | ----------
Anistia                  | sisanistia                  | SQL Server
Asi                      | sisasi                      | SQL Server
cnpjbrasil               | siscnpjbrasil               | SQL Server
dbaprdjustica            | sisdbaprdjustica            | SQL Server
desarma                  | sisdesarma                  | SQL Server
Justiça                  | sisjustica                  | SQL Server
Mj                       | sismj                       | SQL Server
mjcorporativo            | sismjcorporativo            | SQL Server
mjcorporativo_prod       | sismjcorporativo_prod       | SQL Server
pronasci                 | sispronasci                 | SQL Server
repositoriojboss         | sisrepositoriojboss         | SQL Server
repositoriojbosssocrates | sisrepositoriojbosssocrates | SQL Server
sindecnacionalnovo       | sissindecnacionalnovo       | SQL Server
testeaudit               | sistesteaudit               | SQL Server
unicgsis                 | sisunicgsis                 | SQL Server
controlevisitantes       | syscontrolevisitantes       | SQL Server
dbsdrci                  | dbsdrci                     | SQL Server

[comment]: http://www.graphviz.org/content/attrs
