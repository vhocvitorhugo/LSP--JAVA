---
name: base-documentacao-banco
description: >-
  Base interna de links oficiais Senior usados na conversão LSP→Java (HCM /
  Gestão do Ponto): equivalência de funções, índice HCM, sintaxe LSP e SQL em
  regra, mais aliases HCM auxiliares. Use para citar docs oficiais ou interpretar
  aliases. Nunca trate como Senior SQL 2.
---

# Skill 2 · Base de Documentação e Banco
Versão: v1.11 · Interna · `skill-02-base-documentacao-banco.md`

Skill interna — **não** é fluxo de usuário. Aplique as regras globais do Router (`router.md`).

**Escopo deste projeto:** somente documentação útil à **conversão LSP → Java** em **Senior HCM / Gestão do Ponto**. Links de WS, FTP, AD, workflow, relatórios, ERP genérico etc. **não** fazem parte desta base.

**Nota:** ContextSession/DBCenter da plataforma G5 (SELECT/DML em Java) **não** autorizam citar ou usar **Senior SQL 2** — continue usando só o link de SQL em regra abaixo.

**Fronteira:** esta skill = **links oficiais do projeto + aliases HCM**. Mapeamento LSP→Java, `getHorSit`/`setHorSit`, marcações, esqueletos → **Skill 3** (não duplique aqui).

## Quando usar / não usar

| Usar | Não usar |
|---|---|
| Equivalência HCM, índice de funções, sintaxe LSP, SQL em regra, alias HCM | Conversão/mecânica de ponto (Skill 3); integração/WS/AD/eventos; conversa casual |

Não exponha “Skill 2” ao usuário — cite só a fonte validada.

## Ritual de revisão de links (manutenção do treinamento)

A cada bump de versão que toque docs/links **ou** a cada ciclo de manutenção da Skill 2:

1. Percorra **todos** os links listados neste arquivo.  
2. Classifique cada um: `ok` | `quebrado` | `redirecionou_para_indice` | `ausente`.  
3. Link `quebrado` / índice genérico → **não citar** no atendimento; marque no arquivo como indisponível ou remova na próxima entrega.  
4. Tópico sem URL válida → use a frase de link ausente desta skill.  
5. Não adicione URL fora do escopo LSP→Java HCM/Ponto.  
6. Registre no `CHANGELOG.md` se houve remoção/substituição de link.

## Restrições absolutas

1. Somente os links listados **neste arquivo** são oficiais nesta versão do treinamento.  
2. Tópico ausente → `Não encontrei link autorizado na base atual para validar esse ponto com segurança.`  
3. Antes de citar: a página deve ter conteúdo específico, não portal/índice.  
4. Não reescreva `index.htm#...` para URLs diretas inventadas.  
5. Senior SQL 2 proibido — use só o link de SQL em regra.  
6. Aliases são `auxiliar` até o schema real confirmar. **Nunca** diga “está confirmado” só com esta base.  
7. Apostilas LSP/APO/Rubi: **não estão no repo** (`ausente_no_repo`); anexos do usuário são só complementares.  
8. Em HCM/Ponto com SQL/cursor: devolva o **link** (e alias se houver); a decisão API vs EntitySession é da **Skill 3**.

## Instruções

```text
1. Identificar tópico (sintaxe|SQL|equivalência HCM|alias)
2. Localizar seção abaixo
3. Classificar cobertura: confirmado | auxiliar | ausente
4. Se o pedido for método/equivalência de conversão → encaminhar à Skill 3
5. Devolver à skill chamadora: achado + classificação + limite
6. Nunca inventar link/alias “quase igual”
```

## Índice

| Tópico | Seção |
|---|---|
| URLs oficiais de equivalência HCM | Links — Conversão |
| Sintaxe / variáveis / limites LSP | Links — Sintaxe |
| SQL em regra (anti Senior SQL 2) | Links — Banco |
| Aliases HCM de tabela/campo | Mapeamento banco |
| Mecânica LSP (anexo do usuário) | Apostilas (complementar) |
| Métodos Java / HorSit / marcações | **Skill 3** (fora desta skill) |

## Links — Conversão (HCM 6.10.4) — prioritários

- **Equivalência das funções de regras (mapa LSP → Java):**  
  https://documentacao.senior.com.br/gestao-de-pessoas-hcm/6.10.4/informacoes-adicionais/rotinas/gpo/integracao-controle-ponto-refeitorio/equivalencia-funcoes-regras.htm
- **Índice das Funções (detalhe/assinaturas):**  
  https://documentacao.senior.com.br/gestao-de-pessoas-hcm/6.10.4/customizacoes/funcoes.htm  
  (Preferir a URL direta acima; evitar depender só de `index.htm#customizacoes/funcoes.htm`.)

O catálogo operacional e a mecânica LSP→Java estão **somente** na **Skill 3**.  
Aqui ficam as **URLs oficiais** para validar/citar a fonte.

## Links — Sintaxe (Tecnologia 5.10.4)

Úteis para interpretar a regra LSP antes/durante a conversão:

- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/sintaxe-de-comandos-e-operadores.htm
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/declaracao-de-variaveis.htm
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/limite-das-regras.html

## Links — Banco (SQL em regra — nunca Senior SQL 2)

- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/sql-em-regra.html

## Mapeamento banco HCM (auxiliar)

Frase: `O mapeamento sugere essa equivalência, mas a confirmação depende de validação no schema/dicionário de dados.`

| Origem | Candidato | Cobertura |
|---|---|---|
| R035DEP (termo) | `R036DEP` | auxiliar |
| R034FUN.SitCol | `SitAfa` | auxiliar |
| R034FUN.DatDem | `DatAfa` | auxiliar |
| R036DEP.ParDep | `GraPar` | auxiliar |
| R024CAR.DesCar / Cargo | `TitRed` | auxiliar |
| SitAfa Demitido | `7` | auxiliar |

Precedência: mapa mais completo/específico → candidato → schema/dicionário.  
SQL: alias → candidato → módulo → filtros/chaves → nunca existência absoluta só com esta tabela.

**Proibido:** “Use `R024CAR.TitRed`; está confirmado.” (só com alias auxiliar)

## Apostilas (complementar — ausente_no_repo)

Se o usuário anexar apostilas LSP/APO/Rubi, use como `Material complementar de treinamento` (nunca como doc oficial). Âncoras típicas:

- Cursor LSP: criar → abrir → ler → fechar; risco de cursor aberto  
- `ExecSQL` / funções `SQL_*`: SQL em regra (link desta skill), **nunca** Senior SQL 2  
- Em conversão: entender mecânica LSP → mapear na Skill 3

Prioridade em conflito: doc oficial Skill 2 → equivalência HCM → schema → apostila → inferência.

## Saída para a skill chamadora

```text
topico: ...
cobertura: confirmado | auxiliar | ausente
achado: ...
link_ou_alias: ...
limite: ...
```

## Relacionados

Política de evidência do Router · Skill 3 (após docs oficiais)
