# Diagrama de Casos de Uso - QFlow

## Visão Geral

Diagrama UML representando os casos de uso do QFlow, organizado por atores e funcionalidades do MVP.

```mermaid
graph LR
    subgraph Atores
        Cliente["👤 Cliente"]
        Atendente["👨‍💼 Atendente"]
        Admin["🛠️ Administrador"]
    end

    subgraph "Casos de Uso - Cliente"
        UC1["Entrar na fila"]
        UC2["Receber senha"]
        UC3["Consultar posição"]
        UC4["Visualizar tempo estimado"]
        UC5["Acompanhar status"]
    end

    subgraph "Casos de Uso - Atendente"
        UC6["Visualizar fila"]
        UC7["Chamar próximo"]
        UC8["Iniciar atendimento"]
        UC9["Finalizar atendimento"]
        UC10["Pausar atendimento"]
    end

    subgraph "Casos de Uso - Administrador"
        UC11["Criar fila"]
        UC12["Cadastrar atendente"]
        UC13["Configurar prioridades"]
        UC14["Visualizar métricas"]
    end

    subgraph "Motor de Decisão"
        UC15["Calcular prioridade"]
        UC16["Considerar tempo espera"]
        UC17["Considerar tipo serviço"]
        UC18["Determinar próximo"]
    end

    Cliente --> UC1
    Cliente --> UC2
    Cliente --> UC3
    Cliente --> UC4
    Cliente --> UC5

    Atendente --> UC6
    Atendente --> UC7
    Atendente --> UC8
    Atendente --> UC9
    Atendente --> UC10

    Admin --> UC11
    Admin --> UC12
    Admin --> UC13
    Admin --> UC14

    UC1 --> UC2
    UC7 --> UC18
    UC18 --> UC15
    UC18 --> UC16
    UC18 --> UC17
    UC6 -.->|usa| UC18
    UC8 -.->|gera dados| UC5
    UC9 -.->|gera dados| UC14

    style Cliente fill:#e1f5ff
    style Atendente fill:#fff3e0
    style Admin fill:#f3e5f5
```

---

## Descrição dos Casos de Uso

### 👤 Cliente

| Caso de Uso | Descrição |
|---|---|
| **Entrar na fila** | Cliente se posiciona na fila do atendimento |
| **Receber senha** | Sistema gera um número/código de identificação |
| **Consultar posição** | Cliente visualiza sua posição atual na fila |
| **Visualizar tempo estimado** | Sistema calcula e exibe o tempo de espera estimado |
| **Acompanhar status** | Cliente monitora em tempo real o status do seu atendimento |

### 👨‍💼 Atendente

| Caso de Uso | Descrição |
|---|---|
| **Visualizar fila** | Atendente vê a lista de pessoas aguardando |
| **Chamar próximo** | Atendente chama o próximo atendimento (conforme algoritmo) |
| **Iniciar atendimento** | Atendente inicia o atendimento do cliente |
| **Finalizar atendimento** | Atendente encerra o atendimento e registra informações |
| **Pausar atendimento** | Atendente coloca o atendimento em pausa/suspenso |

### 🛠️ Administrador

| Caso de Uso | Descrição |
|---|---|
| **Criar fila** | Admin cria uma nova fila de atendimento |
| **Cadastrar atendente** | Admin registra novos profissionais no sistema |
| **Configurar prioridades** | Admin define as regras de priorização (pesos e fatores) |
| **Visualizar métricas** | Admin acompanha indicadores de desempenho |

### 🧠 Motor de Decisão

| Caso de Uso | Descrição |
|---|---|
| **Calcular prioridade** | Avalia o nível de prioridade do cliente |
| **Considerar tempo espera** | Analisa quanto tempo o cliente está aguardando |
| **Considerar tipo serviço** | Verifica qual tipo de atendimento é necessário |
| **Determinar próximo** | Aplica algoritmo para definir próximo atendimento |

---

## Relacionamentos

- **Inclusão** (→): Indicam fluxo obrigatório entre casos de uso
- **Associação Tracejada** (-.->): Indicam uso ou dependência

### Fluxos Principais

1. **Entrada do Cliente**
   - Cliente → Entrar na fila → Receber senha

2. **Atendimento**
   - Atendente → Visualizar fila → Chamar próximo (usa Motor de Decisão) → Iniciar atendimento

3. **Encerramento**
   - Finalizar atendimento → Gera dados para Métricas e acompanhamento do Cliente

4. **Configuração (Admin)**
   - Criar fila → Cadastrar atendente → Configurar prioridades

