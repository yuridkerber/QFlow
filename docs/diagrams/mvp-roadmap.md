# Roadmap do MVP - QFlow

```mermaid
flowchart LR

    A["1️⃣ Fundação<br/><br/>• Repositório<br/>• Docker<br/>• Estrutura do projeto<br/>• PostgreSQL"]

    B["2️⃣ Usuários<br/><br/>• Cadastro<br/>• Login<br/>• JWT<br/>• Perfis<br/><br/>Cliente · Atendente · Admin"]

    C["3️⃣ Filas<br/><br/>• Criar fila<br/>• Entrar na fila<br/>• Sair da fila<br/>• Visualizar posição"]

    D["4️⃣ Motor de Priorização<br/><br/>• Tempo de espera<br/>• Prioridade<br/>• Tipo de atendimento<br/>• Regras configuráveis"]

    E["5️⃣ Atendimento<br/><br/>• Chamar próximo<br/>• Iniciar atendimento<br/>• Finalizar atendimento<br/>• Atualizar fila"]

    F["6️⃣ Tempo Real<br/><br/>• WebSocket<br/>• Atualização de posição<br/>• Status da fila<br/>• Notificações"]

    G["7️⃣ Métricas<br/><br/>• Tempo médio de espera<br/>• Atendimentos realizados<br/>• Tamanho da fila<br/>• Histórico"]

    H["🚀 MVP<br/><br/>QFlow funcional"]

    A --> B --> C --> D --> E --> F --> G --> H
```

---

### MVP Final
Ao concluir todas as etapas, o projeto entrega uma primeira versão funcional do QFlow, capaz de demonstrar o valor central do sistema: organizar e otimizar filas por regras inteligentes, em vez de priorizar apenas a ordem de chegada.

---
