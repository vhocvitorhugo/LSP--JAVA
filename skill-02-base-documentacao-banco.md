---
name: base-documentacao-banco
description: >-
  Base interna de links autorizados da documentação Senior e aliases ERP/HCM.
  Use quando qualquer skill precisar citar docs oficiais, validar links de SQL
  em regra, web services, sintaxe LSP, URLs de equivalência HCM ou interpretar
  aliases de tabela/campo. Nunca trate como Senior SQL 2.
---

# Skill 2 · Base de Documentação e Banco
Versão: v1.2 · Interna · `skill-02-base-documentacao-banco.md`

Skill interna — **não** é fluxo de usuário. Aplique as regras globais do Router (`router.md`).

**Fronteira:** esta skill = **links oficiais + aliases de banco**. Mapeamento LSP→Java, `getHorSit`/`setHorSit`, marcações, esqueletos → **Skill 3** (não duplique aqui).

## Quando usar / não usar

| Usar | Não usar |
|---|---|
| Link oficial, SQL em regra, WS, sintaxe LSP, URL de equivalência HCM, alias | Conversão/mecânica de ponto (Skill 3); conversa casual |

Não exponha “Skill 2” ao usuário — cite só a fonte validada.

## Ritual de revisão de links (manutenção do treinamento)

A cada bump de versão que toque docs/links **ou** a cada ciclo de manutenção da Skill 2:

1. Percorra **todos** os links listados neste arquivo.  
2. Classifique cada um: `ok` | `quebrado` | `redirecionou_para_indice` | `ausente`.  
3. Link `quebrado` / índice genérico → **não citar** no atendimento; marque no arquivo como indisponível ou remova na próxima entrega.  
4. Tópico sem URL válida → use a frase de link ausente desta skill.  
5. Não adicione URL “parecida” sem validar conteúdo específico da página.  
6. Registre no `CHANGELOG.md` (local) se houve remoção/substituição de link.

## Restrições absolutas

1. Somente os links listados **neste arquivo** são oficiais nesta versão do treinamento.  
2. Tópico ausente → `Não encontrei link autorizado na base atual para validar esse ponto com segurança.`  
3. Antes de citar: a página deve ter conteúdo específico, não portal/índice.  
4. Não reescreva `index.htm#...` para URLs diretas inventadas.  
5. Senior SQL 2 proibido — use só links de SQL em regra / SP / proprietária.  
6. Aliases são `auxiliar` até o schema real confirmar. **Nunca** diga “está confirmado” só com esta base.  
7. Apostilas LSP/APO/Rubi: **não estão no repo** (`ausente_no_repo`); anexos do usuário são só complementares (`Material complementar de treinamento`).  
8. Em HCM/Ponto com SQL/cursor: devolva o **link** (e alias se houver); a decisão API vs EntitySession é da **Skill 3**.

## Instruções

```text
1. Identificar tópico (sintaxe|WS|SQL|evento|equivalência HCM|alias|apostila)
2. Localizar seção abaixo
3. Classificar cobertura: confirmado | auxiliar | ausente
4. Se o pedido for método/equivalência de conversão → encaminhar à Skill 3
5. Devolver à skill chamadora: achado + classificação + limite
6. Nunca inventar link/alias “quase igual”
```

## Índice

| Tópico | Seção |
|---|---|
| Sintaxe / variáveis / limites LSP | Links — Sintaxe |
| Web services / HTTP / JSON / FTP | Links — Integração |
| SQL em regra / SP / proprietária / arquivos | Links — Banco |
| Usuários / AD / diretórios | Links — Acesso |
| Eventos / workflow / relatórios | Links — Eventos |
| URLs oficiais de equivalência HCM | Links — Conversão |
| Aliases de tabela/campo | Mapeamento banco |
| Mecânica LSP/APO/Rubi (anexo do usuário) | Apostilas (complementar) |
| Métodos Java / HorSit / marcações | **Skill 3** (fora desta skill) |

## Links — Sintaxe (Tecnologia 5.10.4)

- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/sintaxe-de-comandos-e-operadores.htm
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/declaracao-de-variaveis.htm
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/limite-das-regras.html
- https://documentacao.senior.com.br/tecnologia/5.10.4/cbds/mascara.htm

## Links — Integração

- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/chamar-web-service-via-regra.htm
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/requisicoes-http.htm
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/criacao-json-token-web.htm
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/regra-para-web-services.html
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/ftp.htm

## Links — Banco (SQL em regra — nunca Senior SQL 2)

- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/sql-em-regra.html
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/execucao-de-stored-procedures-nas-regras.htm
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/manipulacao-da-proprietaria.html
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/manipulacao-de-arquivos-texto.htm

## Links — Acesso

- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/manipulacao-de-usuarios-e-grupos.htm
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/integracao-servidor-ad.htm
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/permissao-de-diretorios.htm

## Links — Eventos

- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#geradores/importacao-exportacao/regras-por-evento.htm
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/workflow.html
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/gerador-de-relatorios.htm
- https://documentacao.senior.com.br/tecnologia/5.10.4/index.htm#lsp/funcoes/agendamento-de-compromissos.htm
- https://documentacao.senior.com.br/tecnologia/5.10.4/lsp/funcoes/gerais.html

## Links — Conversão (HCM 6.10.4)

- **Equivalência das funções de regras (mapa LSP → Java — prioritário na conversão):**  
  https://documentacao.senior.com.br/gestao-de-pessoas-hcm/6.10.4/informacoes-adicionais/rotinas/gpo/integracao-controle-ponto-refeitorio/equivalencia-funcoes-regras.htm
- **Índice das Funções (detalhe/assinaturas):**  
  https://documentacao.senior.com.br/gestao-de-pessoas-hcm/6.10.4/customizacoes/funcoes.htm  
  (Evitar depender só de `index.htm#customizacoes/funcoes.htm` — preferir a URL direta acima para conteúdo específico.)

O catálogo operacional e a mecânica LSP→Java estão **somente** na **Skill 3**.  
Aqui ficam apenas as **URLs oficiais** para validar/citar a fonte.

## Mapeamento banco (auxiliar)

Frase: `O mapeamento sugere essa equivalência, mas a confirmação depende de validação no schema/dicionário de dados.`

### Tabelas ERP

| Termo | Candidato | Cobertura |
|---|---|---|
| NF Saída / Venda | `E120NFV` | auxiliar |
| Item NF Saída | `E140NFV` | auxiliar |

Campos ERP: **ausente** — pedir schema / `validacao_manual`.

### HCM

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
- `ExecSQL` / funções `SQL_*`: SQL em regra (Skill 2 links), **nunca** Senior SQL 2  
- Listas dinâmicas / Editor de Regras: apoio conceitual antes de converter  
- Em conversão: entender mecânica LSP aqui → mapear na Skill 3

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
