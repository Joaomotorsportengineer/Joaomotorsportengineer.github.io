---
title: Projeto do modelo de dados
nav_order: 4
---

O modelo de dados foi projetado de forma relacional, com uso de chaves primárias (PK) e chaves estrangeiras (FK) para garantir integridade referencial.
O fluxograma completo do modelo encontra-se documentado na [ferramenta Miro](https://miro.com/welcomeonboard/Yi9yc0U0ZFFRTENBSnFBYTZ1Y2cwb3NPVWNnNFQ0Z2l5VkpEMXYyU3NseFptdzdKcndWZ1h5SnhYTFNLOGF0TWV4SDJrWGxxMVUyTnVUZW5OeW05dTdXL21YNWRZRHlDN1FSa2RZK1haQkJYaS9CWkNKZWpnbHo4UmhCa2ExKzZQdGo1ZEV3bUdPQWRZUHQzSGl6V2NBPT0hdjE=?share_link_id=848430377304).

---

## Usuario

| Campo        | Descrição |
|--------------|-----------|
| id_usuario   | PK        |
| nome         | Nome do usuário |
| email        | E-mail (login) |
| senha_hash   | Hash da senha |
| papel        | Admin, Gerente, Coordenador, Pesquisador, Logista, Batch |
| ativo        | Indica se o usuário está ativo |
| data_criacao | Data/hora de criação do registro |

## Regiao

| Campo      | Descrição |
|------------|-----------|
| id_regiao  | PK        |
| nome       | Nome da região |

## Loja

| Campo        | Descrição |
|--------------|-----------|
| id_loja      | PK        |
| nome         | Nome da loja |
| cnpj         | CNPJ da loja |
| endereco     | Endereço |
| id_regiao    | FK → Regiao |
| status       | PENDENTE, APROVADA, REPROVADA |
| data_cadastro| Data/hora do cadastro |

## Marca

| Campo     | Descrição |
|-----------|-----------|
| id_marca  | PK        |
| nome      | Nome da marca |

## Modelo

| Campo      | Descrição |
|------------|-----------|
| id_modelo  | PK        |
| nome       | Nome do modelo |
| id_marca   | FK → Marca |

## Pesquisa

| Campo         | Descrição        |
|---------------|------------------|
| id_pesquisa   | PK               |
| id_loja       | FK → Loja        |
| id_pesquisador| FK → Usuario     |
| data_pesquisa | Data da pesquisa |

## Veículo pesquisado

| Campo              | Descrição |
|--------------------|-----------|
| id_veiculo_pesquisado | PK    |
| id_pesquisa        | FK → Pesquisa |
| id_modelo          | FK → Modelo   |
| ano_modelo         | Ano modelo do veículo |
| ano_fabricacao     | Ano de fabricação |
| preco              | Preço pesquisado |
| opcionais          | Opcionais do veículo |

## Cotacao

| Campo         | Descrição |
|---------------|-----------|
| id_cotacao    | PK        |
| id_modelo     | FK → Modelo |
| preco_medio   | Preço médio calculado |
| data_referencia | Mês/ano de referência |

## Consulta

| Campo         | Descrição |
|---------------|-----------|
| id_consulta   | PK        |
| id_modelo     | FK → Modelo |
| filtros_usados| Filtros utilizados na consulta (ex.: marca, ano, mês) |
| data_consulta | Data/hora da consulta |

## Aprovacao

| Campo          | Descrição     |
|----------------|---------------|
| id_aprovacao   | PK            |
| id_loja        | FK → Loja     |
| id_coordenador | FK → Usuario  |
| status         | Status da aprovação (ex.: aprovada, reprovada) |
| data_aprovacao | Data/hora da aprovação |
| observacao     | Observação do coordenador |

## Batch_Resultados

| Campo            | Descrição |
|------------------|-----------|
| id_batch         | PK        |
| mes_ano          | Mês/ano de referência (ex.: 2025-01) |
| id_modelo        | FK → Modelo |
| preco_medio      | Média mensal de preços |
| data_processamento | Data/hora do processamento batch |

---

## Integração FIPE (opcional / futuro)

Se no futuro o sistema armazenar **cache** de preços FIPE ou **referências** utilizadas, pode ser criada uma tabela dedicada (ex.: `fipe_referencia` ou `cache_fipe`) com campos como: referência (mês/ano ou código), tipo de veículo, marca, modelo, ano, valor, data da consulta. Enquanto a consulta usar apenas a API em tempo real e gravar somente na tabela **Consulta**, o modelo atual basta e não é obrigatório alterar o modelo de dados.
