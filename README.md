# My Skills

Repositório pessoal para organizar skills.

## Índice

| Skill | Descrição | Pasta |
| --- | --- | --- |
| Code Reviewer | Revisa PRs do GitHub com contexto do projeto e comentários inline. | [`skills/code-reviewer`](skills/code-reviewer/) |

Novas skills devem ser adicionadas dentro de `skills/`, cada uma em sua própria pasta.

## Como Usar Localmente

Copie a pasta da skill para o diretório global de skills do Codex:

```bash
cp -R skills/code-reviewer ~/.codex/skills/
```

O resultado esperado é:

```text
~/.codex/skills/code-reviewer/SKILL.md
~/.codex/skills/code-reviewer/agents/openai.yaml
~/.codex/skills/code-reviewer/references/
```

Depois disso, invoque a skill em uma conversa:

```text
Use $code-reviewer para revisar owner/repo#123
```

## Validação

Na raiz deste repositório, valide a skill com:

```bash
python ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/code-reviewer
```

Valide também o YAML do agent:

```bash
python -c 'import yaml; yaml.safe_load(open("skills/code-reviewer/agents/openai.yaml")); print("ok")'
```
