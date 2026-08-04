<h1 align="center">LSP→JAVA</h1>

<p align="center">
  <b>Agente de IA especializado em conversão assistida LSP → Java (Senior HCM / Gestão do Ponto)</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/SENIOR_SISTEMAS-HCM_%7C_ERP-blue?style=for-the-badge" alt="Senior Sistemas" />
  <img src="https://img.shields.io/badge/LSP-5.10.4-orange?style=for-the-badge" alt="LSP 5.10.4" />
  <img src="https://img.shields.io/badge/JAVA-17%2B-red?style=for-the-badge" alt="Java 17+" />
  <img src="https://img.shields.io/badge/LSP-JAVA-v1.4-success?style=for-the-badge" alt="LSP→JAVA v1.4" />
</p>

---

O **LSP→JAVA** é um agente em formato **Router + Skills** focado **somente** na conversão assistida de regras **LSP → Java** no **Senior HCM**.

**Versão atual: v1.4** — profundidade de compilação: templates IEntity/`.sc`, DBCenter, cursores, helpers sanitizados, VaPara, mensagens Eclipse e CHK-SCID — sem engolir negócio de cliente do playbook externo.

---

## Funcionalidades

- **Conversão (Skill 1)** — A/B/C + artefatos `USU_*` após inventário  
- **Docs (Skill 2)** — links oficiais; ContextSession ≠ SQL 2  
- **Base conversão (Skill 3)** — catálogo 6.10.4 + `padrao_compilacao` (templates, DML, helpers)  
- **QA (Skill 4)** — suite interna  
- **Gate (Skill 5)** — checks ampliados (SCID, THROWS, TIPCON, …)  

**Precedência:** docs Skill 2 → catálogo Skill 3 → `padrao_compilacao` → anexos → `validacao_manual`.

---

## Arquitetura

| Papel | Arquivo |
| :--- | :--- |
| Router | [`router.md`](router.md) |
| Conversão | [`skill-01-conversao-lsp-java.md`](skill-01-conversao-lsp-java.md) |
| Docs | [`skill-02-base-documentacao-banco.md`](skill-02-base-documentacao-banco.md) |
| Catálogo + mecânica | [`skill-03-base-conversao-lsp-java.md`](skill-03-base-conversao-lsp-java.md) |
| QA | [`skill-04-testes-comportamento.md`](skill-04-testes-comportamento.md) |
| Gate | [`skill-05-check-deterministico.md`](skill-05-check-deterministico.md) |

---

## Versionamento

| Versão | Destaque |
| :--- | :--- |
| **v1.4** | Templates `.sc`/IEntity, DBCenter, helpers, VaPara, Eclipse literals, CHK-SCID |
| v1.3 | Mescla núcleo Treinamento (TipCon, MarcacaoAnterior, USU_*) |
| v1.2 | Renumeração 01–05 |
| v1.1 | Agente exclusivo conversão |
| v1.0 | Baseline |
