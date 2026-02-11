---
title: Modelo de componentes
nav_order: 5
---

O modelo de componentes descreve a organização técnica do sistema, apresentando a divisão da aplicação em componentes de software, suas responsabilidades e a forma como se comunicam. O objetivo é garantir **modularidade**, **separação de responsabilidades**, **facilidade de manutenção** e **testabilidade**.

O sistema foi projetado seguindo uma **arquitetura em camadas** (Layered Architecture), na qual cada componente possui uma função bem definida e se comunica apenas com as camadas adjacentes.

---

## Visão do fluxo entre camadas

```
[Interface Streamlit] → [Serviços] → [Repositórios] → [Banco de Dados]
         ↑                    ↑              ↑
    (usuário)          (regras de      (CRUD, SQL)
                        negócio)
```

A **autenticação e autorização** atuam na entrada das requisições; o **processamento batch** e os **testes** são componentes transversais.

---

## Componente de Interface (Frontend – Streamlit)

**Responsabilidade:**

- Disponibilizar as telas do sistema para os usuários.
- Coletar dados de entrada (filtros de consulta, formulários).
- Exibir resultados e mensagens ao usuário.

**Características:**

- Desenvolvido com Streamlit.
- Não contém regras de negócio.
- Comunica-se exclusivamente com a camada de serviços.

---

## Componente de Autenticação e Autorização

**Responsabilidade:**

- Gerenciar autenticação de usuários.
- Controlar permissões de acesso com base no papel do usuário (Admin, Gerente, Coordenador, Pesquisador, Logista, Batch).
- Realizar validação de credenciais e hash de senha.

**Benefício:**

- Centraliza a segurança do sistema.
- Facilita a manutenção e evolução das regras de acesso.

---

## Componentes de Serviços

Os serviços concentram toda a **lógica de negócio** do sistema, sendo responsáveis por validar regras, coordenar fluxos e interagir com os repositórios.

**Principais serviços:**

| Serviço | Função | Entidades relacionadas (modelo de dados) |
|---------|--------|------------------------------------------|
| UsuarioService | Gerenciamento de usuários e permissões. | Usuario |
| LojaService | Cadastro e aprovação de lojas. | Loja, Regiao |
| MarcaModeloService | Gerenciamento de marcas e modelos. | Marca, Modelo |
| PesquisaService | Registro das pesquisas realizadas pelos pesquisadores. | Pesquisa, Veículo pesquisado |
| CotacaoService | Cálculo e consulta de preços médios. | Cotacao |
| AprovacaoService | Controle do processo de aprovação de lojas. | Aprovacao |
| BatchService | Processamento mensal para cálculo da média de preços. | Batch_Resultados |

---

## Componentes de Persistência (Repositórios / DAO)

**Responsabilidade:**

- Realizar acesso direto ao banco de dados.
- Executar operações de leitura e escrita (CRUD).
- Garantir integridade e consistência dos dados.

**Repositórios (alinhados ao modelo de dados):**

| Repositório | Tabela(s) / entidade(s) |
|-------------|--------------------------|
| UsuarioRepository | Usuario |
| RegiaoRepository | Regiao |
| LojaRepository | Loja |
| MarcaRepository | Marca |
| ModeloRepository | Modelo |
| PesquisaRepository | Pesquisa |
| VeiculoPesquisadoRepository | Veículo pesquisado |
| CotacaoRepository | Cotacao |
| ConsultaRepository | Consulta |
| AprovacaoRepository | Aprovacao |
| BatchResultadosRepository | Batch_Resultados |

Esses componentes **não possuem regras de negócio**, apenas lógica de persistência.

---

## Componente de Banco de Dados (SQL)

**Responsabilidade:**

- Armazenar de forma persistente os dados do sistema.
- Garantir integridade referencial por meio de chaves primárias e estrangeiras.
- Servir como base para consultas e processamento batch.

As tabelas e relacionamentos estão descritos no [Projeto do modelo de dados](modelo-de-dados.md).

---

## Componente de Processamento Batch

**Responsabilidade:**

- Executar periodicamente o cálculo da média mensal dos preços.
- Processar grandes volumes de dados (a partir de Pesquisa / Veículo pesquisado e/ou Cotacao).
- Persistir os resultados na tabela **Batch_Resultados** por meio do BatchResultadosRepository.

---

## Componente de Testes Automatizados

**Responsabilidade:**

- Validar o correto funcionamento dos componentes do sistema.
- Executar testes unitários dos serviços.
- Executar testes de integração entre serviços, repositórios e banco de dados.

**Tecnologia utilizada:** Pytest
