# Diagrama de Arquitetura - QFlow

## Visão Geral da Arquitetura

Arquitetura em camadas do QFlow, mostrando a interação entre Cliente, Backend, Banco de Dados e Infraestrutura.

```mermaid
flowchart TB
    %% CLIENTES
    subgraph CLIENT["🖥️ Clientes"]
        WEB["Frontend Web<br/>React + TypeScript"]
        ADM["Painel Administrativo<br/>React + TypeScript"]
    end

    %% BACKEND
    subgraph BACK["⚙️ Backend — Go"]
        API["API REST<br/>Gin Framework"]
        AUTH["🔐 Autenticação<br/>JWT + bcrypt"]
        QUEUE["📋 Serviço de Filas<br/>Gerenciamento de filas"]
        PRIORITY["🧠 Motor de Priorização<br/>Algoritmo de decisão"]
        SERVICE["🎫 Serviço de Atendimento<br/>Controle de atendimentos"]
        METRICS["📊 Serviço de Métricas<br/>Relatórios e KPIs"]
        WS["🔄 WebSocket<br/>Real-time"]
    end

    %% DATABASE
    subgraph DATA["🗄️ Persistência"]
        DB[("PostgreSQL<br/>Banco de Dados")]
        CACHE["Redis<br/>Cache & Sessions"]
    end

    %% INFRA
    subgraph INFRA["📦 Infraestrutura"]
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
    classDef client fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef backend fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef database fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef infra fill:#e8f5e9,stroke:#388e3c,stroke-width:2px

    class CLIENT client
    class BACK backend
    class DATA database
    class INFRA infra
```

---

## Componentes da Arquitetura

### Camada Cliente

| Componente | Tecnologia | Responsabilidade |
|---|---|---|
| **Frontend Web** | React + TypeScript | Interface para Cliente e Atendente |
| **Painel Administrativo** | React + TypeScript | Interface para Administrador |

### Camada Backend

| Componente | Tecnologia | Responsabilidade |
|---|---|---|
| **API REST** | Go + Gin Framework | Orquestra requisições HTTP e roteia para serviços |
| **Autenticação** | JWT + bcrypt | Valida credenciais, gera tokens, protege rotas |
| **Serviço de Filas** | Go | Cria, gerencia e organiza filas de atendimento |
| **Motor de Priorização** | Go | Calcula prioridade e determina próximo atendimento |
| **Serviço de Atendimento** | Go | Controla ciclo de vida do atendimento |
| **Serviço de Métricas** | Go | Coleta dados e gera relatórios/KPIs |
| **WebSocket** | Go | Envia atualizações em tempo real aos clientes |

### Camada de Persistência

| Componente | Tecnologia | Responsabilidade |
|---|---|---|
| **Banco de Dados** | PostgreSQL | Armazena dados persistentes (usuários, filas, atendimentos) |
| **Cache** | Redis | Armazena sessões, cache de operações frequentes |

### Camada de Infraestrutura

| Componente | Tecnologia | Responsabilidade |
|---|---|---|
| **Docker** | Docker | Containeriza aplicações para portabilidade |
| **Docker Compose** | Docker Compose | Orquestra containers em ambiente local/desenvolvimento |

---

## Decisões Arquiteturais

| Decisão | Justificativa |
|---|---|
| **Go para Backend** | Performance, concorrência, deployment simples |
| **PostgreSQL** | Confiabilidade, ACID, escalabilidade, suporte a JSON |
| **Redis** | Cache rápido, sessões, pub/sub para real-time |
| **React** | Ecosistema maduro, comunidade grande, SPA reativo |
| **WebSocket** | Atualizações instantâneas da fila e posição |
| **Docker** | Portabilidade, consistência entre ambientes |
| **JWT** | Stateless, escalável, seguro |

