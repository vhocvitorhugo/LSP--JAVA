---
name: diagnostico-debug
description: >-
  Diagnostica erros, logs, exceções, falhas de integração e performance em
  Senior/LSP; entrega diagnóstico parcial útil e regra corrigida completa quando
  possível. Use quando o usuário enviar erro, log, comportamento inesperado ou
  regra quebrada. Sempre execute o gate da Skill 9 antes de publicar regra
  corrigida substituível.
---

# Skill 2 · Diagnóstico e Debug
Versão: v1.14 · Arquivo: `skill-02-diagnostico-debug.md`

Aplique as regras globais do Router. Não as reescreva.

## Quando usar / não usar

| Usar | Não usar |
|---|---|
| Erro, log, exceção, comportamento inesperado, performance ruim | Só conceito → 1; criar do zero → 3; analisar regra saudável → 4; converter → 5 |

**Handoff:** conversão → Skill 5; reescrita ampla sem foco em bug → Router pode escolher Skill 3  
**Desempate 2×3×4:** use a tabela do Router (ex.: “melhorar regra” com falha → esta skill).

## Catálogo de riscos (sempre avaliar)

cursor aberto · consulta sem liberação · SQL sem filtro · performance · efeitos colaterais · inconsistência transacional · concorrência · alteração indevida de dados · falha silenciosa

## Instruções

1. Analise o material já enviado.  
2. Nomeie o sintoma principal; causa provável + alternativas.  
3. Skill 6 se precisar confirmar sintaxe/comportamento/aliases.  
4. Explique como validar cada hipótese.  
5. Se houver código suficiente: monte **rascunho completo** corrigido (ciclo abrir→ler→fechar).  
6. Se for publicar regra corrigida → **gate Skill 9** (`desenvolvimento_lsp`); corrija até 2 ciclos.  
7. Publique diagnóstico (+ código) + resumo Check 9 (ou N/A) + evidência + continuidade.  
8. Peça complemento só se estiver bloqueado — nunca responda só “preciso do código completo”.

## Saída

```text
## Problema identificado
## Causa provável
## Hipóteses alternativas
## Como validar
## Correção sugerida
## Versão corrigida comentada
## Riscos e impactos
## Referência

Evidência: ...
Bases consultadas: Skill 6 [sim/não]; Skill 7 [não]

## Check determinístico (Skill 9)
Veredito: PASS | FAIL | N/A
Origem: Skill 2
Ciclos de correção: 0|1|2
Críticos: PASS | FAIL [IDs] · falhos/total = n/n
Demais: falhos/total = n/n
Falhas remanescentes: ...

Deseja continuar neste fluxo, voltar ao menu ou seguir para outra opção?
```

## Exemplos

**Entrada:** log mostra cursor sem fechar → diagnosticar + correção completa + gate 9.  
**Não faça:** publicar regra corrigida sem Skill 9; inventar APIs; Senior SQL 2.

## Relacionados

Router · Skill 6 · gate Skill 9 · handoff Skill 5
