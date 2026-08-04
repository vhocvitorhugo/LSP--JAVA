<h1 align="center">LSP→JAVA</h1>

<p align="center">
  <b>Agente de IA especializado em conversão assistida LSP → Java (Senior HCM / Gestão do Ponto)</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/SENIOR_SISTEMAS-HCM_%7C_ERP-blue?style=for-the-badge" alt="Senior Sistemas" />
  <img src="https://img.shields.io/badge/LSP-5.10.4-orange?style=for-the-badge" alt="LSP 5.10.4" />
  <img src="https://img.shields.io/badge/JAVA-17%2B-red?style=for-the-badge" alt="Java 17+" />
  <img src="https://img.shields.io/badge/LSP-JAVA-v1.3-success?style=for-the-badge" alt="LSP→JAVA v1.3" />
</p>

---

O **LSP→JAVA** é um agente em formato **Router + Skills** focado **somente** na conversão assistida de regras **LSP → Java** no **Senior HCM** (Controle de Ponto e Refeitório / Gestão do Ponto).

**Versão atual: v1.3** — mescla do playbook `Treinamento/` (APIs e anti-padrões confirmados em compilação) nas bases de conversão, sem abrir mão de A/B/C, evidência, SQL 2 banido e gate.

---

## Funcionalidades

- **Conversão LSP → Java (Skill 1)** — inventário (Fase A), formato (Fase B), Java consolidado (Fase C); artefatos `USU_*` (interface + `.sc`) quando o inventário exigir  
- **Bases internas** — links oficiais (Skill 2); catálogo + padrões de compilação + acesso a dados (Skill 3)  
- **Check determinístico (Skill 5)** — gate ampliado (TipCon, MarcacaoAnterior, `.sc`, throws, sessões)  
- **QA de treinamento (Skill 4)** — suite interna  

**Fora de escopo:** mentoria genérica, diagnóstico sem conversão, criação/refatoração de LSP sem migrar para Java, engenharia reversa sem objetivo de conversão.

---

## Arquitetura

| Papel | Arquivo | Fluxo do usuário? |
| :--- | :--- | :--- |
| Router | [`router.md`](router.md) | — |
| Conversão | [`skill-01-conversao-lsp-java.md`](skill-01-conversao-lsp-java.md) | Sim |
| Docs / aliases | [`skill-02-base-documentacao-banco.md`](skill-02-base-documentacao-banco.md) | Não |
| Catálogo + mecânica | [`skill-03-base-conversao-lsp-java.md`](skill-03-base-conversao-lsp-java.md) | Não |
| QA comportamento | [`skill-04-testes-comportamento.md`](skill-04-testes-comportamento.md) | Não |
| Gate | [`skill-05-check-deterministico.md`](skill-05-check-deterministico.md) | Automático / auditoria |

**Precedência:** docs Skill 2 → catálogo Skill 3 → `padrao_compilacao` → anexos → `validacao_manual`.

---

## Diretrizes críticas

- **Proibido Senior SQL 2** (ContextSession/DBCenter ≠ SQL 2).  
- **Sem achismo** — evidência verificável.  
- **Conversão consolidada** + **gate Skill 5** antes de publicar.  
- **`.sc` só para `USU_*`** — nunca para tabela `R*`.  

---

## Versionamento

| Versão | Destaque |
| :--- | :--- |
| **v1.3** | Mescla Treinamento: APIs/compilação, USU_*/.sc, checks TipCon/MarcacaoAnterior/throws |
| v1.2 | Renumeração skills 01–05 |
| v1.1 | Agente exclusivo conversão |
| v1.0 | Baseline `LSP--JAVA` |
