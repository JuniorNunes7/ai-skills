# Output Policy

## Choose Output
For each PR, ask whether the user wants a Markdown draft or a GitHub review.

Prefer GitHub inline comments for actionable findings with exact diff lines. Never publish to GitHub without explicit confirmation.

## Markdown Draft
Use this format:

```markdown
# Revisão do PR
## Achados
### [major] path/to/file.ext:123
Problema claro e objetivo.
Impacto: por que isso importa.
Sugestão: ação concreta.
## Perguntas
- Pergunta necessária para julgar uma decisão ambígua.
## Resumo
Breve síntese do risco geral e lacunas de teste/contexto.
```

When the PR description or accessible task context is absent or insufficient, make the summary state directly what the diff changed and any access limitation. When documented scope and implementation agree, a separate scope summary is unnecessary.

Put architectural uncertainties in `Perguntas` when the user has not answered them yet. Do not present them as defects unless project evidence or the user's answer supports that conclusion.

If there are no meaningful findings, write:

```markdown
# Revisão do PR
Nenhum problema relevante encontrado no contexto analisado.
Risco residual: descreva lacunas de teste, limitações de contexto ou validações não executadas.
```

## GitHub Review
Use inline comments for findings that map to a changed diff line.

Publish through the GitHub review API with inline file comments. Use a normal `COMMENT` review unless the user explicitly asks to request changes. For blocker findings, recommend requesting changes in the body and ask before using a stricter action.

Each inline comment should be self-contained:

```text
**[major]**
Este caminho não trata X. Se Y ocorrer, Z quebra. 
**Sugestão:** validar A antes de chamar B ou cobrir esse caso no fluxo C.
```

Use the review body for:

- Overall summary.
- Findings without exact diff line.
- Questions that affect the whole PR, especially unresolved architectural clarification questions.
- Residual risk and tests not run.
- A direct summary of observed changes and task-access limitations when the documented scope is absent or insufficient.

Do not create top-level issue comments for normal review findings. If inline comments cannot be posted with available GitHub MCP tools, generate Markdown instead and explain the limitation.

## Tone
Be direct and useful. Prefer concrete examples over broad principles.

Avoid vague comments such as "consider improving this" unless paired with a clear risk and action.
