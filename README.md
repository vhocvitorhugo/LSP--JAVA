<h1 align="center">LSP→JAVA</h1>

<p align="center">
  <b>Agente de IA especializado em conversão assistida LSP → Java (Senior HCM / Gestão do Ponto)</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/SENIOR_SISTEMAS-HCM_%7C_ERP-blue?style=for-the-badge" alt="Senior Sistemas" />
  <img src="https://img.shields.io/badge/LSP-5.10.4-orange?style=for-the-badge" alt="LSP 5.10.4" />
  <img src="https://img.shields.io/badge/JAVA-17%2B-red?style=for-the-badge" alt="Java 17+" />
  <img src="https://img.shields.io/badge/LSP-JAVA-v1.6-success?style=for-the-badge" alt="LSP→JAVA v1.6" />
</p>

---

O **LSP→JAVA** é um agente em formato **Router + Skills** focado **somente** na conversão assistida de regras **LSP → Java** no **Senior HCM / Gestão do Ponto**.

**Versão atual: v1.6** — caminho qualidade: cartão de decisão, goldens G-SIT/G-CUR/G-USU, `CHK-STUB`, sintaxe `Logico`/`Escolha`, norma `USU_*`. Itens de API que dependem de SDK (`TipoHoraExtra`, `@Transactional`) ficam **bloqueados até validação com jar/projeto** (teto ~9.x sem SDK).

**Para quem:** analistas e desenvolvedores que migram regras LSP de ponto para Java no ecossistema Senior.

**Fora de escopo:** mentoria genérica, debug sem conversão, criar/refatorar LSP sem migrar para Java, ou só engenharia reversa.

---

## Quick start

1. Carregue o agente com [`router.md`](router.md) e as skills `skill-01` … `skill-05` deste repositório.
2. Digite `inicio`, `menu` ou `ajuda` para ver as boas-vindas.
3. Cole a regra LSP (ou anexe o arquivo) e peça para **converter**.
4. Opcional: diga o formato — **canvas**, **documento/arquivo** ou **bloco único**.
5. Para auditar uma conversão já gerada: peça `check` / auditoria.

---

## Pipeline de conversão

```text
A  Inventário + mapeamento + plano     (sem Java final)
B  Escolha de formato (se ainda não pediu)
C  Java completo → gate Skill 5 → resposta (+ resumo do check)
```

| Fase | O que acontece |
| :--- | :--- |
| **A** | Inventário LSP→Java, evidências e plano |
| **B** | Pergunta formato só se você não indicou |
| **C** | Código consolidado; gate determinístico antes de publicar |

**Ordem de decisão (Skill 1):** contexto → API semântica → `USU_*` (IEntity/`.sc`) → `R*`/TipCon (ContextSession) → `validacao_manual` sem omitir bloco.

---

## Arquitetura

| Papel | Arquivo | Uso |
| :--- | :--- | :--- |
| Router | [`router.md`](router.md) | Escopo, boas-vindas, evidência, roteamento |
| Conversão | [`skill-01-conversao-lsp-java.md`](skill-01-conversao-lsp-java.md) | Fluxo do usuário (fases A/B/C) |
| Docs | [`skill-02-base-documentacao-banco.md`](skill-02-base-documentacao-banco.md) | Interna — links oficiais e aliases |
| Catálogo | [`skill-03-base-conversao-lsp-java.md`](skill-03-base-conversao-lsp-java.md) | Interna — padrões, goldens, mecânica |
| QA | [`skill-04-testes-comportamento.md`](skill-04-testes-comportamento.md) | Interna — suite de regressão do treinamento |
| Gate | [`skill-05-check-deterministico.md`](skill-05-check-deterministico.md) | Gate obrigatório / auditoria (`CHK-STUB`, …) |

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
| **v1.6** | Goldens G-SIT/G-CUR/G-USU; CHK-STUB; cartão de decisão; Logico/Escolha; bloqueio SDK explícito |
| v1.5 | README público (quick start/pipeline); checklist Router Skills 2/3 + gate 5 |
| v1.4 | Templates `.sc`/IEntity, DBCenter, helpers, VaPara, Eclipse literals, CHK-SCID |
| v1.3 | Mescla núcleo Treinamento (TipCon, MarcacaoAnterior, USU_*) |
| v1.2 | Renumeração 01–05 |
| v1.1 | Agente exclusivo conversão |
| v1.0 | Baseline |
