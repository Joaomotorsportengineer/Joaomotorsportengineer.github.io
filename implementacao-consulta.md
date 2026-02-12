---
title: Implementação da funcionalidade de consulta pelo usuário
nav_order: 7
---

A funcionalidade de consulta permite que **usuários não autenticados** realizem pesquisas de cotação de veículos.

---

## Fonte dos dados na consulta

Atualmente a consulta pública utiliza a **API externa da Tabela FIPE** ([Parallelum v2](https://deividfortuna.github.io/fipe/v2/)), com seleção de **mês/ano de referência**. O usuário escolhe a referência (mês/ano), o tipo de veículo (carros, motos, caminhões), marca, modelo e ano-modelo; o backend chama o **serviço de integração FIPE** e exibe o valor retornado.

Quando houver banco próprio com dados internos, o backend poderá consultar **Cotacao** e/ou **Batch_Resultados** além da FIPE (ou em substituição), conforme a regra de negócio definida (ex.: “sempre FIPE”, “FIPE + média interna” ou “prioridade dados internos”).

**Observação:** a API pública FIPE costuma retornar marcas e modelos apenas para **referências recentes** (ex.: últimos meses). Histórico maior pode exigir serviço pago (ex.: [fipe.online](https://fipe.online)).

---

## Fluxo da funcionalidade

1. O usuário acessa a interface desenvolvida em **Streamlit**.
2. Seleciona, em ordem:
   - **Mês/ano de referência**
   - **Tipo** de veículo (carros, motos, caminhões)
   - **Marca** → **Modelo** → **Ano modelo**
3. Clica em **Pesquisar**.
4. O **frontend** envia os filtros para o **backend**.
5. O backend chama o **FipeService** (integração API FIPE) e/ou, no futuro, **CotacaoService** / **BatchService** (dados internos em Cotacao/Batch_Resultados).
6. O **preço** (valor FIPE e/ou preço médio interno) é exibido na interface.
7. **Em paralelo**, quando a persistência estiver implementada, o sistema registra a consulta na tabela **Consulta** (modelo consultado, filtros utilizados, data e hora).

---

## Componentes envolvidos

- **Serviços:** **FipeService** (integração API FIPE — em uso); CotacaoService e/ou BatchService (dados internos, quando houver banco).
- **Repositórios:** ConsultaRepository (para registrar a consulta quando a persistência estiver ativa); CotacaoRepository, BatchResultadosRepository (futuro).
- **Tabelas:** [Consulta](modelo-de-dados.md#consulta) (registro da consulta); [Cotacao](modelo-de-dados.md#cotacao), [Batch_Resultados](modelo-de-dados.md#batch_resultados) (dados internos, futuro).

Detalhes em [Modelo de componentes](modelo-de-componentes.md).

---

## Objetivo técnico

- Permitir **acesso público** às cotações (sem necessidade de login).
- Coletar **dados de uso** para análise estatística e tomada de decisão futura.
- Garantir **desempenho** e **simplicidade** na experiência do usuário.

---

## Demonstração do aplicativo

As telas abaixo ilustram o fluxo da consulta pública à Tabela FIPE, conforme planejado e implementado.

### 1. Seleção da referência (mês/ano)

O usuário escolhe o mês/ano de referência da tabela FIPE. A interface exibe aviso sobre a limitação da API pública (referências recentes) e orienta a informar em seguida marca, modelo e ano modelo.

![Seleção de mês/ano de referência](/assets/images/Imagem 1.PNG)

### 2. Formulário de pesquisa

Seleção do tipo de veículo (Carros, Motos, Caminhões), marca, modelo e ano modelo. O usuário pode digitar nos campos para buscar. Botão **PESQUISAR** dispara a consulta ao backend (FipeService).

![Formulário: tipo, marca, modelo e ano modelo](/assets/images/consulta-fipe-02-formulario.png)

### 3. Resultado da consulta

Exibição do **Valor FIPE** retornado pela API. Opção de expandir "Ver todos os dados" (atributos e campos da resposta) e de **Baixar PDF da pesquisa**.

![Resultado da consulta com valor FIPE e opção de PDF](/assets/images/consulta-fipe-03-resultado.png)

### 4. Dados da pesquisa e resultado detalhado

Visão que reúne os **dados da pesquisa** (referência, tipo, marca, modelo, ano modelo) e o **resultado da consulta** (valor FIPE e detalhes como CodigoFipe, combustível, mês de referência).

![Dados da pesquisa e resultado detalhado](/assets/images/consulta-fipe-04-resultado-detalhes.png)
