---
name: check-deterministico
description: >-
  Gate determinístico PASS/FAIL/N/A de conformidade para toda regra criada,
  refatorada, convertida ou corrigida com código substituível. Use
  automaticamente após rascunhos das Skills 2/3/5 antes de publicar ao usuário,
  e quando o usuário pedir auditoria/conformidade/check de um artefato gerado.
---

# Skill 9 · Check Determinístico
Versão: v1.14 · Gate obrigatório · `skill-09-check-deterministico.md`

Checks binários apenas — cite evidência observável. Proibido “parece ok”.

## Quando usar / não usar

| Usar | Não usar |
|---|---|
| **Gate** após Skill 3 / Skill 5 Fase C / código corrigido da Skill 2; auditoria avulsa | Criar/converter do zero (3/5); QA de menu (8) |

## Pipeline do gate (obrigatório)

```text
1. Skill origem monta RASCUNHO (ainda não envia)
2. Skill 9 no modo gate_obrigatorio
3. PASS → publica rascunho + resumo do check
4. FAIL → corrige na origem → reexecuta 9 (máx. 2 ciclos)
5. Ainda FAIL → publica + FAIL transparente + IDs que falharam
6. Pergunta de continuidade só na resposta final ao usuário
```

**Proibido:** mostrar regra gerada/convertida ao usuário sem este gate.

Sem gate para: menu, Skill 1, Skill 4, Skill 5 Fase A/B, diagnóstico sem código corrigido.

## Ordem de execução (obrigatória)

```text
1. Rodar checks CRÍTICOS aplicáveis
2. Se qualquer crítico = FAIL → veredito FAIL imediato (ainda pode anotar demais)
3. Só então rodar checks não críticos aplicáveis
4. N/A = check não se aplica ao artefato (ex.: CHK-FIN sem cursor)
5. Veredito: todo aplicável PASS → PASS; qualquer FAIL → FAIL; evidência insuficiente → INCOMPLETO
```

Não marque N/A em check crítico só para “passar”. Se o artefato exige o check e falha → FAIL.

## Modos

| Modo | Bateria |
|---|---|
| `gate_obrigatorio` + conversão | `conversao_lsp_java` |
| `gate_obrigatorio` + criar/corrigir regra | `desenvolvimento_lsp` |
| `auditoria_avulsa` | laudo completo (mesmo ordem: críticos → demais) |

## Bateria — conversão (Skill 5 C)

### Críticos (rodar primeiro)

| ID | PASS | FAIL |
|---|---|---|
| CHK-INV | Tabela de inventário presente | Ausente na conversão completa |
| CHK-COMP | Classe/`execute` completo, sem omissão | Stub / `// restante` / partes |
| CHK-CONS | Entrega única consolidada | Fragmentada |
| CHK-STAT | `Status da conversão: COMPLETA` | Ausente |
| CHK-EVID | `Evidência:` + `Bases consultadas:` | Ausente |
| CHK-SQL2 | Sem Senior SQL 2 | Recomenda SQL 2 |
| CHK-SITAPI | `getHorSit`/`setHorSit`/`zeraHorasSituacao` (se manipula situações) | `getSituacao().get/setMinutos` |
| CHK-FIN | Cursor/`EntitySession` com `finally`/close (se usa cursor) | Abre sem fechar |

### Demais (após críticos)

| ID | PASS | FAIL |
|---|---|---|
| CHK-CTX | Contexto nomeado | Ausente |
| CHK-MAP | Seção de mapeamento | Só código |
| CHK-CLASS | Rótulos de evidência usados | “ok” vago |
| CHK-B67 | Skills 6+7 sim no HCM | Marcado não |
| CHK-SQLAPI | API ou nota manual | SQL/EntitySession cego |
| CHK-ORDEM | Ordem de parâmetros confirmada ou marcada manual | Cópia cega da ordem LSP |
| CHK-TIPO | Tipos Java explícitos coerentes | `Numero` solto / tipagem fraca |
| CHK-CTXOK | Métodos do contexto correto da regra | Getter de apuração em contexto errado |
| CHK-MIN | Minutos inteiros / conversão explícita | `HH:mm` em API de minutos |
| CHK-END | End→retorno ou manual | Ignorado |
| CHK-SOLTO | Contexto mapeado | Variável solta |
| CHK-VAL | Lista manual se necessário | Manual sem lista |
| CHK-LINK | Sem downloads falsos | Link falso/não autorizado como oficial |
| CHK-SIG | Sanitizado | Vazamento |
| CHK-COM | Comentários por bloco | Código longo sem comentário |
| CHK-CONT | Continuidade na resposta **final** | Ausente no final (N/A no rascunho interno) |

## Bateria — desenvolvimento / correção (Skill 3 / 2)

### Críticos

| ID | PASS | FAIL |
|---|---|---|
| CHK-FULL | Código completo | `// restante` |
| CHK-SQL2 | Sem SQL 2 | Usa SQL 2 |
| CHK-EVID | Campos de evidência | Ausente |

### Demais

| ID | PASS | FAIL |
|---|---|---|
| CHK-OBJ | Objetivo/premissas | Ausente |
| CHK-CUR | Abrir/ler/fechar | Abre sem fechar |
| CHK-COM | Comentários por bloco | Ausente em regra longa |
| CHK-SIG | Sanitizado | Vazamento |
| CHK-CONT | Na resposta final | Ausente (N/A no rascunho) |

## Resumo ao usuário (sempre após o gate)

```text
## Check determinístico (Skill 9)
Veredito: PASS | FAIL | INCOMPLETO
Origem: Skill N
Ciclos de correção: 0|1|2
Críticos: PASS | FAIL [IDs] · falhos/total = n/n
Demais: falhos/total = n/n
Falhas remanescentes: nenhuma | [IDs]
```

**Métrica obrigatória:** `falhos/total` conta só checks **aplicáveis** (ignore N/A no denominador). Ex.: 0/8 críticos e 1/12 demais.

## Laudo avulso (`auditoria_avulsa`)

```text
## Laudo Skill 9
Modo: auditoria_avulsa
Artefato: conversao | desenvolvimento | outro
Veredito: PASS | FAIL | INCOMPLETO

### Críticos
| ID | Resultado | Evidência |
|---|---|---|
| CHK-… | PASS/FAIL/N/A | … |

### Demais
| ID | Resultado | Evidência |
|---|---|---|
| CHK-… | PASS/FAIL/N/A | … |

Contagens: PASS=n FAIL=n N/A=n
Críticos falhos/total = n/n
Demais falhos/total = n/n
Ações corretivas: …
Evidência / Bases consultadas: …
+ continuidade
```

## Exemplos

Gate PASS após Fase C limpa · FAIL crítico `CHK-COMP` por stub → corrige ≤2 · **Não** publicar sem gate · **Não** pular críticos.

## Relacionados

Router (gate) · Skills 2/3/5 · vs Skill 8 (QA de comportamento ≠ gate de artefato)
