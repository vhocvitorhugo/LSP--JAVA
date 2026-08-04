---
name: desenvolvimento-orientado
description: >-
  Cria ou refatora regras, rotinas, integrações e validações Senior/LSP como
  código completo comentado. Use quando o usuário pedir construir, estruturar ou
  refatorar uma regra sem conversão LSP→Java. Sempre execute o gate da Skill 9
  antes de publicar a regra ao usuário.
---

# Skill 3 · Desenvolvimento Orientado
Versão: v1.14 · Arquivo: `skill-03-desenvolvimento-orientado.md`

Aplique as regras globais do Router. Não as reescreva.

## Quando usar / não usar

| Usar | Não usar |
|---|---|
| Criar/refatorar regra LSP, rotina, WS, automação | Conceito → 1; só debug → 2; só engenharia reversa → 4; converter → 5 |

**Handoff:** conversão → Skill 5  
**Desempate 2×3×4:** use a tabela do Router (ex.: “revise/refatore” sem bug → esta skill).

## Instruções

1. Declare objetivo funcional + premissas.  
2. Skill 6 para sintaxe/aliases/SQL.  
3. Escolha a estratégia mais segura; implemente com comentários por bloco.  
4. Liste riscos (performance, transação, concorrência, impacto sistêmico) + validação manual.  
5. Monte **rascunho completo** (sem `// restante` / `// implementar demais validações`).  
6. **Gate Skill 9** (`desenvolvimento_lsp`); se FAIL, corrija até 2 ciclos.  
7. Publique código + resumo Check 9 + evidência + continuidade.

## Saída

```text
## Objetivo da implementação
## Premissas adotadas
## Estratégia técnica
## Código completo comentado
## Riscos / impactos
## Pontos de validação manual
## Referência

Evidência: ...
Bases consultadas: Skill 6 [sim/não]; Skill 7 [não]

## Check determinístico (Skill 9)
Veredito: PASS | FAIL
Origem: Skill 3
Ciclos de correção: 0|1|2
Críticos: PASS | FAIL [IDs] · falhos/total = n/n
Demais: falhos/total = n/n
Falhas remanescentes: ...

Deseja continuar neste fluxo, voltar ao menu ou seguir para outra opção?
```

## Exemplos

**Entrada:** `Crie regra LSP que valide colaborador ativo` → rascunho → gate 9 → publicar.  
**Não faça:** publicar sem Skill 9; omitir código com comentários; entregar Java HCM (Skill 5).

## Relacionados

Router · Skill 6 · gate Skill 9 · handoff Skill 5
