# Skills

Cada skill fica em sua própria subpasta aqui dentro, seguindo o padrão:

```
.github/skills/<nome-da-skill>/
├── SKILL.md        # obrigatório — nome deve bater com a pasta
├── scripts/        # scripts executáveis (opcional)
├── references/     # docs carregados sob demanda (opcional)
└── assets/         # templates, boilerplate (opcional)
```

## Formato do SKILL.md

```markdown
---
name: nome-da-skill
description: 'O que a skill faz e quando usar. Máx. 1024 caracteres.'
---

# Nome da Skill

## Quando usar
- Gatilho 1
- Gatilho 2

## Procedimento
1. Passo 1
2. Passo 2
```

## Regras importantes
- `name` (1-64 caracteres, minúsculo, hífens) deve ser idêntico ao nome da pasta.
- `description` é a principal forma de descoberta pelo agente — inclua palavras-chave e o padrão "Use quando...".
- Mantenha o `SKILL.md` enxuto (menos de 500 linhas); use `references/` para conteúdo extenso.
- Referencie arquivos auxiliares com caminhos relativos (`./scripts/...`, `./references/...`).

Os agentes em `.github/agents/*.agent.md` carregam skills automaticamente quando a `description` da skill combina com a tarefa.

## Skills curadas para os agentes de gestão de projetos

Este projeto reúne skills de fontes diversas; nem todas se aplicam a um time de agentes de gestão de projetos (várias são de engenharia de software pura, como frontend, testes automatizados, CI/CD e hardening de segurança de código). As skills abaixo foram avaliadas como relevantes e mapeadas para os agentes:

| Skill | Usada por |
|---|---|
| `interview-me` | Senior Project Manager, Project Shepherd |
| `spec-driven-development` | Senior Project Manager |
| `planning-and-task-breakdown` | Senior Project Manager, Project Shepherd |
| `idea-refine` | Project Shepherd, Studio Producer, Experiment Tracker |
| `documentation-and-adrs` | Meeting Notes Specialist, Project Shepherd, Studio Operations, Studio Producer, Experiment Tracker |
| `doubt-driven-development` | Orchestrator, Experiment Tracker |
| `using-agent-skills` | Orchestrator (meta — garante que a descoberta de skills funcione) |

As skills não são acionadas em toda tarefa — só quando o próprio agente julga que agregam valor.

As pastas `file-to-markdown/` e `git-workflow-and-versioning/` estão vazias (sem `SKILL.md`), portanto não são carregadas. Elas não se aplicam a este time — `git-workflow-and-versioning` inclusive contraria a regra do `AGENTS.md` (não gerar comandos de versionamento) e `file-to-markdown` contraria a regra do Orchestrator (não converter arquivos automaticamente). Recomenda-se removê-las para reduzir ruído.
