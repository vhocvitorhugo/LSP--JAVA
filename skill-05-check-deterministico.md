---
name: check-deterministico
description: >-
  Gate determinístico PASS/FAIL/N/A de conformidade para Java convertido na
  Skill 1. Use automaticamente após o rascunho Java antes de publicar ao
  usuário, e quando o usuário pedir auditoria/conformidade/check de um
  artefato gerado. Sempre cite evidência observável por crítico aplicável.
---

# Skill 5 · Check Determinístico
Versão: v1.11 · Gate obrigatório · `skill-05-check-deterministico.md`

Checks binários apenas — cite evidência observável. Proibido “parece ok”.  
**Proibido** declarar PASS de crítico sem trecho/citação observável no artefato.

## Quando usar / não usar

| Usar | Não usar |
|---|---|
| **Gate** após rascunho Java da Skill 1; auditoria avulsa | Resposta só de boas-vindas/recusa; QA de comportamento (Skill 4); fora de escopo |

## Pipeline do gate (obrigatório)

```text
1. Skill 1 monta inventário interno + RASCUNHO Java (ainda não envia)
2. Skill 5 no modo gate_obrigatorio
3. PASS → publica: código primeiro → análise/inventário → resumo do check com evidências
4. FAIL → corrige na Skill 1 → reexecuta Skill 5 (máx. 2 ciclos)
5. Ainda FAIL → publica + FAIL transparente + IDs que falharam
6. Pergunta de continuidade só na resposta final ao usuário
```

**Proibido:** mostrar Java convertido ao usuário sem este gate.

Sem gate para: boas-vindas, pedido sem artefato (só pedir LSP), recusa de escopo.

## Ordem de execução (obrigatória)

```text
1. Rodar checks CRÍTICOS aplicáveis
2. Se qualquer crítico = FAIL → veredito FAIL imediato (ainda pode anotar demais)
3. Só então rodar checks não críticos aplicáveis
4. N/A = check não se aplica ao artefato (ex.: CHK-FIN sem cursor)
5. Veredito: todo aplicável PASS → PASS; qualquer FAIL → FAIL; evidência insuficiente → INCOMPLETO
```

Não marque N/A em check crítico só para “passar”. Se o artefato exige o check e falha → FAIL.

### Evidência mínima por crítico (obrigatório na publicação)

Para **cada** crítico aplicável (não N/A), a resposta final deve trazer:

| Campo | Exigência |
|---|---|
| ID | ex. `CHK-STUB` |
| Resultado | PASS / FAIL / N/A |
| Evidência | trecho observável (linha/método/`Status`/tabela) — não opinião |

Sem essa tabela → veredito **INCOMPLETO** (mesmo que o restante “pareça” ok).

## Modos

| Modo | Bateria |
|---|---|
| `gate_obrigatorio` + conversão | `conversao_lsp_java` |
| `auditoria_avulsa` | laudo completo (mesmo ordem: críticos → demais) |

## Bateria — conversão (Skill 1)

### Críticos (rodar primeiro)

| ID | PASS | FAIL |
|---|---|---|
| CHK-INV | Tabela de inventário presente na resposta (pode vir **após** o código) | Ausente na conversão completa |
| CHK-COMP | Classe/`execute` completo, sem omissão | Stub / `// restante` / partes |
| CHK-CONS | Entrega única consolidada | Fragmentada |
| CHK-STAT | `Status da conversão: COMPLETA` | Ausente |
| CHK-EVID | `Evidência:` + `Bases consultadas:` | Ausente |
| CHK-SQL2 | Sem Senior SQL 2 | Recomenda SQL 2 |
| CHK-SITAPI | `getHorSit`/`setHorSit`/`zeraHorasSituacao` (se manipula situações) | `getSituacao().get/setMinutos` |
| CHK-FIN | Cursor/`EntitySession` com `finally`/close (se usa ICursor) | Abre sem fechar |
| CHK-THROWS | `execute()` **sem** `throws Exception` | Declara throws |
| CHK-SCNAT | Sem descritor `.sc` para tabela `R*` nativa | `.sc` em `Rxxxxx` |
| CHK-SCID | Se há `.sc`: campo `id` = nome do arquivo **sem extensão** | `id` divergente do filename |
| CHK-STUB | Java publicado sem omissão disfarçada | `return new int[]{0,0}`; `// preencher`; `// mesma lógica`; `// restante`; corpo vazio onde o LSP tinha lógica |

**Nota `CHK-STUB`:** `// TODO: <problema> — Sugestão: <caminho>` com bloco presente e evidência `validacao_manual` = **PASS** (não é stub).

### Demais (após críticos)

| ID | PASS | FAIL |
|---|---|---|
| CHK-CTX | Contexto nomeado | Ausente |
| CHK-MAP | Seção de mapeamento presente (após o código é OK) | Só código, sem mapeamento |
| CHK-CLASS | Rótulos de evidência usados | “ok” vago |
| CHK-B23 | Skills 2+3 sim no HCM | Marcado não |
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
| CHK-NEST | Auxiliares no nível da classe | Método aninhado / código solto fora de método |
| CHK-SCJSON | Se há `.sc`: JSON puro começando com `{` | Texto/YAML/BOM antes do `{` |
| CHK-TIPCON | TipCon via SQL/`ContextSession` (se usado) | `col.getTipCon()` |
| CHK-MARANT | `MarcacaoAnterior` só `diferencaMinutos` (se usado) | `getHora`/`getData` |
| CHK-RS0 | `IResultSet` índice base-0 (se usado) | base-1 como JDBC |
| CHK-DBSESS | ContextSession sem close indevido; DBCenter com close (se DML) | Sessão mal gerenciada |
| CHK-USULONG | Campos `USU_*` de usuário/consultor tipados `long` (se interface) | `int` em ID de usuário |

## Resumo ao usuário (sempre após o gate)

```text
## Check determinístico (Skill 5)
Veredito: PASS | FAIL | INCOMPLETO
Origem: Skill 1
Ciclos de correção: 0|1|2
Críticos: PASS | FAIL [IDs] · falhos/total = n/n
Demais: falhos/total = n/n
### Críticos aplicáveis (obrigatório)
| ID | Resultado | Evidência (trecho observável) |
|---|---|---|
| CHK-COMP | PASS | execute() completo em RegraXxx |
| CHK-STUB | PASS | sem // restante; TODOs só no formato permitido |
| CHK-… | … | … |
Falhas remanescentes: nenhuma | [IDs]
```

**Métrica obrigatória:** `falhos/total` conta só checks **aplicáveis** (ignore N/A no denominador). Ex.: 0/8 críticos e 1/12 demais.

## Laudo avulso (`auditoria_avulsa`)

```text
## Laudo Skill 5
Modo: auditoria_avulsa
Artefato: conversao | outro
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

Gate PASS após rascunho limpo **com tabela de evidências** · FAIL `CHK-COMP`/`CHK-STUB`/`CHK-THROWS`/`CHK-SCNAT`/`CHK-SCID` → corrige ≤2 · FAIL `CHK-TIPCON`/`CHK-MARANT` · **Não** publicar sem gate · **Não** pular críticos · Inventário/mapeamento após o código = PASS em `CHK-INV`/`CHK-MAP` · PASS sem tabela de evidência = **INCOMPLETO**.

## Relacionados

Router (gate) · Skill 1 · vs Skill 4 (QA de comportamento ≠ gate de artefato)
