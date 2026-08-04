---
name: conversao-lsp-java
description: >-
  Converte regras LSP Senior para Java (HCM/Gestão do Ponto) com inventário,
  mapeamento, fases A/B/C e entrega consolidada. Use ao converter, migrar ou
  mapear LSP→Java. Sempre execute o gate da Skill 9 antes de publicar a Fase C.
  Prefira documentação oficial (Skill 6) aos padrões da Skill 7.
---

# Skill 5 · Conversão LSP → Java
Versão: v1.0 · Arquivo: `skill-05-conversao-lsp-java.md`

Aplique as regras globais do Router. Preserve a **intenção funcional**, não a sintaxe literal.

## Quando usar / não usar

| Usar | Não usar |
|---|---|
| Converter/migrar/mapear LSP→Java / HCM Ponto | Conceito → 1; debug → 2; só criar LSP → 3; só engenharia reversa → 4 |

**Handoff:** só explicar → 4; gate FAIL → corrigir aqui e reexecutar 9; auditoria avulsa → 9  
**Reuso:** se a Skill 4 já entregou inventário no formato Fase A, **reaproveite** — não remapeie do zero sem motivo.

## Restrições locais

1. Fases A→B→C; sem Java final antes do inventário (salvo formato já pedido e A+C na mesma resposta transparente).  
2. Java só consolidado; sem pedaços / `// restante`.  
3. Nunca invente assinaturas; desconhecido → `validacao_manual`.  
4. Ordem de parâmetros não se presume igual à LSP.  
5. SQL/cursor → API semântica antes de EntitySession.  
6. Skill 6 obrigatória para docs; Skill 7 obrigatória em HCM/Ponto; **6 prevalece** em conflito.  
7. **Fase C:** rascunho → **gate Skill 9** → publicar com resumo do check.  
8. Sem links de download inventados.  
9. Regra completa enviada → conversão integral (mesmo com pontos manuais marcados).

## Fases

```text
A  Inventário + mapeamento + plano   (sem Java final)
   → se o usuário já pediu canvas|doc|código inteiro → pular B e ir à C após A
B  Perguntar 1=canvas / 2=documento  (sem Java final)
C  Rascunho Java completo → gate Skill 9 → publicar + Consolidação final
```

### Quando perguntar formato (Fase B)

Pergunte se o usuário pediu conversão sem indicar formato (`converta`, `faça a conversão completa`, etc.).

### Quando não perguntar

Não pergunte se já pediu: canvas, documento/link/arquivo, “regra toda”, “código inteiro”.

### Prioridade de entrega

1. Canvas/área de edição  
2. Documento/arquivo **real** (nunca inventar link)  
3. Bloco único na conversa, se couber com segurança  

## Protocolo de entrega consolidada

1. **Leitura integral** — início/fim, variáveis, cursores, SQLs, `End`, efeitos colaterais.  
2. **Plano lógico** — blocos (init, validações, consultas, negócio, situações, retorno); o plano **não** autoriza entregar Java em partes.  
3. **Java completo** — proibido substituir implementação por `// restante`, `// continuar conforme original`, `// mesma lógica`.  
4. **Entrega** no formato escolhido.  
5. **Consolidação final** — status COMPLETA + o que é confirmado / adaptação / inferência / validação manual.

## Prioridade arquitetural (Gestão do Ponto)

1. Equivalência oficial (Skill 6 / catálogo Skill 7)  
2. Métodos documentados do módulo  
3. Métodos de contexto (`contextoApuracao` etc.)  
4. Padrões operacionais Skill 7  
5. Exemplos sanitizados / anexos do usuário (`padrao_anexo`)  
6. Aliases/banco Skill 6 (só interpretação)  
7. EntitySession/cursor manual — último recurso, com justificativa  

## Tabela de inventário (A)

| Item LSP | Tipo | Uso na regra | Equivalente Java / padrão | Evidência | Status |

Tipos: variável de contexto | local | função | `End` | array | cursor | SQL | marcação | situação | histórico | totalizador | dependência.

Regras: End → retorno; arrays → métodos/coleções; horas → minutos (`14:30`→`870`); ordem de parâmetros Java confirmada.

## Instruções

1. Leia a LSP inteira; defina contexto: `apuracao|consistencia|bloqueio|fechamento_bh|geral|indefinido`.  
2. Consulte Skill 6 (**URLs/aliases**) e Skill 7 (**mecânica + catálogo** — ordem A→G do arquivo).  
3. Monte inventário; mapeie com `confirmada|adaptacao_arquitetural|padrao_anexo|inferencia|validacao_manual`.  
4. Mecânica antes da sintaxe (Skill 7: restrições → workflow → família do catálogo → armadilhas).  
5. Execute A/B/C; gate na C (Skill 9: **críticos primeiro**).

Âncoras: Skill 7 — catálogo + `getHorSit`/`setHorSit`/`zeraHorasSituacao`/`getDefinicaoSituacoes`.  
**Não** usar `getSituacao(...).getMinutos()/setMinutos(...)`.  
Cursor `R014SIN`/`R030EMP` → `CodDsi` → `getDefinicaoSituacoes().getCodigo()`.

## Checklist antes do Java (C)

- [ ] Li a regra inteira e nomeei o contexto?  
- [ ] Inventário cobre variáveis/funções/arrays/`End`/cursores/SQLs?  
- [ ] Consultei Skills 6 e 7?  
- [ ] Classifiquei evidências?  
- [ ] Há API semântica antes de EntitySession?  
- [ ] Ordem de parâmetros / minutos / sem variável solta?

## Saída — Fase A

```text
## Objetivo da regra original
## Resumo da lógica de negócio
## Contexto de execução
## Inventário de conversão
(tabela)
## Mapeamento LSP → Java (plano)
## Itens sem equivalência direta

Evidência: ...
Bases consultadas: Skill 6 [sim]; Skill 7 [sim]
[pergunta Fase B, se necessário]
+ continuidade
```

## Saída — Fase C (após o gate)

```text
## Objetivo / Inventário / Mapeamento
## Código Java convertido   [completo]
## Comentários técnicos
## Itens sem equivalência / validação manual
## Referência documental
## Consolidação final
Status da conversão: COMPLETA
Formato de entrega: ...

Evidência: ...
Bases consultadas: Skill 6 [sim]; Skill 7 [sim]

## Check determinístico (Skill 9)
Veredito: PASS | FAIL
Origem: Skill 5
Ciclos de correção: 0|1|2
Críticos: PASS | FAIL [IDs] · falhos/total = n/n
Demais: falhos/total = n/n
Falhas remanescentes: ...

+ continuidade
```

## Exemplos

**A→B:** converter sem formato → inventário + perguntar 1/2.  
**Pular B + gate:** “no canvas, regra toda” → rascunho A+C → Skill 9 → publicar.  
**Não faça:** publicar C sem Skill 9; inventar método; entregar em partes; `// restante da lógica`.

## Relacionados

Router · Skills 6 e 7 · gate Skill 9
