# 🚦 QFlow

### Plataforma Inteligente de Gestão e Otimização de Filas

O **QFlow** é uma plataforma para gerenciamento de filas de atendimento que utiliza **regras configuráveis de priorização e distribuição**, buscando reduzir o tempo de espera e otimizar a utilização dos atendentes.

A proposta é substituir filas baseadas exclusivamente na ordem de chegada por um sistema capaz de considerar diferentes fatores para definir a ordem de atendimento.

---

## 💡 Proposta

O QFlow utiliza um **motor de decisão** para determinar o próximo atendimento com base em fatores como:

-  Tempo de espera
-  Prioridade
-  Tipo de atendimento
-  Disponibilidade e compatibilidade dos atendentes
-  Regras configuradas pela organização

As regras podem ser adaptadas de acordo com o contexto de cada instituição.

### Possíveis aplicações

 Saúde ·  Bancos ·  Educação ·  Órgãos públicos ·  Suporte técnico ·  Centrais de atendimento

---

# 🏗️ Arquitetura
### Diagrama básico da arquitetura do software e suas ferramentas

```mermaid
flowchart TB
    %% CLIENTES
    subgraph CLIENT["Clientes"]
        WEB["Frontend Web<br/>React + TypeScript"]
        ADM["Painel Administrativo<br/>React + TypeScript"]
    end

    %% BACKEND
    subgraph BACK["Backend — Go"]
        API["API REST<br/>Gin Framework"]
        AUTH["Autenticação<br/>JWT + bcrypt"]
        QUEUE["Serviço de Filas<br/>Gerenciamento de filas"]
        PRIORITY["Motor de Priorização<br/>Algoritmo de decisão"]
        SERVICE["Serviço de Atendimento<br/>Controle de atendimentos"]
        METRICS["Serviço de Métricas<br/>Relatórios e KPIs"]
        WS["WebSocket<br/>Real-time"]
    end

    %% DATABASE
    subgraph DATA["Persistência"]
        DB[("PostgreSQL<br/>Banco de Dados")]
        CACHE["Redis<br/>Cache & Sessions"]
    end

    %% INFRA
    subgraph INFRA["Infraestrutura"]
        DOCKER["Docker<br/>Containerização"]
        COMPOSE["Docker Compose<br/>Orquestração local"]
    end

    %% CONEXÕES - Cliente para Backend
    WEB -->|"HTTP / REST"| API
    ADM -->|"HTTP / REST"| API

    %% CONEXÕES - API para Serviços
    API --> AUTH
    API --> QUEUE
    API --> SERVICE
    API --> METRICS

    %% CONEXÕES - Serviços internos
    QUEUE --> PRIORITY
    SERVICE --> PRIORITY
    PRIORITY --> QUEUE

    %% CONEXÕES - Serviços para Dados
    AUTH --> DB
    AUTH --> CACHE
    QUEUE --> DB
    PRIORITY --> DB
    SERVICE --> DB
    METRICS --> DB

    %% CONEXÕES - WebSocket
    API --> WS
    WS -->|"Atualizações em tempo real"| WEB
    WS -->|"Atualizações em tempo real"| ADM

    %% CONEXÕES - Infraestrutura
    DOCKER -.->|"Contém"| BACK
    DOCKER -.->|"Contém"| DB
    DOCKER -.->|"Contém"| CACHE
    COMPOSE -.->|"Orquestra"| DOCKER

    %% Estilos
    classDef client fill:#f0f0f0,stroke:#333,stroke-width:2px,color:#000
    classDef backend fill:#f8f8f8,stroke:#333,stroke-width:2px,color:#000
    classDef database fill:#f5f5f5,stroke:#333,stroke-width:2px,color:#000
    classDef infra fill:#f0f0f0,stroke:#333,stroke-width:2px,color:#000

    class CLIENT client
    class BACK backend
    class DATA database
    class INFRA infra
```

---

## 🛠️ Tecnologias a serem utilizadas

![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![Gin](https://img.shields.io/badge/Gin-008ECF?style=for-the-badge&logo=gin&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white)
![WebSocket](https://img.shields.io/badge/WebSocket-010101?style=for-the-badge&logo=socketdotio&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Docker Compose](https://img.shields.io/badge/Docker%20Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)

---

## Autor do projeto
*projeto orientado ao primeiro semestre da matéria de engenharia de software I*

**Yuri Duarte Kerber Alves da Silva**

[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github)](https://github.com/yuridkerber)
[![Gmail](https://img.shields.io/badge/Gmail-181717?style=for-the-badg&logo=gmail)](https://github.com/yuridkerber)

---

<p align="center">
  <strong>QFlow — Transformando filas em fluxos inteligentes.</strong>
</p>
