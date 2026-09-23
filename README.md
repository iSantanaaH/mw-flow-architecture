<div align="center">

# 🚀 MW-Flow | Enterprise Multitenant Microservices POS & ERP System

![Status](https://img.shields.io/badge/Status-Em_Desenvolvimento_Active_WIP-yellow.svg?style=for-the-badge)
[![Java](https://img.shields.io/badge/Java-21-orange.svg?style=for-the-badge&logo=openjdk&logoColor=white)](https://www.oracle.com/java/)
[![Quarkus](https://img.shields.io/badge/Quarkus-3.x-4695EB?style=for-the-badge&logo=quarkus&logoColor=white)](https://quarkus.io/)
[![Keycloak](https://img.shields.io/badge/Keycloak-IAM_&_OAuth2-4D4D4D?style=for-the-badge&logo=keycloak&logoColor=white)](https://www.keycloak.org/)
[![RabbitMQ](https://img.shields.io/badge/RabbitMQ-Event_Driven-FF6600?style=for-the-badge&logo=rabbitmq&logoColor=white)](https://www.rabbitmq.com/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestrated-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI%2FCD-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)](https://github.com/features/actions)
[![Prometheus](https://img.shields.io/badge/Prometheus-Metrics-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)](https://prometheus.io/)
[![Grafana](https://img.shields.io/badge/Grafana-Observability-F46800?style=for-the-badge&logo=grafana&logoColor=white)](https://grafana.com/)
[![GraphQL](https://img.shields.io/badge/GraphQL-Enabled-E10098?style=for-the-badge&logo=graphql&logoColor=white)](https://graphql.org/)
[![Angular](https://img.shields.io/badge/Angular-22+-DD0031.svg?style=for-the-badge&logo=angular&logoColor=white)](https://angular.io/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1.svg?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-Cache-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)

<p align="center">
  <b>Ecossistema Distribuído Multitenant de Ponto de Venda (PDV) Omnichannel & Gestão ERP Enterprise</b><br>
  Microserviços Cloud-Native em Quarkus com Clean Architecture, Keycloak IAM, Event-Driven Architecture (RabbitMQ), Observabilidade Total (Prometheus/Grafana) e CI/CD via GitHub Actions.
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

* 🏢 **`mw-flow-architecture` (Este Repositório / Público):** Documentação arquitetural macro, especificações de domínio, diagramas do ecossistema multitenant e diretrizes de integração.
* 🛠️ **`ms-infra` (Privado):** Repositório central de infraestrutura, orquestração local (`docker-compose.yml`), manifestos Kubernetes (Deployments, HPA, Ingress, ConfigMaps), pipelines no GitHub Actions e configurações de observabilidade (Prometheus/Grafana) e IAM (Keycloak).
* 🔑 **`ms-auth` (Privado):** Microserviço de Autenticação Multitenant, Tokens JWT, Rate-Limiting e Integração Keycloak.
* 🛒 **`ms-pos` (Privado):** Microserviço de Ponto de Venda, Contingência Offline-First e Emissão Fiscal SEFAZ.
* 📦 **`ms-inventory` (Privado):** Microserviço de Gestão de Estoque, Catálogo Multitenant, EAN/GTIN e APIs GraphQL.

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
* **Comunicação Assíncrona Desacoplada:** Processamento de eventos de venda, baixa de estoque e auditoria via filas e trocas (exchanges) do RabbitMQ.
* **Resiliência:** Estratégias de *Retry* reativo e **Dead Letter Exchange (DLX)** para tratamento seguro de falhas temporárias.

### 📊 Observabilidade Total (Prometheus & Grafana)
* **Métricas Quarkus SmallRye Metrics / Micrometer:** Monitoramento de CPU, memória, pool de conexões com banco e métricas de mensagens consumidas do RabbitMQ.
* **Prometheus & Grafana:** Agregação de dados e exibições em tempo real através de dashboards operacionais e de infraestrutura.

### 🚀 CI/CD Integrado (GitHub Actions & Kubernetes)
* **Pipelines CI/CD (GitHub Actions):** Workflows automatizados para lint, testes unitários/integração, build de imagens Docker e deployment no cluster Kubernetes.
* **Orquestração K8s:** Manifestos configurados com **Horizontal Pod Autoscaler (HPA)** no `ms-infra`, escalando os pods dos microserviços conforme demanda do sistema.
* **Self-Healing:** *Liveness* e *Readiness Probes* configuradas para recuperação automática de pods degradados.

---

## 🏛️ Estrutura Geral do Ecossistema

### 🏢 `mw-flow-architecture` (Este Repositório Público)
```text
mw-flow-architecture/
├── docs/                           # Diagramas de arquitetura, C4 Model e fluxos de integração
├── openapi/                        # Especificações públicas das APIs REST dos microserviços
└── README.md                       # Documentação institucional da arquitetura do ecossistema
