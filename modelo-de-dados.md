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
| nome         |           |
| email        |           |
| senha_hash   |           |
| papel        | Admin, Gerente, Coordenador, Pesquisador, Logista, Batch |
| ativo        |           |
| data_criacao |           |

## Regiao

| Campo      | Descrição |
|------------|-----------|
| id_regiao  | PK        |
| nome       |           |

## Loja

| Campo        | Descrição |
|--------------|-----------|
| id_loja      | PK        |
| nome         |           |
| cnpj         |           |
| endereco     |           |
| id_regiao    | FK        |
| status       | PENDENTE, APROVADA, REPROVADA |
| data_cadastro|           |

## Marca

| Campo     | Descrição |
|-----------|-----------|
| id_marca  | PK        |
| nome      |           |

## Modelo

| Campo      | Descrição |
|------------|-----------|
| id_modelo  | PK        |
| nome       |           |
| id_marca   | FK        |

## Pesquisa

| Campo         | Descrição        |
|---------------|------------------|
| id_pesquisa   | PK               |
| id_loja       | FK               |
| id_pesquisador| FK → Usuario     |
| data_pesquisa |                  |

## Veículo pesquisado

| Campo              | Descrição |
|--------------------|-----------|
| id_veiculo_pesquisado | PK    |
| id_pesquisa        | FK        |
| id_modelo          | FK        |
| ano_modelo         |           |
| ano_fabricacao     |           |
| preco              |           |
| opcionais          |           |

## Cotacao

| Campo         | Descrição |
|---------------|-----------|
| id_cotacao    | PK        |
| id_modelo     | FK        |
| preco_medio   |           |
| data_referencia |         |

## Consulta

| Campo         | Descrição |
|---------------|-----------|
| id_consulta   | PK        |
| id_modelo     | FK        |
| filtros_usados|           |
| data_consulta |           |

## Aprovacao

| Campo          | Descrição     |
|----------------|---------------|
| id_aprovacao   | PK            |
| id_loja        | FK            |
| id_coordenador | FK → Usuario  |
| status         |               |
| data_aprovacao |               |
| observacao     |               |

## Batch_Resultados

| Campo            | Descrição |
|------------------|-----------|
| id_batch         | PK        |
| mes_ano          |           |
| id_modelo        | FK        |
| preco_medio      |           |
| data_processamento |         |
