---
title: Detalhamento do conteúdo funcional
nav_order: 2
---

Este documento descreve o planejamento do sistema de cotação de veículos.

O projeto foi desenvolvido utilizando a metodologia ágil **Scrum**, com gerenciamento das atividades realizado na ferramenta **Jira**, por meio da técnica de Épicos e User Stories.

O planejamento, priorização do backlog e acompanhamento da evolução do desenvolvimento encontram-se disponíveis no [link do planning na plataforma Atlassian](https://unifei-team-zb4wfmoq.atlassian.net/jira/software/projects/MS3/boards/67/backlog?epics=visible).

---

## Épico / História: Consulta pública de preços com Tabela FIPE

**Descrição:** Permitir que usuários não autenticados consultem preços de veículos com base na Tabela FIPE (referência mês/ano, tipo, marca, modelo, ano).

**Critérios de aceite (ex.):**

- Usuário não logado escolhe **mês/ano de referência**, **tipo de veículo** (carros, motos, caminhões), **marca**, **modelo** e **ano** e visualiza o valor FIPE retornado pela API.
- Sistema registra a consulta na tabela **Consulta** quando a persistência estiver implementada.
- Interface alinhada ao fluxo de referência da Tabela FIPE: seleção de referência → tipo → marca → modelo → ano → pesquisar.

**Nota:** Implementado com integração à API [Parallelum FIPE](https://deividfortuna.github.io/fipe/v2/). Dados internos (Cotacao/Batch_Resultados) a integrar conforme backlog.
