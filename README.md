<h1 align="center">LSP→JAVA</h1>

<p align="center">
  <b>Agente de IA especializado em conversão assistida LSP → Java (Senior HCM / Gestão do Ponto)</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/SENIOR_SISTEMAS-HCM_%7C_ERP-blue?style=for-the-badge" alt="Senior Sistemas" />
  <img src="https://img.shields.io/badge/LSP-5.10.4-orange?style=for-the-badge" alt="LSP 5.10.4" />
  <img src="https://img.shields.io/badge/JAVA-17%2B-red?style=for-the-badge" alt="Java 17+" />
  <img src="https://img.shields.io/badge/LSP--JAVA-v1.10-success?style=for-the-badge" alt="LSP→JAVA v1.10" />
</p>

---

## O que é

O **LSP→JAVA** é um agente em formato **Router + Skills** focado **somente** na conversão assistida de regras **LSP → Java** no **Senior HCM / Gestão do Ponto**.

Ele **não** é uma aplicação web nem um compilador: é o **treinamento** (Markdown) que um assistente de IA carrega para converter regras com inventário, evidência, Java consolidado e gate de conformidade.

**Versão atual: v1.10** — alinhamento [Agent Skills](https://agentskills.io/home) / [skills.sh](https://www.skills.sh/): Skill 3 com **progressive disclosure** (núcleo + `skill-03-referencia-*`); Router/Skill 4 com Saída/Relacionados/Quando usar. Mantém Java primeiro, TODO, G-MIX, gate com evidência e Skill 2 enxuta. Itens de API que dependem de SDK ficam **bloqueados até validação com jar/projeto**.

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

1. Carregue no assistente o [`router.md`](router.md) e as skills `skill-01` … `skill-05` deste repositório (no atendimento: Router + Skill 1 primeiro; Skill 3 por âncora; Skill 4 só manutenção).
2. Digite `inicio` / `menu` / `ajuda` (opcional) para ver as boas-vindas.
3. Cole a regra LSP (ou anexe o arquivo) e peça para **converter** / **migrar**.
4. Opcional: diga o formato — **canvas**, **documento/arquivo** ou **bloco único** (se omitir, usa bloco único).
5. Receba o **Java consolidado no topo**, depois inventário/análise e o Check com evidências por crítico.
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
3. Skill 1 — gera rascunho Java completo (TODO+sugestão se API desconhecida; sem inventar confirmada)
4. Formato: canvas/documento se pedido; senão padrão bloco único (sem perguntar)
5. Consulta Skill 3: núcleo + referência catalogo/acesso/exemplos-goldens **só por âncora**; Skill 2 só para links
6. Ordem de decisão: contexto → API semântica → USU_* → R*/TipCon → validacao_manual+TODO
7. Gate Skill 5: críticos com evidência observável + falhos/total
8. Se FAIL: corrige na Skill 1 e reexecuta o gate (máx. 2 ciclos)
9. Publica: (1) Código Java  (2) Análise/inventário  (3) Status COMPLETA + Evidência + Check + continuidade
```

### Pipeline de publicação

```text
INVENTÁRIO INTERNO → RASCUNHO JAVA → Gate Skill 5 (evidência) → [FAIL? corrige ≤2]
  → RESPOSTA: código → análise → consolidação + Check
```

### O que o projeto cobre (capacidades)

- Conversão LSP → Java com inventário e classificação de evidência  
- Entrega consolidada (canvas / arquivo real / bloco único) — **código primeiro**, análise depois  
- Desempate TODO quando falta equivalência (bloco completo, sem stub)  
- Goldens G-SIT / G-CUR / G-USU / **G-MIX**  
- Templates `USU_*` (interface IEntity + descritor `.sc`) quando o inventário exige  
- Proibição de **Senior SQL 2**; SQL em regra via links oficiais (Skill 2)  
- Gate determinístico PASS/FAIL com evidência por crítico e métrica `falhos/total`  
- Auditoria avulsa (`check`) de artefato já gerado  
- Suite interna de QA (Skill 4 — folha de corrida; só manutenção)

---

## Arquitetura

| Papel | Arquivo | Uso |
| :--- | :--- | :--- |
| Router | [`router.md`](router.md) | Escopo, boas-vindas, evidência, carga seletiva |
| Conversão | [`skill-01-conversao-lsp-java.md`](skill-01-conversao-lsp-java.md) | Fluxo do usuário (código → análise) |
| Docs | [`skill-02-base-documentacao-banco.md`](skill-02-base-documentacao-banco.md) | Interna — links oficiais e aliases |
| Catálogo | [`skill-03-base-conversao-lsp-java.md`](skill-03-base-conversao-lsp-java.md) + [`skill-03-referencia-*.md`](skill-03-referencia-catalogo.md) | Interna — núcleo + progressive disclosure |
| QA | [`skill-04-testes-comportamento.md`](skill-04-testes-comportamento.md) | Interna — regressão do treinamento |
| Gate | [`skill-05-check-deterministico.md`](skill-05-check-deterministico.md) | Gate obrigatório / auditoria |

**Precedência de evidência:** docs Skill 2 → catálogo Skill 3 → padrões de compilação → anexos → validação manual.

---

## PDFs

Cópias em PDF (mesma versão do Markdown):

- [`pdf/router.pdf`](pdf/router.pdf)
- [`pdf/skill-01-conversao-lsp-java.pdf`](pdf/skill-01-conversao-lsp-java.pdf)
- [`pdf/skill-02-base-documentacao-banco.pdf`](pdf/skill-02-base-documentacao-banco.pdf)
- [`pdf/skill-03-base-conversao-lsp-java.pdf`](pdf/skill-03-base-conversao-lsp-java.pdf)
- [`pdf/skill-03-referencia-catalogo.pdf`](pdf/skill-03-referencia-catalogo.pdf)
- [`pdf/skill-03-referencia-acesso-dados.pdf`](pdf/skill-03-referencia-acesso-dados.pdf)
- [`pdf/skill-03-referencia-exemplos-goldens.pdf`](pdf/skill-03-referencia-exemplos-goldens.pdf)
- [`pdf/skill-04-testes-comportamento.pdf`](pdf/skill-04-testes-comportamento.pdf)
- [`pdf/skill-05-check-deterministico.pdf`](pdf/skill-05-check-deterministico.pdf)

---

## Versionamento

| Versão | Destaque |
| :--- | :--- |
| **v1.10** | Agent Skills: Skill 3 progressive disclosure; Router/Skill 4 seções Saída/Quando usar; AGENTS alinhado |
| v1.9 | Skill 2: só links LSP→Java HCM/Ponto (remove WS/FTP/AD/eventos/ERP) |
| v1.8 | TODO desempate; G-MIX + índice Skill 3; gate com evidência; Skill 4 folha/fixtures; PDF router; carga seletiva |
| v1.7 | Código Java primeiro, inventário/análise depois; default bloco único sem Fase B bloqueante |
| v1.6 | Goldens G-SIT/G-CUR/G-USU; CHK-STUB; cartão de decisão; Logico/Escolha; bloqueio SDK explícito |
| v1.5 | README público (quick start/pipeline); checklist Router Skills 2/3 + gate 5 |
| v1.4 | Templates `.sc`/IEntity, DBCenter, helpers, VaPara, Eclipse literals, CHK-SCID |
| v1.3 | Mescla núcleo Treinamento (TipCon, MarcacaoAnterior, USU_*) |
| v1.2 | Renumeração 01–05 |
| v1.1 | Agente exclusivo conversão |
| v1.0 | Baseline |
