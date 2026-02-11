---
title: Definição de casos de teste, implementação e testes automatizados
nav_order: 8
---

A estrutura dos testes (pasta `tests/`, Pytest) está descrita no [Technical Design](technical-design.md).

## Testes de integração

- Verificação da **comunicação entre backend e banco de dados**.
- Testes de **consultas SQL com filtros**.
- Verificação da **persistência correta** dos dados nas tabelas.

---

## Testes automatizados

- **Execução automática** dos testes durante o desenvolvimento.
- Garantia de que **novas alterações não quebrem funcionalidades existentes** (regressão).

### Exemplos de casos de teste

| Cenário | Objetivo |
|---------|----------|
| Consulta com filtros válidos (marca, modelo, mês) | Retornar o preço médio correspondente. |
| Realização de uma consulta pelo usuário | Registrar um novo registro na tabela **Consulta** (modelo, filtros, data). |
| Cadastro de loja com status PENDENTE | Persistir corretamente; Coordenador pode aprovar ou reprovar. |
| Persistência em Cotacao / Batch_Resultados | Garantir integridade dos dados e relacionamentos (FK). |

---

## Benefícios dos testes

- Maior **confiabilidade** do sistema.
- **Redução de falhas** em produção.
- **Facilidade de manutenção** e evolução do código.
