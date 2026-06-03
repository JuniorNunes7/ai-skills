# Code Reviewer

Skill para auxiliar revisão de código em pull requests, independente da linguagem.

Ela foi desenhada para ajudar o usuário a revisar PRs com mais clareza: entender riscos, explicar pontos complexos de forma objetiva, respeitar padrões do projeto e publicar comentários inline quando houver confirmação.

## O Que Ela Faz

- Lê PRs, diffs, arquivos alterados e discussões usando GitHub MCP.
- Busca contexto mínimo do projeto antes de criticar uma mudança.
- Avalia bugs, regressões, segurança, contratos, testes, manutenibilidade, SOLID e documentação.
- Respeita padrões existentes do projeto quando eles podem ser inferidos.
- Pergunta ao usuário quando uma decisão depende de contexto ou convenção ambígua.
- Produz uma revisão em Markdown ou publica comentários inline no GitHub, sempre com confirmação antes de publicar.
- Mantém memória compacta dentro da própria pasta da skill para preferências e decisões confirmadas.
- Sugere salvar memória de forma proativa quando o feedback do usuário revela uma preferência reutilizável.

## Estrutura

```text
code-reviewer/
├── README.md
├── SKILL.md
├── agents/
│   └── openai.yaml
├── memory/
│   └── .gitignore
└── references/
    ├── context-policy.md
    ├── memory-policy.md
    ├── output-policy.md
    └── review-rubric.md
```

## Arquivos Principais

- [`SKILL.md`](SKILL.md): workflow principal da skill.
- [`agents/openai.yaml`](agents/openai.yaml): metadados do agent e dependência do GitHub MCP.
- [`references/review-rubric.md`](references/review-rubric.md): critérios de severidade e qualidade dos achados.
- [`references/context-policy.md`](references/context-policy.md): regras para buscar contexto de forma eficiente.
- [`references/output-policy.md`](references/output-policy.md): formato da revisão em Markdown e no GitHub.
- [`references/memory-policy.md`](references/memory-policy.md): política de memória local.

## Memória

A memória da skill fica sempre dentro da própria pasta da skill:

```text
code-reviewer/memory/<owner>__<repo>.json
```

Isso evita criar arquivos no repositório revisado e garante que a skill sempre saiba onde procurar preferências antes de começar uma revisão.

Os arquivos JSON de memória devem guardar apenas decisões duráveis e confirmadas. Eles não devem conter diffs, trechos de código, segredos, dados sensíveis ou fatos temporários de um PR.