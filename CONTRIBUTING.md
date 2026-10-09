# Contribuindo

## Nova skill

1. Copie `templates/skill-template/` para `skills/<categoria>/<nome-da-skill>/`.
2. Nome da pasta em `kebab-case`, igual ao `name` do frontmatter.
3. `SKILL.md` começa com frontmatter YAML contendo `name` e `description`.
4. A `description` diz o que a skill faz **e quando usar**: é o gatilho de ativação do agente.
5. Conteúdo longo vai para `references/`; artefatos reutilizáveis para `templates/`; helpers determinísticos para `scripts/`.
6. Adicione a skill na tabela do `README.md`.

## Skill derivada de terceiros

- Confirme que a licença permite redistribuição.
- Mantenha a licença original dentro da pasta da skill e registre a origem em "Créditos" no `README.md`.

## Checklist de PR

- [ ] Estrutura de pastas segue o padrão
- [ ] Frontmatter válido com `name` e `description`
- [ ] Links para `references/`, `templates/`, `scripts/` e `assets/` resolvem
- [ ] `npx skills add ./ --list` lista a skill
- [ ] README atualizado
