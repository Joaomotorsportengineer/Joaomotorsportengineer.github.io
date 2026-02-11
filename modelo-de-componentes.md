---
title: Modelo de componentes
nav_order: 5
---

O modelo de componentes descreve a organização técnica do sistema, apresentando a divisão da aplicação em componentes de software, suas responsabilidades e a forma como se comunicam. O objetivo é garantir modularidade, separação de responsabilidades, facilidade de manutenção e testabilidade.

O sistema foi projetado seguindo uma **arquitetura em camadas**, na qual cada componente possui uma função bem definida.

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
- Controlar permissões de acesso com base no papel do usuário (Admin, Gerente, Coordenador, etc.).
- Realizar validação de credenciais e hash de senha.

**Benefício:**

- Centraliza a segurança do sistema.
- Facilita a manutenção e evolução das regras de acesso.

---

## Componentes de Serviços

Os serviços concentram toda a **lógica de negócio** do sistema, sendo responsáveis por validar regras, coordenar fluxos e interagir com os repositórios.

**Principais serviços:**

| Serviço | Função |
|---------|--------|
| UsuarioService | Gerenciamento de usuários e permissões. |
| LojaService | Cadastro e aprovação de lojas. |
| MarcaModeloService | Gerenciamento de marcas e modelos. |
| PesquisaService | Registro das pesquisas realizadas pelos pesquisadores. |
| CotacaoService | Cálculo e consulta de preços médios. |
| AprovacaoService | Controle do processo de aprovação. |
| BatchService | Processamento mensal para cálculo da média de preços. |

---

## Componentes de Persistência (Repositórios / DAO)

**Responsabilidade:**

- Realizar acesso direto ao banco de dados.
- Executar operações de leitura e escrita (CRUD).
- Garantir integridade e consistência dos dados.

**Exemplos de repositórios:**

- UsuarioRepository
- LojaRepository
- ModeloRepository
- CotacaoRepository
- ConsultaRepository

Esses componentes não possuem regras de negócio, apenas lógica de persistência.

---

## Componente de Banco de Dados (SQL)

**Responsabilidade:**

- Armazenar de forma persistente os dados do sistema.
- Garantir integridade referencial por meio de chaves primárias e estrangeiras.
- Servir como base para consultas e processamento batch.

---

## Componente de Processamento Batch

**Responsabilidade:**

- Executar periodicamente o cálculo da média mensal dos preços.
- Processar grandes volumes de dados.
- Persistir os resultados na tabela Batch_Resultados.

---

## Componente de Testes Automatizados

**Responsabilidade:**

- Validar o correto funcionamento dos componentes do sistema.
- Executar testes unitários dos serviços.
- Executar testes de integração entre serviços, repositórios e banco de dados.

**Tecnologia utilizada:** Pytest
