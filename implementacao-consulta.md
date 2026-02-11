---
title: Implementação da funcionalidade de consulta pelo usuário
nav_order: 7
---

A funcionalidade de consulta permite que **usuários não autenticados** realizem pesquisas de cotação de veículos.

---

## Fluxo da funcionalidade

1. O usuário acessa a interface desenvolvida em **Streamlit**.
2. Seleciona os filtros desejados:
   - Marca
   - Modelo
   - Ano-modelo
   - Ano de fabricação
   - Mês de referência
3. O **frontend** envia os filtros selecionados para a camada de **backend**.
4. O backend executa uma consulta SQL na tabela **Cotacao** e/ou **Batch_Resultados**, retornando o **preço médio** correspondente ao mês de referência.
5. O resultado é exibido na interface para o usuário.
6. **Em paralelo**, o sistema registra a consulta na tabela **Consulta**, armazenando:
   - Modelo consultado
   - Filtros utilizados
   - Data e hora da consulta

---

## Componentes envolvidos

- **Serviços:** CotacaoService (e/ou BatchService) para obter o preço médio.
- **Repositórios:** CotacaoRepository, ConsultaRepository (e eventualmente BatchResultadosRepository).
- **Tabelas:** [Cotacao](modelo-de-dados.md#cotacao), [Batch_Resultados](modelo-de-dados.md#batch_resultados), [Consulta](modelo-de-dados.md#consulta).

Detalhes em [Modelo de componentes](modelo-de-componentes.md).

---

## Objetivo técnico

- Permitir **acesso público** às cotações (sem necessidade de login).
- Coletar **dados de uso** para análise estatística e tomada de decisão futura.
- Garantir **desempenho** e **simplicidade** na experiência do usuário.
