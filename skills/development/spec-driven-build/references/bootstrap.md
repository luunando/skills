# Bootstrap — projeto do zero

Use este fluxo antes da Fase 1 do [workflow.md](workflow.md) quando o projeto ainda não tem código nem documentação.

## Detecção

Ative o Bootstrap quando **as duas** condições forem verdadeiras:

- Não existe código-fonte da aplicação (ignorar `.git/`, `docs/`, `.devcontainer/`, `.claude/`, `README.md`, `CLAUDE.md`, `LICENSE` e arquivos de configuração do editor).
- Não existe `docs/fundacao-projeto/SPEC.md` com status `Aprovada`.

Também ative quando o usuário disser explicitamente que é um projeto novo.

Se existe código mas não existe `docs/`, **não** use o Bootstrap: siga a Fase 1 normal e explore o código.

### Retomada

O Bootstrap pode ser interrompido. Ao reentrar, verifique o que já existe e retome a partir da primeira etapa incompleta:

| Existe | Próxima etapa |
|---|---|
| nada, ou `docs/VISION.md` com status `Rascunho` | B1 — Visão (se houver "Registro de decisões", continuar a entrevista a partir dele) |
| `docs/VISION.md` com status `Aprovado` | B2 — ADRs |
| `docs/adr/` com decisões aceitas | B3 — PROJECT-CONTEXT |
| `docs/PROJECT-CONTEXT.md` | B4 — Roadmap |
| `docs/ROADMAP.md` com status `Rascunho` | B4 — Roadmap (revisar e aprovar) |
| `docs/ROADMAP.md` com status `Aprovado` | B5 — Feature de fundação |
| `docs/fundacao-projeto/SPEC.md` sem tasks | B5 — aprovação da SPEC e tasks |

## Sequência

1. `docs/VISION.md`
2. `docs/adr/ADR-NNN-<decisao>.md`
3. `docs/PROJECT-CONTEXT.md`
4. `docs/ROADMAP.md`
5. `docs/fundacao-projeto/` (SPEC + tasks)
6. Fluxo normal (Fase 2 em diante) para cada feature do roadmap

Não avance para a próxima etapa enquanto a atual não estiver aprovada pelo usuário.

## B1 — Visão do produto (entrevista guiada)

### Objetivo

Registrar o que o produto é, para quem e qual é o MVP, antes de qualquer decisão técnica.

### Antes da entrevista

Criar `docs/VISION.md` a partir de [templates/vision-template.md](../templates/vision-template.md) **antes da primeira pergunta**, com `Status: Rascunho`, a data e a ideia como o usuário a descreveu na seção "Ponto de partida". Assim nada se perde se a sessão for interrompida.

### Durante a entrevista

1. **Uma pergunta por mensagem.** Esperar a resposta antes da próxima.
2. **Cada pergunta traz uma resposta recomendada**, marcada como sugestão, que o usuário confirma ou corrige.
3. **Percorrer a árvore de decisões:** resolver primeiro o que outras respostas dependem (ex.: usuários antes de resultados do MVP).
4. **Aprofundar respostas vagas.** "Todo mundo", "rápido", "várias funcionalidades" pedem um exemplo concreto, um número ou um perfil específico.
5. **Não perguntar o que dá para ler.** Se `README.md`, `CLAUDE.md` ou outro arquivo já responde, ler em vez de perguntar.
6. Perguntas-base, nesta ordem, pulando o que já foi respondido. São um roteiro mínimo; aprofundar conforme as respostas:
   1. Que problema o produto resolve e para quem?
   2. Quem são os usuários principais (perfis)?
   3. Como esse problema é resolvido hoje (alternativas, concorrentes, planilha, processo manual)?
   4. Quais são os 3 a 5 resultados que o MVP precisa entregar?
   5. O que fica explicitamente fora do MVP?
   6. Como saberemos que o MVP deu certo (métricas ou sinais)?
   7. Há restrições conhecidas (prazo, orçamento, time, compliance, infraestrutura obrigatória)?
7. **Após cada resposta resolvida**, acrescentar uma linha ao "Registro de decisões" do `docs/VISION.md`: pergunta, decisão, origem (`usuário` ou `recomendação aceita`), justificativa e alternativas descartadas. Registrar em silêncio, sem transformar uma pergunta em várias.
8. **Encerrar** quando todas as seções do template tiverem conteúdo confirmado ou quando o usuário pedir para parar. O que ficou sem resposta vai para "Questões em aberto".

### Depois da entrevista

1. **Passe de elaboração:** reescrever as seções do `docs/VISION.md` em texto autossuficiente, legível por quem não viu a conversa. Não deixar formato de pergunta e resposta. Manter o "Registro de decisões".
2. Validar com o VISION checklist e emitir o relatório de qualidade do Bootstrap (seção Visão).
3. Pedir aprovação: `A visão está correta? Posso seguir para as decisões técnicas?`
4. Só após aprovação explícita, mudar o status do arquivo para `Aprovado`.

### Regras

- A visão é de produto. Não citar stack, framework ou arquitetura aqui.
- Recomendar é obrigatório; decidir é do usuário. Recomendação não confirmada não entra no documento: vai para "Questões em aberto".
- Não inventar métricas, usuários ou funcionalidades.

## B2 — Decisões técnicas (ADRs)

### Objetivo

Escolher stack e arquitetura com alternativas e trade-offs visíveis, e registrar cada decisão.

### Procedimento

1. Ler `CLAUDE.md`, `.devcontainer/` e qualquer restrição de ambiente já existente. Restrições do ambiente (ex.: runtime disponível, banco compartilhado) entram como premissas, não como opções.
2. Listar as decisões necessárias para o MVP. Típicas:
   - linguagem e runtime
   - framework de backend/API
   - framework de UI (se houver)
   - banco de dados e modelagem
   - autenticação
   - estrutura do repositório (monorepo, pastas)
   - ferramentas de teste, lint e formatação
   - CI e estratégia de deploy
3. Agrupar decisões acopladas no mesmo ADR (ex.: runtime + framework). Um ADR por assunto.
4. Para cada ADR: apresentar 2 ou 3 opções com prós, contras e uma recomendação justificada pela VISION. Perguntar ao usuário qual opção escolher, **um ADR por mensagem**, seguindo as mesmas regras de entrevista do B1 (aprofundar respostas vagas, resolver dependências primeiro).
5. Registrar a escolha em `docs/adr/ADR-NNN-<decisao>.md` usando [templates/adr-template.md](../templates/adr-template.md), com status `Aceito`.
6. Decisões que não bloqueiam o MVP podem ficar com status `Adiado` e aparecer como "a definir" no PROJECT-CONTEXT.
7. Validar com o ADR checklist e emitir o relatório (seção Decisões técnicas).

### Regra

Nunca decidir pelo usuário. Recomendar é obrigatório; escolher é do usuário.

## B3 — PROJECT-CONTEXT a partir das decisões

1. Criar `docs/PROJECT-CONTEXT.md` com [templates/project-context-template.md](../templates/project-context-template.md).
2. Preencher a partir da VISION e dos ADRs aceitos, não da exploração de código.
3. Marcar cada item da stack e das convenções como `decidido (ADR-NNN)` ou `a definir`.
4. Validar com o PROJECT-CONTEXT checklist.

## B4 — Roadmap do MVP

### Objetivo

Quebrar o MVP em features pequenas, ordenadas e com dependências explícitas, para alimentar o fluxo normal.

### Procedimento

1. Derivar as features dos resultados do MVP na VISION.
2. Cada feature deve ter nome `kebab-case`, objetivo em uma linha, dependências e qual resultado da VISION atende.
3. A primeira feature é sempre `fundacao-projeto`.
4. Ordenar por dependência e valor; indicar o que pode ser feito em paralelo.
5. Criar `docs/ROADMAP.md` com [templates/roadmap-template.md](../templates/roadmap-template.md).
6. Validar com o ROADMAP checklist, emitir o relatório (seção Roadmap) e pedir aprovação.
7. Só após aprovação explícita, mudar o status do arquivo para `Aprovado`.

### Regra

Prefira fatias verticais (do usuário ao banco) a camadas horizontais ("criar todos os models"). Cada feature deve ser demonstrável sozinha.

## B5 — Feature de fundação

### Objetivo

Deixar o repositório pronto para receber features: estrutura, build, testes, lint, CI e configuração de ambiente.

### Procedimento

1. Criar `docs/fundacao-projeto/` e `docs/fundacao-projeto/tasks/`.
2. **Não gerar PRD** para esta feature: ela não tem história de usuário. A origem dos requisitos são os ADRs aceitos.
3. Gerar `docs/fundacao-projeto/SPEC.md` com o template de SPEC, adaptando:
   - Seção 1: origem = ADRs (listar quais).
   - Seção 3 (Estado atual): "Repositório sem código" e o que já existe (devcontainer, `CLAUDE.md` etc.).
   - Seção 10 (Arquivos afetados): estrutura a criar, seguindo as convenções dos ADRs.
4. A SPEC deve cobrir no mínimo:
   - estrutura de pastas e entrypoint da aplicação
   - gerenciador de dependências e scripts (`dev`, `build`, `test`, `lint`)
   - configuração de ambiente via variáveis (ex.: `.env.example`), sem credenciais no código
   - test runner com um teste de fumaça
   - lint e formatação
   - pipeline de CI rodando lint e testes
   - healthcheck ou comando mínimo que prove que a aplicação sobe
5. Adicionar `Status: Rascunho` logo abaixo do título da SPEC. Validar com o SPEC checklist aplicando as "Regras de projeto novo" de [quality-checklists.md](quality-checklists.md), emitir o relatório e pedir aprovação. Após aprovação explícita, mudar para `Status: Aprovada`.
6. Após aprovação, gerar as tasks como na Fase 6 do workflow, terminando em `TASK-N-verificacao-e2e.md` (aplicação sobe, teste de fumaça passa, CI verde).
7. Preencher a seção "Comandos" de `docs/PROJECT-CONTEXT.md` com os comandos definidos na SPEC (dev, build, testes, lint).

## Saída do Bootstrap

Ao final, apresentar:

- `docs/VISION.md`
- `docs/adr/`
- `docs/PROJECT-CONTEXT.md`
- `docs/ROADMAP.md`
- `docs/fundacao-projeto/SPEC.md` e `tasks/`
- próxima feature sugerida do roadmap

Depois, para cada feature do roadmap, seguir o fluxo normal a partir da Fase 0 do workflow (nome já definido no roadmap) e Fase 2 (PRD). Enquanto a fundação não estiver implementada, a seção "Estado atual" das SPECs deve citar o que a SPEC de fundação vai criar, marcado como "planejado".
