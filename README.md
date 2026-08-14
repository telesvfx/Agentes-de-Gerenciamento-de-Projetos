# Gerenciamento de Projetos Agentes

## Visao executiva

Este projeto implementa um time de agentes especializados em gestao de projetos dentro do Copilot CLI. O objetivo é transformar pedidos em entregas praticas, com combinacao de especialistas para aumentar qualidade, velocidade e consistencia.

### Como o projeto funciona (resumo executivo)

1. O usuario envia um pedido (texto, notas ou especificacao).
2. O **Orchestrator** classifica o pedido e escolhe um modo de operacao:
   - **Modo Rapido**: 1 agente para tarefa objetiva.
   - **Modo Time**: 2 a 4 agentes para pedidos multifuncionais (padrao).
   - **Modo Profundo**: time completo com revisao cruzada para decisoes criticas.
3. O Orchestrator delega para os especialistas adequados.
4. Cada especialista produz sua parte seguindo regras e templates proprios.
5. O Orchestrator revisa, integra e entrega uma resposta unica e priorizada.

### Agentes e responsabilidade de negócio

| Agente | Foco de negocio |
|---|---|
| **Orchestrator** | Triagem, delegacao, integracao e controle de qualidade da entrega final |
| **Senior Project Manager** | Quebrar especificacoes em tarefas de desenvolvimento acionaveis |
| **Project Shepherd** | Coordenacao entre times, cronograma, riscos e stakeholders |
| **Meeting Notes Specialist** | Estruturar reunioes em decisoes, acoes e pendencias |
| **Studio Operations** | Eficiencia operacional, processos internos e padronizacao |
| **Studio Producer** | Estrategia de portfolio, prioridades e alocacao de recursos |
| **Experiment Tracker** | Testes A/B, validacao de hipoteses e decisoes orientadas a dados |

### Valor esperado

- Decisoes mais claras e rastreaveis.
- Menos retrabalho por falta de alinhamento.
- Planos com priorizacao, risco e responsaveis explicitos.
- Melhor conexao entre estrategia, operacao e execucao.

## Visao tecnica

### Estrutura do repositorio

```text
Gerenciamento de Projetos - Agentes
├── agents/      # Definicoes dos agentes (.agent.md)
├── skills/      # Skills reutilizaveis (cada uma em sua pasta com SKILL.md)
├── docs/        # Documentacao de uso
└── resultado/   # Entregas geradas em markdown
AGENTS.md        # Regras globais de funcionamento
```

### Arquitetura de agentes

- Cada agente e definido em `Gerenciamento de Projetos - Agentes/agents/*.agent.md` com:
  - `name`, `description`, estilo, regras, templates e workflow.
  - lista de skills relacionadas para acionar quando fizer sentido.
- O Orchestrator funciona como camada de coordenacao:
  - escolhe o modo de profundidade;
  - define quais especialistas entram;
  - revisa saidas;
  - integra convergencias e resolve divergencias.

### Skills disponiveis

| Skill | Funcao principal | Agentes que tendem a usar |
|---|---|---|
| `interview-me` | Clarificar pedidos ambiguos pergunta por pergunta | Senior Project Manager, Project Shepherd |
| `spec-driven-development` | Transformar ideia vaga em especificacao clara | Senior Project Manager |
| `planning-and-task-breakdown` | Quebrar escopo em tarefas ordenadas e dependencias | Senior Project Manager, Project Shepherd |
| `idea-refine` | Refinar ideias e hipoteses antes de executar | Project Shepherd, Studio Producer, Experiment Tracker |
| `documentation-and-adrs` | Registrar decisoes importantes como referencia | Meeting Notes Specialist, Project Shepherd, Studio Operations, Studio Producer, Experiment Tracker |
| `doubt-driven-development` | Revisao critica de conclusoes antes de aceitar | Orchestrator, Experiment Tracker |
| `using-agent-skills` | Meta-skill para descoberta e acionamento de skills | Orchestrator |

### Fluxo tecnico padrao

1. **Entrada**: prompt do usuario (com ou sem arquivo de contexto).
2. **Classificacao**: Orchestrator identifica natureza da demanda.
3. **Delegacao**: especialistas sao acionados na ordem adequada ao problema.
4. **Revisao de qualidade**: verificacao de aderencia ao pedido e ao template.
5. **Sintese**: consolidacao em uma entrega unica, com plano priorizado.
6. **Persistencia**: entrega salva em markdown em pasta de resultado.

### Regras operacionais importantes

- Projeto executa localmente (sem fluxo obrigatorio de GitHub/Jira para operar).
- Entregas finais devem ser persistidas como `.md`.
- O sistema privilegia especializacao por papel e integracao por orquestracao.
- O objetivo nao e apenas responder, mas gerar artefatos reutilizaveis.

## Quando usar cada agente direto (sem orquestracao)

- Use **Meeting Notes Specialist** para atas e resumos de reuniao.
- Use **Senior Project Manager** para converter especificacao em backlog de execucao.
- Use **Experiment Tracker** para hipoteses, metricas e validacao experimental.
- Use **Project Shepherd** para cronogramas e coordenacao cross-funcional.
- Use **Studio Operations** para processos internos e eficiencia diaria.
- Use **Studio Producer** para decisoes de portfolio e alinhamento estrategico.

## Importante 

-Crie uma pasta .github e coloque os arquivos que estão dentro de "Gerenciamento de Projetos - Agentes"  em .github para que a ativação dos agentes de certo, a estrutura ficaria:

```text
Gerenciamento de Projetos - Agentes (arquivo principal do projeto)
.github (nova pasta que precisa adicionar)
   ├── agents/      # Definicoes dos agentes (.agent.md)
   ├── skills/      # Skills reutilizaveis (cada uma em sua pasta com SKILL.md)
   ├── docs/        # Documentacao de uso
   └── resultado/   # Entregas geradas em markdown
   AGENTS.md        # Regras globais de funcionamento
```

## Conclusao

Este projeto e um sistema de gestao de projetos orientado a agentes especializados, com governanca central pelo Orchestrator, uso seletivo de skills e producao de artefatos estruturados em markdown. A combinacao da visao executiva (decisao e alinhamento) com a visao tecnica (estrutura, fluxo e padroes) permite escalar a qualidade das entregas sem perder foco no contexto de negocio.
