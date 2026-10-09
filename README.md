# Skills

Skills reutilizáveis para agentes de IA (Claude Code, Codex, Cursor, Copilot e outros compatíveis com o padrão `SKILL.md`), instaláveis via [`skills` CLI](https://skills.sh/).

## Instalação

Listar as skills disponíveis:

```bash
npx skills add luunando/skills --list
```

Instalar uma skill no projeto atual:

```bash
npx skills add luunando/skills --skill spec-driven-build
```

Instalar globalmente, sem prompts:

```bash
npx skills add luunando/skills --skill spec-driven-build -g -y
```

Sem CLI: clone o repositório e copie a pasta da skill para o diretório de skills do seu agente (ex.: `~/.claude/skills/`).

## Skills disponíveis

| Skill | Categoria | Descrição |
|---|---|---|
| [`spec-driven-build`](./skills/development/spec-driven-build/SKILL.md) | development | Orquestra PRD, SPEC e tasks com gates de qualidade e histórico por feature. Inclui bootstrap de projeto novo (visão por entrevista guiada, ADRs de stack, roadmap e feature de fundação). |

## Estrutura

```text
skills/
  <categoria>/
    <nome-da-skill>/
      SKILL.md
      references/   (opcional)
      templates/    (opcional)
      scripts/      (opcional)
      assets/       (opcional)
templates/
  skill-template/   ponto de partida para novas skills
```

Categorias: `development`, `design`, `productivity`, `others`.

## Contribuição

Veja [CONTRIBUTING.md](./CONTRIBUTING.md).

## Créditos

`spec-driven-build` é derivada de [jjeanjacques10/skills](https://github.com/jjeanjacques10/skills) (MIT). A licença original está em [`skills/development/spec-driven-build/LICENSE`](./skills/development/spec-driven-build/LICENSE). A técnica de entrevista do bootstrap se inspira nas skills `grilling` e `grill-me`.

## Licença

MIT. Veja [LICENSE](./LICENSE).
