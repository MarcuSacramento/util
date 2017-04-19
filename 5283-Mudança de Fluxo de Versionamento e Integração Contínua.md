# Mudança de Fluxo de Versionamento

## Proteção de Branches no GitLab

- Alterados os branches GQUAL, master e stable para protegê-los de push, permitindo apenas o branch GQUAL para que a equipe de desenvolvedores possa realizar os merges na mesma.

> Dessa forma será possível o desenvolvedor realizar o merge para a CGTI realizando a entrega.

```sql
-- Script de banco de dados para remover as proteções de todos os branches dos projetos da CGTI e CGTI-DIPROS-LEGADO
SELECT 'DELETE from public.protected_branches where project_id = '||id||';'
FROM projects p
WHERE p.namespace_id IN
(SELECT id
FROM namespaces
WHERE name in ('CGTI','CGTI-DIPROS-LEGADO'));

-- Script de banco de dados para inserir as proteções de todos os branches dos projetos da CGTI e CGTI-DIPROS-LEGADO
SELECT 'INSERT INTO public.protected_branches (id,project_id,name,created_at,updated_at,developers_can_push) VALUES (nextval(''protected_branches_id_seq''::regclass),'||id||',''GQUAL'',current_timestamp,current_timestamp,TRUE);'
FROM projects p
WHERE p.namespace_id IN
    (SELECT id
     FROM namespaces
     WHERE name in ('CGTI','CGTI-DIPROS-LEGADO'));


-- Exemplo de delete gerado:
DELETE
FROM public.protected_branches
WHERE project_id = 53;

-- Exemplo de insert Gerado
INSERT INTO public.protected_branches (id,project_id,name,created_at,updated_at,developers_can_push)
VALUES (nextval('protected_branches_id_seq'::regclass),
        53,
        'GQUAL',
        CURRENT_TIMESTAMP,
        CURRENT_TIMESTAMP,
        TRUE);
```

## Alteração dos Jobs Jenkins

- Adicionar a permissão de aprovação dos Jobs Jenkins **_db-changes_** no pipeline **Teste** para a equipe de desenvolvedores;
- Necessário atualizar grupo para desenvolvedores:

  - Grupo Atual:

    - Alexandre Martins da Silva <alexandre.martins.terceirizado@mj.gov.br>;
    - Deividy Rodrigues Pinheiro <deividy.pinheiro.terceirizado@mj.gov.br>;
    - Diego Francisco Nogueira <diego.nogueira.terceirizado@mj.gov.br>;
    - Fernando Braz Martins Costa <fernando.braz.terceirizado@mj.gov.br>;
    - Francisco Antonio Zacariotti Filho <francisco.zacariotti.terceirizado@mj.gov.br>;
    - Gabriel Aparecido Santana Rosa <gabriel.santana.terceirizado@mj.gov.br>;
    - Guilherme Pereira de Jesus <guilherme.jesus.terceirizado@mj.gov.br>;
    - Lincoln Mileno Alves <lincoln.alves.terceirizado@mj.gov.br>;
    - Roberio Cardoso Fernandes <roberio.fernandes.terceirizado@mj.gov.br>;
    - Ronald Correa Calazans Barbosa <ronald.barbosa.terceirizado@mj.gov.br>;
    - Thiago Sousa da Costa <thiago.scosta.terceirizado@mj.gov.br>;
    - William César Pereira Barreto <william.barreto.terceirizado@mj.gov.br>;

  - Adicionar:

    - Márcio Muzi de Medeiros <marcio.muzi.terceirizado@mj.gov.br>;
    - Jonathan Pereira Cabral <jonathan.cabral.terceirizado@mj.gov.br>;

## Documentação

- Geração de Documento markdown para utilização por pate dos executores no Java Jenkins e no GitLab
