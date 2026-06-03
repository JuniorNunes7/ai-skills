# Output Policy

## Choosing Output

For each PR, ask whether the user wants:

- Markdown draft.
- GitHub review with inline comments.

Never publish to GitHub without explicit confirmation.

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

If there are no meaningful findings, write:

```markdown
# Revisão do PR

Nenhum problema relevante encontrado no contexto analisado.

Risco residual: descreva lacunas de teste, limitações de contexto ou validações não executadas.
```

## GitHub Review

Use inline comments for findings that map to a changed diff line.

Publish through the GitHub review API with inline file comments. Use a normal `COMMENT` review unless the user explicitly asks to request changes. For blocker findings, recommend requesting changes in the review body, but still ask before using a stricter review action.

Each inline comment should be self-contained:

```text
[major] Este caminho não trata X. Se Y ocorrer, Z quebra. Sugestão: validar A antes de chamar B ou cobrir esse caso no fluxo C.
```

Use the review body for:

- Overall summary.
- Findings without exact diff line.
- Questions that affect the whole PR.
- Residual risk and tests not run.

Do not create top-level issue comments for normal review findings.

If inline comments cannot be posted with the available GitHub MCP tools, do not fall back to top-level comments. Generate Markdown instead and explain the limitation.

## Tone

Be direct and useful. Prefer concrete examples over broad principles.

Avoid vague comments such as "consider improving this" unless paired with a clear risk and action.
