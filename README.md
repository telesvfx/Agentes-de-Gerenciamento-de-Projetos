# Como Funciona o Sistema de Agentes de Gestão de Projetos

Este documento explica o sistema em duas camadas:

1. **Visão executiva** — para quem quer entender rapidamente o valor e o papel de cada agente.
2. **Visão técnica** — para quem precisa entender como os agentes, habilidades e regras se conectam.

---

## 1) Visão executiva

### O que este sistema faz

Este ambiente funciona como um **time de especialistas em inteligência artificial** para apoiar gestão de projetos. Em vez de uma única resposta genérica, o sistema encaminha cada pedido para o agente mais adequado e devolve uma entrega mais clara, organizada e fácil de usar.

O resultado prático é:
- menos retrabalho;
- decisões mais rápidas;
- documentação mais organizada;
- melhor alinhamento entre estratégia, operação e execução.

### Quem faz o quê

| Agente | Nome original | Função principal | Quando usar |
|---|---|---|---|
| **Agente Coordenador** | Orchestrator | Recebe o pedido, entende a necessidade, escolhe os especialistas certos e confere a qualidade da resposta final. | Sempre. É o ponto de entrada. |
| **Gerente Sênior de Projetos** | Senior Project Manager | Converte uma ideia ou especificação em uma lista de tarefas claras, com ordem de execução e dependências. | Quando o pedido precisa virar plano de trabalho. |
| **Pastor de Projetos** | Project Shepherd | Organiza cronograma, riscos, responsáveis e comunicação entre áreas ou pessoas. | Quando o projeto envolve vários times ou dependências. |
| **Especialista em Atas de Reunião** | Meeting Notes Specialist | Extrai decisões, ações e pendências de reuniões ou transcrições. | Depois de reuniões importantes. |
| **Operações do Estúdio** | Studio Operations | Melhora processos, rotinas, padrões e eficiência operacional. | Quando o foco é organização e produtividade do dia a dia. |
| **Produtor Estratégico** | Studio Producer | Apoia decisões de alto nível, prioridades e alocação de recursos. | Quando a decisão é executiva ou de portfólio. |
| **Acompanhador de Experimentos** | Experiment Tracker | Estrutura testes, acompanha métricas e ajuda a validar hipóteses com dados. | Quando é preciso testar antes de escalar. |

### Como ele trabalha na prática

1. Você faz um pedido em linguagem natural.
2. O **Agente Coordenador** identifica o tipo de necessidade.
3. Ele aciona um ou mais especialistas.
4. Cada agente entrega sua parte.
5. O coordenador revisa, consolida e devolve a resposta final.
6. O material final é salvo em `.md` dentro de `resultado/`.

### Exemplo simples

Pedido: **“Preciso planejar o lançamento de um novo produto com três times envolvidos.”**

Leitura executiva:
- o **Produtor Estratégico** avalia a direção e a prioridade;
- o **Pastor de Projetos** organiza cronograma, riscos e alinhamento entre áreas;
- o **Operações do Estúdio** ajuda a desenhar a rotina e os processos;
- o **Agente Coordenador** junta tudo em uma resposta única.

### Em linguagem de negócio

Este sistema serve para transformar pedidos soltos em entregas úteis. Ele ajuda a responder perguntas como:
- vale a pena fazer este projeto?
- quem precisa participar?
- qual é a ordem certa?
- quais são os riscos?
- como isso vira execução real?

---

## 2) Visão técnica

### Arquitetura geral

O sistema é organizado em três camadas:

1. **Entrada**
   - o usuário escreve o pedido no Copilot CLI;
   - o pedido chega ao **Agente Coordenador**.

2. **Delegação**
   - o coordenador identifica o tipo de tarefa;
   - chama os agentes especializados adequados;
   - passa contexto de um agente para o outro quando necessário.

3. **Síntese final**
   - o coordenador revisa o resultado;
   - corrige incoerências;
   - entrega uma resposta consolidada;
   - salva o arquivo final em `resultado/`.

### Fluxo técnico

```text
Usuário
  ↓
Agente Coordenador
  ↓
Seleção do especialista correto
  ↓
Execução do agente especializado
  ↓
Revisão de qualidade
  ↓
Síntese final
  ↓
Arquivo .md salvo em resultado/
```

### Papel técnico de cada agente

#### Agente Coordenador (Orchestrator)
- Faz a triagem inicial do pedido.
- Decide se o trabalho é melhor em modo rápido, em time ou em modo profundo.
- Encaminha para os agentes corretos.
- Faz controle de qualidade da saída.
- Evita respostas genéricas ou incompletas.

#### Gerente Sênior de Projetos (Senior Project Manager)
- Lê especificações e pedidos.
- Transforma requisitos em tarefas executáveis.
- Organiza dependências e critérios de aceitação.
- Mantém o escopo realista.

#### Pastor de Projetos (Project Shepherd)
- Trabalha na coordenação entre áreas.
- Planeja cronogramas e pontos de controle.
- Identifica riscos e dependências.
- Ajuda a manter alinhamento entre stakeholders.

#### Especialista em Atas de Reunião (Meeting Notes Specialist)
- Extrai decisões, ações e dúvidas abertas.
- Estrutura atas em formato padronizado.
- Não inventa informações ausentes.
- É o agente mais mecânico e direto do time.

#### Operações do Estúdio (Studio Operations)
- Documenta e melhora processos operacionais.
- Cria procedimentos padrão.
- Apoia rotina, eficiência e organização interna.
- Registra mudanças de processo quando necessário.

#### Produtor Estratégico (Studio Producer)
- Atua em decisões de nível executivo.
- Ajuda a priorizar iniciativas e alocar recursos.
- Analisa valor de portfólio e direção estratégica.
- Conecta visão de negócio com execução.

#### Acompanhador de Experimentos (Experiment Tracker)
- Estrutura hipóteses e testes.
- Define métricas e critérios de sucesso.
- Acompanha resultados e validações.
- Sustenta decisões com evidência.

### Habilidades do sistema

As **habilidades** são módulos especializados que os agentes acionam quando a tarefa pede um tipo específico de raciocínio ou estrutura.

| Habilidade | Quando entra em cena | O que faz |
|---|---|---|
| `interview-me` | Quando o pedido está vago ou incompleto | Faz uma pergunta por vez para esclarecer o objetivo. |
| `spec-driven-development` | Quando a ideia ainda precisa ser formalizada | Organiza a especificação antes da execução. |
| `planning-and-task-breakdown` | Quando já existe clareza e é preciso executar | Quebra o trabalho em tarefas ordenadas. |
| `idea-refine` | Quando a ideia ainda está solta ou mal definida | Refina a proposta até ela ficar mais sólida. |
| `documentation-and-adrs` | Quando existe uma decisão importante a registrar | Formaliza contexto, decisão e razão. |
| `doubt-driven-development` | Quando uma conclusão precisa ser criticada com rigor | Faz revisão adversarial para reduzir erro. |
| `using-agent-skills` | Quando é preciso orquestrar o uso das habilidades | Ajuda o agente a escolher a habilidade certa. |

### Modos de operação

#### Modo Rápido
- Usado quando existe um especialista óbvio.
- Exemplo: resumir reunião.
- Normalmente envolve um agente só.

#### Modo Time
- Usado quando o pedido cruza áreas diferentes.
- Exemplo: planejar um lançamento.
- Envolve dois a quatro agentes em sequência.

#### Modo Profundo
- Usado quando a decisão é estratégica ou sensível.
- Exemplo: avaliar um novo investimento.
- Envolve vários agentes e revisão cruzada.

### Sequência recomendada de delegação

Quando há mais de um agente, a ordem sugerida é:

1. **Produtor Estratégico**
2. **Pastor de Projetos**
3. **Operações do Estúdio**
4. **Gerente Sênior de Projetos**
5. **Acompanhador de Experimentos**

Nem todo pedido usa todos eles. A lógica é simples:

- primeiro define-se a direção;
- depois se organiza a coordenação;
- depois se ajusta a operação;
- depois se detalha a execução;
- por fim, valida-se com dados, se isso fizer sentido.

### Regras de qualidade

O **Agente Coordenador** só aceita a entrega final se ela:

- responder ao que foi pedido;
- estiver no formato esperado;
- não inventar requisitos;
- não deixar etapas críticas de fora;
- usar as habilidades certas quando necessário.

Se a resposta vier fraca, o coordenador devolve ao agente responsável para refazer.

### Saída obrigatória

Toda entrega final deve ser salva como arquivo `.md` em `resultado/`, com nome descritivo e em português sempre que possível.

Exemplos:
- `resultado/ata-discovery-geral-2026-08-11.md`
- `resultado/como-funciona-o-sistema.md`
- `resultado/plano-lancamento-produto.md`

### Resumo técnico curto

| Item | Descrição |
|---|---|
| **Entrada** | Pedido em linguagem natural |
| **Roteamento** | Feito pelo Agente Coordenador |
| **Execução** | Feita por agentes especialistas |
| **Controle de qualidade** | Feito antes da resposta final |
| **Persistência** | Arquivos `.md` salvos em `resultado/` |

---

## 3) Resumo final

Este sistema existe para transformar pedidos de gestão de projetos em entregas úteis, organizadas e fáceis de reutilizar.

Na prática:
- o **executivo** entende o valor rapidamente;
- o **time técnico** entende a lógica por trás;
- o **Agente Coordenador** garante que a resposta final não fique solta nem genérica.

**Localização do documento:** `resultado/como-funciona-o-sistema.md`
