# Quality Checklists

## VISION checklist

- [ ] O problema está descrito em linguagem de usuário, sem solução técnica
- [ ] Os usuários principais e suas necessidades estão identificados
- [ ] Há de 3 a 5 resultados do MVP, cada um observável
- [ ] O que fica fora do MVP está explícito
- [ ] Há ao menos uma métrica ou sinal de sucesso
- [ ] Restrições conhecidas foram registradas
- [ ] Todo conteúdo veio do usuário ou de recomendações que ele confirmou; lacunas estão em "Questões em aberto"
- [ ] O "Registro de decisões" cobre cada pergunta resolvida, com origem e justificativa
- [ ] O texto é autossuficiente, sem formato de pergunta e resposta

## ADR checklist

- [ ] Todas as decisões que bloqueiam o MVP têm ADR aceito ou adiado com justificativa
- [ ] Cada ADR trata de um assunto só
- [ ] Cada ADR tem ao menos 2 opções com prós e contras
- [ ] A recomendação está justificada pela VISION ou pelas restrições
- [ ] A decisão final foi tomada pelo usuário
- [ ] Restrições do ambiente (`CLAUDE.md`, devcontainer) foram respeitadas

## ROADMAP checklist

- [ ] A primeira feature é `fundacao-projeto`
- [ ] Todo resultado do MVP é atendido por ao menos uma feature
- [ ] Nenhuma feature está fora do escopo do MVP
- [ ] Cada feature tem nome `kebab-case`, objetivo e dependências
- [ ] As features são fatias verticais demonstráveis, não camadas técnicas
- [ ] A ordem respeita as dependências

## PROJECT-CONTEXT checklist

- [ ] Explica claramente o que o produto faz
- [ ] Resume stack e ferramentas principais
- [ ] Registra convenções importantes do projeto
- [ ] Inclui regras de domínio que se repetem entre features
- [ ] Não contém detalhes descartáveis de uma única feature
- [ ] Está curto o suficiente para ser consultado rapidamente

## PRD checklist

- [ ] O contexto de produto está descrito (cenário atual e motivação)
- [ ] O problema está claro e concreto
- [ ] O objetivo é compreensível e observável
- [ ] Há ao menos uma história de usuário no formato "Como / quero / para"
- [ ] Cada história tem critérios de aceite verificáveis (sim/não ou mensuráveis)
- [ ] O escopo diz o que entra e o que fica de fora
- [ ] O fluxo esperado está descrito de forma simples
- [ ] Não há excesso de detalhe técnico que deveria ir para a SPEC

## SPEC checklist

- [ ] A SPEC reflete corretamente o PRD aprovado (em `fundacao-projeto`: reflete os ADRs aceitos)
- [ ] A história, tarefa ou solicitação do usuário está clara
- [ ] A necessidade do usuário ou negócio está clara
- [ ] O problema e o objetivo técnico estão claros
- [ ] O estado atual foi descrito com base no código real (em projeto novo: "sem código" ou o que a fundação vai criar, marcado como planejado)
- [ ] O escopo do que muda e do que não muda está explícito
- [ ] Os requisitos funcionais estão explícitos e rastreáveis
- [ ] Restrições, pressupostos e edge cases relevantes foram registrados
- [ ] Os arquivos afetados fazem sentido para a solução
- [ ] Contratos, dados e interfaces relevantes foram descritos
- [ ] Alternativas e trade-offs foram documentados quando a decisão não é óbvia
- [ ] Há detalhes suficientes para implementar sem suposições críticas
- [ ] Requisitos não funcionais relevantes foram considerados
- [ ] Rollout, fallback, migração e observabilidade foram cobertos quando aplicável
- [ ] Os critérios de aceite são verificáveis
- [ ] Há estratégia clara de validação
- [ ] Riscos e observações relevantes foram registrados

## Regras de qualidade da SPEC

- Sempre referenciar código real quando houver implementação existente
- Em projeto novo, referenciar os ADRs e seguir as convenções do PROJECT-CONTEXT nos arquivos a criar
- Sempre começar com a história, tarefa ou motivação do usuário
- Sempre explicitar o que está fora do escopo
- Sempre manter o documento focado no problema e nas decisões úteis
- Sempre separar requisitos funcionais de requisitos não funcionais
- Sempre manter critérios de aceite objetivos
- Sempre cobrir edge cases e comportamentos de erro relevantes
- Sempre descrever impacto por arquivo ou área
- Sempre registrar restrições e pressupostos que moldam a solução
- Sempre registrar trade-offs quando houver múltiplos caminhos plausíveis
- Nunca depender de ambiguidades para implementar
- Nunca propor refatorações paralelas sem necessidade clara
- Sempre diferenciar contexto funcional do PRD e detalhe técnico da SPEC

## Regras de projeto novo

Aplicam-se às SPECs geradas durante ou logo após o Bootstrap:

- `fundacao-projeto` não tem PRD: os itens de aderência ao PRD são avaliados contra os ADRs aceitos.
- "Estado atual" pode ser "repositório sem código", desde que liste o que já existe (devcontainer, `CLAUDE.md` etc.).
- "Referências ao código real" é substituído por: arquivos a criar seguem as convenções do PROJECT-CONTEXT e dos ADRs.
- Rollout e migração podem ser "não se aplica" quando não houver dados nem usuários em produção.
- Toda decisão técnica citada na SPEC deve apontar para um ADR aceito; se não houver, abrir novo ADR antes.

## Regras das tasks

1. Cada task deve ser granular e executável.
2. Dependências devem ser explícitas.
3. Sempre incluir uma task final de verificação e2e.
4. Tasks não substituem a SPEC.
5. Não criar task apenas para documentação.
