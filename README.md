<h1 align="center">LSP→JAVA</h1>

<p align="center">
  <b>Agente de IA especializado em conversão assistida LSP → Java (Senior HCM / Gestão do Ponto)</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/SENIOR_SISTEMAS-HCM_%7C_ERP-blue?style=for-the-badge" alt="Senior Sistemas" />
  <img src="https://img.shields.io/badge/LSP-5.10.4-orange?style=for-the-badge" alt="LSP 5.10.4" />
  <img src="https://img.shields.io/badge/JAVA-17%2B-red?style=for-the-badge" alt="Java 17+" />
  <img src="https://img.shields.io/badge/LSP--JAVA-v1.7-success?style=for-the-badge" alt="LSP→JAVA v1.7" />
</p>

---

## O que é

O **LSP→JAVA** é um agente em formato **Router + Skills** focado **somente** na conversão assistida de regras **LSP → Java** no **Senior HCM / Gestão do Ponto**.

Ele **não** é uma aplicação web nem um compilador: é o **treinamento** (Markdown) que um assistente de IA carrega para converter regras com inventário, evidência, Java consolidado e gate de conformidade.

**Versão atual: v1.7** — conversão completa na mesma resposta: **Java primeiro**, inventário/análise depois; formato omitido = `bloco único` (sem pergunta bloqueante). Mantém goldens G-SIT/G-CUR/G-USU, `CHK-STUB` e cartão de decisão. Itens de API que dependem de SDK (`TipoHoraExtra`, `@Transactional`) ficam **bloqueados até validação com jar/projeto**.

**Para quem:** analistas e desenvolvedores que migram regras LSP de ponto para Java no ecossistema Senior.

Histórico de mudanças: [`CHANGELOG.md`](CHANGELOG.md).

---

## Como usar

Gatilhos de boas-vindas: `inicio`, `início`, `menu`, `começar`, `comecar`, `help`, `ajuda`, `opções`, `opcoes`, `voltar`.

```text
LSP→JAVA — Conversão LSP para Java

Sou o LSP→JAVA, agente especializado somente em conversão assistida de regras LSP para Java (Senior HCM / Gestão do Ponto).

Como usar:
- Cole a regra LSP (ou anexe o arquivo) e peça para converter.
- Opcional: diga o formato — canvas, documento/arquivo ou bloco único (padrão: bloco único).
- Posso auditar uma conversão já gerada (`check` / auditoria).

Fora de escopo: mentoria, debug sem conversão, criar/refatorar LSP sem migrar para Java, ou só engenharia reversa.

Envie a regra LSP para começar.
```

### Passo a passo (usuário)

1. Carregue no assistente o [`router.md`](router.md) e as skills `skill-01` … `skill-05` deste repositório.
2. Digite `inicio` / `menu` / `ajuda` (opcional) para ver as boas-vindas.
3. Cole a regra LSP (ou anexe o arquivo) e peça para **converter** / **migrar**.
4. Opcional: diga o formato — **canvas**, **documento/arquivo** ou **bloco único** (se omitir, usa bloco único).
5. Receba o **Java consolidado no topo**, depois inventário/análise e o resumo do check.
6. Para auditar uma conversão já gerada: peça `check` / **auditoria**.
7. Depois da conversão, `continuar` = validar/revisar — **não** gera o “próximo bloco” de código.

### Fora de escopo

Mentoria genérica, debug sem conversão, criar/refatorar LSP sem migrar para Java, ou só engenharia reversa.

```text
Este agente (LSP→JAVA) faz somente conversão LSP → Java.

Para mentoria, diagnóstico sem conversão, criação de regras LSP ou engenharia reversa sem migração, use outro fluxo/ferramenta.

Se quiser converter uma regra, cole o LSP (ou anexe o arquivo) e peça a conversão.
```

---

## Como o agente funciona

### Roteamento (Router)

```text
SE auditoria avulsa de artefato gerado       → Skill 5
SE converter/migrar/mapear LSP→Java          → Skill 1  [+ gate Skill 5]
SE fora de escopo                            → RECUSA + redirecionar
SENÃO                                        → BOAS-VINDAS
```

| Entrada | Ação |
| :--- | :--- |
| Gatilho de boas-vindas | Somente o texto canônico acima |
| Demanda de conversão / migrar LSP→Java | Skill 1 (código → análise) |
| `check` / auditoria | Skill 5 (`auditoria_avulsa`) |
| Fora de escopo | Recusa + redirecionamento |
| `continuar` após conversão | Validar/revisar — nunca próximo bloco de código |

### Passo a passo (agente — conversão)

```text
1. Router confirma escopo (conversão vs recusa vs boas-vindas vs check)
2. Skill 1 — inventário + mapeamento internos (não publica resposta só-inventário)
3. Skill 1 — gera rascunho Java completo (consolidado; sem "// restante")
4. Formato: canvas/documento se pedido; senão padrão bloco único (sem perguntar)
5. Consulta Skill 2 (docs/links) e Skill 3 (catálogo/padrões/goldens) conforme o inventário
6. Ordem de decisão: contexto → API semântica → USU_* (IEntity/.sc) → R*/TipCon (ContextSession) → validacao_manual
7. Gate Skill 5 (obrigatório): checks críticos (ex. CHK-STUB, CHK-SITAPI, CHK-THROWS…)
8. Se FAIL: corrige na Skill 1 e reexecuta o gate (máx. 2 ciclos)
9. Publica: (1) Código Java  (2) Análise/inventário  (3) Status COMPLETA + Evidência + Check + continuidade
```

### Pipeline de publicação

```text
INVENTÁRIO INTERNO → RASCUNHO JAVA → Gate Skill 5 → [FAIL? corrige ≤2]
  → RESPOSTA: código → análise → consolidação + Check
```

### O que o projeto cobre (capacidades)

- Conversão LSP → Java com inventário e classificação de evidência  
- Entrega consolidada (canvas / arquivo real / bloco único) — **código primeiro**, análise depois  
- Templates `USU_*` (interface IEntity + descritor `.sc`) quando o inventário exige  
- Proibição de **Senior SQL 2**; SQL em regra via links oficiais (Skill 2)  
- Armadilhas de compilação (TipCon, HorSit, MarcacaoAnterior, `execute()` sem `throws`, …)  
- Gate determinístico PASS/FAIL com métrica `falhos/total`  
- Auditoria avulsa (`check`) de artefato já gerado  
- Suite interna de QA do treinamento (Skill 4 — só manutenção, não é fluxo de usuário)

---

## Arquitetura

| Papel | Arquivo | Uso |
| :--- | :--- | :--- |
| Router | [`router.md`](router.md) | Escopo, boas-vindas, evidência, roteamento |
| Conversão | [`skill-01-conversao-lsp-java.md`](skill-01-conversao-lsp-java.md) | Fluxo do usuário (código → análise) |
| Docs | [`skill-02-base-documentacao-banco.md`](skill-02-base-documentacao-banco.md) | Interna — links oficiais e aliases |
| Catálogo | [`skill-03-base-conversao-lsp-java.md`](skill-03-base-conversao-lsp-java.md) | Interna — padrões, goldens, mecânica |
| QA | [`skill-04-testes-comportamento.md`](skill-04-testes-comportamento.md) | Interna — regressão do treinamento |
| Gate | [`skill-05-check-deterministico.md`](skill-05-check-deterministico.md) | Gate obrigatório / auditoria |

**Precedência de evidência:** docs Skill 2 → catálogo Skill 3 → padrões de compilação → anexos → validação manual.

---

## PDFs

Cópias em PDF das skills (mesma versão do Markdown):

- [`pdf/skill-01-conversao-lsp-java.pdf`](pdf/skill-01-conversao-lsp-java.pdf)
- [`pdf/skill-02-base-documentacao-banco.pdf`](pdf/skill-02-base-documentacao-banco.pdf)
- [`pdf/skill-03-base-conversao-lsp-java.pdf`](pdf/skill-03-base-conversao-lsp-java.pdf)
- [`pdf/skill-04-testes-comportamento.pdf`](pdf/skill-04-testes-comportamento.pdf)
- [`pdf/skill-05-check-deterministico.pdf`](pdf/skill-05-check-deterministico.pdf)

---

## Versionamento

| Versão | Destaque |
| :--- | :--- |
| **v1.7** | Código Java primeiro, inventário/análise depois; default bloco único sem Fase B bloqueante |
| v1.6 | Goldens G-SIT/G-CUR/G-USU; CHK-STUB; cartão de decisão; Logico/Escolha; bloqueio SDK explícito |
| v1.5 | README público (quick start/pipeline); checklist Router Skills 2/3 + gate 5 |
| v1.4 | Templates `.sc`/IEntity, DBCenter, helpers, VaPara, Eclipse literals, CHK-SCID |
| v1.3 | Mescla núcleo Treinamento (TipCon, MarcacaoAnterior, USU_*) |
| v1.2 | Renumeração 01–05 |
| v1.1 | Agente exclusivo conversão |
| v1.0 | Baseline |
