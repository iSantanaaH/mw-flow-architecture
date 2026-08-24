<div align="center">

# 🚀 MW-Flow | Enterprise Microservices POS & ERP System

![Status](https://img.shields.io/badge/Status-Em_Desenvolvimento_Active_WIP-yellow.svg?style=for-the-badge)
[![Java](https://img.shields.io/badge/Java-21-orange.svg?style=for-the-badge&logo=openjdk&logoColor=white)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)](https://spring.io/projects/spring-boot)
[![Keycloak](https://img.shields.io/badge/Keycloak-IAM_&_OAuth2-4D4D4D?style=for-the-badge&logo=keycloak&logoColor=white)](https://www.keycloak.org/)
[![Apache Kafka](https://img.shields.io/badge/Apache_Kafka-Event_Driven-231F20?style=for-the-badge&logo=apachekafka&logoColor=white)](https://kafka.apache.org/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestrated-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![Prometheus](https://img.shields.io/badge/Prometheus-Metrics-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)](https://prometheus.io/)
[![Grafana](https://img.shields.io/badge/Grafana-Observability-F46800?style=for-the-badge&logo=grafana&logoColor=white)](https://grafana.com/)
[![Jenkins](https://img.shields.io/badge/Jenkins-CI%2FCD_Pipeline-D24939?style=for-the-badge&logo=jenkins&logoColor=white)](https://www.jenkins.io/)
[![GraphQL](https://img.shields.io/badge/GraphQL-Enabled-E10098?style=for-the-badge&logo=graphql&logoColor=white)](https://graphql.org/)
[![Angular](https://img.shields.io/badge/Angular-22+-DD0031.svg?style=for-the-badge&logo=angular&logoColor=white)](https://angular.io/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1.svg?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-Cache-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)

<p align="center">
  <b>Ecossistema Distribuído de Ponto de Venda (PDV) Omnichannel & Gestão ERP Enterprise</b><br>
  Microserviços com Clean Architecture, Keycloak IAM, Event-Driven (Kafka/RabbitMQ), Observabilidade Total (Prometheus/Grafana) e CI/CD (Jenkins).
</p>

</div>

---

> ⚠️ **Aviso de Desenvolvimento:** O **MW-Flow** é um produto comercial SaaS atualmente em fase de **desenvolvimento ativo de migração e expansão para Microserviços**. Este repositório serve como documentação pública da arquitetura macro, decisões de engenharia, DevOps e especificações do sistema.

---

## 📌 Sobre o MW-Flow

O **MW-Flow** é uma plataforma SaaS distribuída, projetada sob a arquitetura de **Microserviços**, **Clean Architecture**, **DDD (Domain-Driven Design)** e **Event-Driven Architecture (EDA)**. O sistema foi concebido para suportar altas cargas do varejo moderno, oferecendo tolerância a falhas, resiliência *offline-first* para frente de caixa, governança estrita de identidade e automação completa de entrega contínua.

Este projeto consolida **6+ anos de engenharia de software**, demonstrando a orquestração e execução de um ecossistema cloud-native real de grande porte.

---

## 🔒 Visão de Repositórios do Ecossistema

Para garantir a proteção da propriedade intelectual da aplicação mantendo a transparência arquitetural para portfólio, o projeto é estruturado de forma desacoplada:

* 🏢 **`mw-flow-architecture` (Este Repositório / Público):** Visão geral, diagramas, especificações de APIs, manifestos Kubernetes, pipelines Jenkins e orquestração Docker Compose.
* 🔑 **`ms-auth` (Privado):** Microserviço de Autenticação, Tokens JWT/Cookies, Rate-Limiting e Integração Keycloak.
* 🛒 **`ms-pos` (Privado):** Microserviço de Ponto de Venda, Contingência Offline-First e Emissão Fiscal SEFAZ.
* 📦 **`ms-inventory` (Privado):** Microserviço de Gestão de Estoque, Produtos, EAN/GTIN e APIs GraphQL.

---

## 🧩 Visão Geral dos Microserviços

O core do backend é dividido em três microserviços independentes e especializados:

### 🔑 1. `ms-auth` (Identidade e Permissões)
Serviço centralizador de governança, autenticação e autorização federada do ecossistema:
* **Autenticação & Gestão de Sessão:** Login, registro de usuários, gerenciamento completo de contas e endereços.
* **Segurança & Tokens:** Emissão e rotação segura de tokens JWT via `Set-Cookie` com suporte a perfis e permissões granulares (*Roles/RBAC*).
* **Proteção Defensiva:** Controle de taxa de requisições (*rate-limiting*) por IP/usuário integrado ao **Redis** para mitigação de ataques de força bruta.
* **IAM Enterprise:** Integração e federação de identidade via **Keycloak**.

### 🛒 2. `ms-pos` (Point of Sale / PDV)
API responsável pela operação de frente de caixa, processamento direto de vendas e integração fiscal:
* **Abertura e Fechamento de Caixa:** Controle rigoroso de saldo inicial, sangrias e suprimentos.
* **Processamento de Checkout:** Recebimento dos itens do carrinho consumidos do frontend Angular, cálculo automático de descontos e suporte a múltiplas formas de pagamento (Pix, Cartão, Dinheiro).
* **Fila de Sincronização (Sync Offline-First):** Endpoint resiliente para receber, processar em lote e persistir as vendas efetuadas localmente pelo cliente Angular durante períodos de contingência offline.
* **Comunicação Assíncrona:** Ao finalizar cada venda, o `ms-pos` publica eventos em mensageria (**RabbitMQ/Kafka**) notificando o `ms-inventory` para efetuar a baixa automática de estoque.
* **Emissão Fiscal Integrada:** Autorização e geração de documentos fiscais (NFC-e/NF-e) com SEFAZ.

### 📦 3. `ms-inventory` (Estoque e Produtos)
API responsável pela inteligência de catálogo, precificação e ciclo de vida das mercadorias:
* **Gestão de Catálogo:** Cadastro completo de produtos, categorias, variações, precificação (custo x venda) e identificadores globais (código de barras EAN/GTIN).
* **Controle de Movimentações:** Rastreamento de entradas de produtos por notas fiscais, ajustes e saídas manuais, além de registro de perdas/avarias.
* **Alertas Inteligentes:** Monitoramento preventivo de níveis mínimos de estoque e emissão de alertas de reabastecimento.
* **APIs de Consulta Eficientes:** Endpoints GraphQL para resolução de consultas complexas e dinâmicas de catálogo sem *over-fetching*.

---

## ⚙️ Ecossistema & Infraestrutura Enterprise

### 🔐 Gestão de Identidade & Segurança Zero-Trust
* **OAuth2 / OpenID Connect (OIDC):** Servidor de identidade centralizado com **Keycloak**, delegando a autenticação e autorização de forma federada.
* **Proteção OWASP & HTTP Security Headers:** Injeção automática de cabeçalhos de segurança (`X-Content-Type-Options: nosniff`, `X-Frame-Options: DENY`, `Content-Security-Policy`, `Strict-Transport-Security`).
* **Request Payload Limit Filter:** Sanitização e limite estrito do tamanho do corpo das requisições para mitigar DoS.

### 🔄 Mensageria & Event-Driven Architecture (Kafka / RabbitMQ)
* **Comunicação Assíncrona Desacoplada:** Processamento de vendas e atualização de estoque desacoplados via tópicos/filas entre `ms-pos` e `ms-inventory`.
* **Garantia de Entrega & DLT:** Estratégias de *Retry* com **Dead Letter Topics (DLT)** para evitar perda de dados operacionais ou fiscais em instabilidades temporárias.

### 📊 Observabilidade Total (Prometheus & Grafana)
* **Coleta de Métricas Expostas:** Endpoints do **Spring Boot Actuator** e Micrometer coletando dados de uso de CPU, memória, conexões com bancos de dados e throughput de mensagens.
* **Prometheus:** Agregação contínua de métricas de saúde, latência e disponibilidade de cada um dos 3 microserviços.
* **Dashboards no Grafana:** Visualização centralizada em tempo real para monitoramento do estado da infraestrutura e volumetria do PDV.

### 🚀 CI/CD & Automação de Infraestrutura (Jenkins & K8s)
* **Pipelines de CI/CD (Jenkins):** Automação do ciclo de vida do software — análise estática de código, execução de suítes de testes unitários/integração, build de imagens Docker e deploy contínuo.
* **Orquestração em Kubernetes (K8s):** Manifestos configurados para **Horizontal Pod Autoscaler (HPA)**, gerando escalabilidade dinâmica para os pods do `ms-pos` e `ms-inventory` durante picos de movimentação.
* **Self-Healing:** *Liveness* e *Readiness Probes* configurados para autorrecuperação transparente em caso de indisponibilidade.

---

## 🏛️ Estrutura da Infraestrutura (DevOps & Configurações)

```text
mw-flow-architecture/
├── devops/                               # Infraestrutura & Suporte Cloud-Native
│   ├── jenkins/                          # Jenkinsfile e scripts de Pipeline CI/CD
│   ├── keycloak/                         # Realm configurations & export files
│   ├── prometheus-grafana/               # Configurações do Prometheus & Dashboards Grafana
│   └── k8s/                              # Manifestos Kubernetes (Deployments, HPA, Ingress)
└── docker-compose.yml                    # Provisionamento local do ecossistema completo
