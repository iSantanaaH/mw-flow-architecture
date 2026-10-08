<div align="center">

# 🚀 MW-Flow | Sistema Enterprise Multitenant de PDV & ERP em Microserviços

![Status](https://img.shields.io/badge/Status-Em_Desenvolvimento_Active_WIP-yellow.svg?style=for-the-badge)
[![Java](https://img.shields.io/badge/Java-21-orange.svg?style=for-the-badge&logo=openjdk&logoColor=white)](https://www.oracle.com/java/)
[![Quarkus](https://img.shields.io/badge/Quarkus-3.x-4695EB?style=for-the-badge&logo=quarkus&logoColor=white)](https://quarkus.io/)
[![Keycloak](https://img.shields.io/badge/Keycloak-IAM_&_OAuth2-4D4D4D?style=for-the-badge&logo=keycloak&logoColor=white)](https://www.keycloak.org/)
[![RabbitMQ](https://img.shields.io/badge/RabbitMQ-Event_Driven-FF6600?style=for-the-badge&logo=rabbitmq&logoColor=white)](https://www.rabbitmq.com/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestrated-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI%2FCD-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)](https://github.com/features/actions)
[![SonarQube](https://img.shields.io/badge/SonarQube-Code_Quality-4E9BCD?style=for-the-badge&logo=sonarqube&logoColor=white)](https://www.sonarqube.org/)
[![Swagger](https://img.shields.io/badge/Swagger-OpenAPI_3.0-85EA2D?style=for-the-badge&logo=swagger&logoColor=white)](https://swagger.io/)
[![Prometheus](https://img.shields.io/badge/Prometheus-Metrics-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)](https://prometheus.io/)
[![Grafana](https://img.shields.io/badge/Grafana-Observability-F46800?style=for-the-badge&logo=grafana&logoColor=white)](https://grafana.com/)
[![GraphQL](https://img.shields.io/badge/GraphQL-Enabled-E10098?style=for-the-badge&logo=graphql&logoColor=white)](https://graphql.org/)
[![Angular](https://img.shields.io/badge/Angular-22+-DD0031.svg?style=for-the-badge&logo=angular&logoColor=white)](https://angular.io/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1.svg?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-Cache-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)

<p align="center">
  <b>Ecossistema Distribuído Multitenant de Ponto de Venda (PDV) Omnichannel & Gestão ERP Enterprise</b><br>
  Microserviços Cloud-Native em Quarkus com Clean Architecture, Keycloak IAM, Event-Driven Architecture (RabbitMQ), Qualidade Continuada (SonarQube), Documentação OpenAPI/Swagger, Observabilidade Total (Prometheus/Grafana) e CI/CD via GitHub Actions.
</p>

</div>

---

> ⚠️ **Aviso de Desenvolvimento:** O **MW-Flow** é um produto comercial SaaS multitenant em **fase ativa de migração e expansão para Microserviços de altíssima performance utilizando Quarkus**. Este repositório serve como documentação pública da arquitetura macro, decisões de engenharia e especificações de ecossistema.

---

## 📌 Sobre o MW-Flow

O **MW-Flow** é uma plataforma SaaS distribuída e **Multitenant**, projetada sob a arquitetura de **Microserviços Reativos**, **Clean Architecture**, **DDD (Domain-Driven Design)** e **Event-Driven Architecture (EDA)**. Powered by **Quarkus e Java 21**, o sistema garante um footprint de memória extremamente reduzido e tempo de inicialização (*startup time*) quase instantâneo, ideal para escalabilidade reativa no Kubernetes.

A plataforma foi concebida para atender empresas e varejistas em escala multitenant, oferecendo isolamento seguro de dados, tolerância a falhas, resiliência *offline-first* no frente de caixa, governança federada de identidade e automação fluida de entrega contínua.

Este projeto consolida **6+ anos de experiência em engenharia de software**, demonstrando a orquestração e execução de um ecossistema cloud-native real de alto desempenho.

---

## 🔒 Visão de Repositórios do Ecossistema

Para garantir a proteção da propriedade intelectual da aplicação mantendo a transparência arquitetural para portfólio, o ecossistema MW-Flow é estruturado de forma desacoplada:

* 🏢 **`mw-flow-architecture` (Este Repositório / Público):** Documentação arquitetural macro, especificações de domínio, diagramas do ecossistema multitenant, contratos OpenAPI/Swagger e diretrizes de integração.
* 🛠️ **`ms-infra` (Privado):** Repositório central de infraestrutura local (`docker-compose.yml`), contendo os serviços de suporte (PostgreSQL, Redis, RabbitMQ, Keycloak, SonarQube, Prometheus e Grafana), manifestos Kubernetes e pipelines CI/CD no GitHub Actions.
* 🔑 **`ms-auth` (Privado):** Microserviço em Quarkus para Autenticação Multitenant, Rotação de Tokens JWT, Rate-Limiting com Redis e Governança IAM via Keycloak.
* 🛒 **`ms-pos` (Privado):** Microserviço em Quarkus para Ponto de Venda (PDV), Contingência Offline-First, Emissão Fiscal SEFAZ e Comunicação via Mensageria.
* 📦 **`ms-inventory` (Privado):** Microserviço em Quarkus para Gestão de Estoque, Catálogo Multitenant, Rastreamento EAN/GTIN e APIs GraphQL / REST.
* 💻 **`mw-flow-web` (Privado):** Aplicação Frontend SPA em Angular, responsável pelo Dashboard Operacional e Interface Web Multitenant.

---

## 🧩 Visão Geral dos Microserviços (Stack Quarkus)

O core reativo do backend é construído em **Quarkus** e dividido em três microserviços especializados:

### 🔑 1. `ms-auth` (Identidade e Governança Multitenant)
Serviço centralizador de governança, autenticação e autorização federada para todos os *tenants*:
* **Isolamento e Contexto Multitenant:** Resolução e validação do *Tenant ID* em cada requisição para garantia de isolamento absoluto de dados.
* **Autenticação & Gestão de Sessão:** Login, registro de usuários e gerenciamento completo de contas e permissões organizacionais.
* **Segurança & Tokens:** Emissão e rotação de tokens JWT com suporte a perfis e permissões granulares (*RBAC/ABAC*).
* **Proteção Defensiva:** Controle de taxa de requisições (*rate-limiting*) reativo por IP/tenant/usuário integrado ao **Redis**.
* **IAM Enterprise:** Integração e federação de identidade via **Keycloak**.
* **Swagger/OpenAPI:** Documentação interativa e contratos de API de identidade gerados automaticamente.

### 🛒 2. `ms-pos` (Point of Sale / PDV)
API Reativa responsável pela operação de frente de caixa, processamento de vendas e integração fiscal:
* **Abertura e Fechamento de Caixa:** Controle rigoroso de saldo inicial, sangrias e suprimentos por operador e filial do tenant.
* **Processamento de Checkout:** Recebimento do carrinho vindo do frontend Angular, cálculo dinâmico de descontos e suporte a múltiplas formas de pagamento (Pix, Cartão, Dinheiro).
* **Fila de Sincronização (Sync Offline-First):** Endpoint ultra-resiliente para loteamento e persistência das vendas efetuadas offline pela aplicação client.
* **Comunicação Assíncrona via Mensageria:** Publicação de eventos via **RabbitMQ** para baixa automática de estoque no `ms-inventory` logo após a confirmação da venda.
* **Emissão Fiscal Integrada:** Processamento assíncrono para autorização e geração de documentos fiscais (NFC-e/NF-e) na SEFAZ.

### 📦 3. `ms-inventory` (Estoque e Produtos Multitenant)
API responsável pela inteligência de catálogo, precificação e ciclo de vida das mercadorias por organização:
* **Gestão de Catálogo Multitenant:** Cadastro completo de produtos, categorias, variações, precificação (custo x venda) e identificadores globais (EAN/GTIN) isolados por *tenant*.
* **Controle de Movimentações:** Rastreamento de entradas por NF-e, ajustes, saídas e registro de perdas/avarias.
* **Alertas Inteligentes:** Monitoramento de estoque mínimo e regras automáticas de reabastecimento.
* **APIs GraphQL Reativas:** Endpoints GraphQL de alta performance para consultas complexas e dinâmicas de catálogo sem *over-fetching*.

---

## ⚙️ Ecossistema & Infraestrutura Enterprise

### 🛠️ Infraestrutura Compartilhada (`ms-infra`)
Ambiente unificado para desenvolvimento local e testes de integração via Docker Compose:

| Serviço | Tecnologia | Porta Interna | Porta Mapeada (Host) | Finalidade / Acesso |
| :--- | :--- | :--- | :--- | :--- |
| **PostgreSQL (App)** | Database Engine | `5432` | `5432` | Banco de dados primário do ecossistema (`mwflow_db`) |
| **PostgreSQL (Sonar)** | Database Engine | `5432` | *Interna* | Banco de dados isolado para dados do SonarQube |
| **SonarQube** | Quality & Security | `9000` | `9000` | Análise estática, bugs, code smells e cobertura (http://localhost:9000) |
| **Keycloak** | Identity Provider | `8080` | `8082` | Servidor IAM, OAuth2 e OpenID Connect (http://localhost:8082) |
| **RabbitMQ** | Message Broker | `5672` / `15672` | `5672` / `15672` | Broker de eventos e painel de gestão AMQP (http://localhost:15672) |
| **Redis** | In-Memory Data Store | `6379` | `6379` | Armazenamento em memória para cache rápido e rate limiting |
| **Prometheus** | Metrics Collector | `9090` | `9090` | Motor de coleta e agregação de métricas temporais (http://localhost:9090) |
| **Grafana** | Observability Dashboard | `3000` | `3000` | Visualização centralizada de métricas e dashboards (http://localhost:3000) |
| **Swagger UI** | API Documentation | *Embedded* | Via Microserviço | Interface visual interativa para teste e exploração de endpoints |

---

### 🏢 Arquitetura SaaS Multitenant
* **Tenant Isolation:** Estratégia flexível de isolamento multitenant no banco de dados e na camada de aplicação via contextos de execução do Quarkus (`TenantResolver`).
* **Roteamento de Requisições:** Identificação e roteamento automático de requisições baseados no token JWT ou headers organizacionais.

### ⚡ Quarkus & Supersonic Subatomic Java
* **Desempenho Extremo:** Aplicações otimizadas para baixo consumo de memória RAM e inicialização em milissegundos.
* **Compilação Nativa (GraalVM):** Suporte total a builds nativos executáveis em contêineres ultra-leves.

### 🔐 Gestão de Identidade & Segurança Zero-Trust
* **OAuth2 / OpenID Connect (OIDC):** Autenticação e autorização centralizadas via **Keycloak**.
* **OWASP & Security Headers:** Injeção automática de cabeçalhos defensivos (`X-Content-Type-Options`, `X-Frame-Options`, `Content-Security-Policy`, `HSTS`).

### 🔄 Mensageria Event-Driven (RabbitMQ)
* **Comunicação Assíncrona Desacoplada:** Processamento de eventos de venda, baixa de estoque e auditoria via filas e trocas (*exchanges*) do RabbitMQ.
* **Resiliência:** Estratégias de *Retry* reativo e **Dead Letter Exchange (DLX)** para tratamento seguro de falhas temporárias.

### 🎯 Qualidade de Código & Governança (SonarQube & Swagger)
* **SonarQube & Clean Code:** Análise estática automatizada em pipelines para acompanhamento de dívida técnica, identificação de vulnerabilidades (*security hotspots*), bugs e cobertura de testes unitários e de integração.
* **OpenAPI 3.0 & Swagger UI:** Contratos de API REST devidamente padronizados e expostos de forma interativa via Swagger UI em cada microserviço.

### 📊 Observabilidade Total (Prometheus & Grafana)
* **Métricas Quarkus SmallRye Metrics / Micrometer:** Monitoramento de CPU, memória, pool de conexões com banco e métricas de mensagens consumidas do RabbitMQ.
* **Prometheus & Grafana:** Agregação de dados e exibições em tempo real através de dashboards operacionais e de infraestrutura.

### 🚀 CI/CD Integrado (GitHub Actions & Kubernetes)
* **Pipelines CI/CD (GitHub Actions):** Workflows automatizados para lint, testes unitários/integração, validação no SonarQube, build de imagens Docker e deployment no cluster Kubernetes.
* **Orquestração K8s:** Manifestos configurados com **Horizontal Pod Autoscaler (HPA)** no `ms-infra`, escalando os pods dos microserviços conforme demanda do sistema.
* **Self-Healing:** *Liveness* e *Readiness Probes* configuradas para recuperação automática de pods degradados.

---

## 🏛️ Estrutura Geral do Ecossistema

```text
mw-flow-architecture/
├── docs/                    # Diagramas de arquitetura, C4 Model e fluxos de integração
├── openapi/                 # Especificações públicas das APIs REST dos microserviços (Swagger/OpenAPI)
└── README.md                # Documentação institucional da arquitetura do ecossistema
