---
title: Technical Design (TD) dos componentes
nav_order: 6
---

## Visão Geral da Arquitetura

A aplicação segue o padrão de **Arquitetura em Camadas** (Layered Architecture), separando responsabilidades entre interface, regras de negócio, persistência de dados e testes, facilitando manutenção, escalabilidade e testabilidade.

### Tecnologias

| Área | Tecnologia |
|------|------------|
| Frontend | Streamlit |
| Backend | Python |
| Banco de Dados | SQL |
| Testes automatizados | Pytest |
| Metodologia | Scrum (Jira) |
| Modelagem | Fluxograma no Miro |

---

## Estrutura do Projeto (base)

```
projeto-cotacao/
├── .env
├── .env.example
├── README.md
├── requirements.txt
├── pytest.ini
├── app.py                          # Ponto de entrada Streamlit (streamlit run app.py)
│
├── config/                         # Core / infra
│
├── auth/                           # Autenticação e autorização
│
├── domain/                         # (Opcional) Modelos/entidades em memória
│
├── repos/                          # Camada de persistência (um arquivo por entidade ou agrupamento)
│
├── services/                       # Camada de serviço (regras de negócio, orquestração)
│
├── pages/                          # Interface Streamlit (uma página por "tela" ou papel)
│
├── ui/                             # Componentes de UI reutilizáveis
│
├── migrations/                     # (Opcional) Scripts SQL de migração
│
├── scripts/                        # Scripts úteis (seed, batch manual, etc.)
│
└── tests/                          # Testes automatizados (pytest)
```

### Descrição das pastas

| Pasta | Função |
|-------|--------|
| **app.py** | Ponto de entrada da aplicação; executar com `streamlit run app.py`. |
| **config/** | Configurações e infraestrutura (variáveis de ambiente, conexão com banco, etc.). |
| **auth/** | Autenticação e autorização (login, perfis, permissões). |
| **domain/** | (Opcional) Modelos/entidades em memória. |
| **repos/** | Camada de persistência; um arquivo por entidade ou agrupamento (DAO/Repository). |
| **services/** | Camada de serviço; regras de negócio e orquestração. |
| **pages/** | Páginas Streamlit; uma página por tela ou papel. |
| **ui/** | Componentes de interface reutilizáveis. |
| **migrations/** | (Opcional) Scripts SQL de migração do banco. |
| **scripts/** | Scripts auxiliares (seed, batch manual, etc.). |
| **tests/** | Testes automatizados (pytest). |
