<h1 align="center">LSP→JAVA</h1>

<p align="center">
  <b>Agente de IA especializado em conversão assistida LSP → Java (Senior HCM / Gestão do Ponto)</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/SENIOR_SISTEMAS-HCM_%7C_ERP-blue?style=for-the-badge" alt="Senior Sistemas" />
  <img src="https://img.shields.io/badge/LSP-5.10.4-orange?style=for-the-badge" alt="LSP 5.10.4" />
  <img src="https://img.shields.io/badge/JAVA-17%2B-red?style=for-the-badge" alt="Java 17+" />
  <img src="https://img.shields.io/badge/LSP-JAVA-v1.2-success?style=for-the-badge" alt="LSP→JAVA v1.2" />
</p>

---

O **LSP→JAVA** é um agente em formato **Router + Skills** focado **somente** na conversão assistida de regras **LSP → Java** no **Senior HCM** (Controle de Ponto e Refeitório / Gestão do Ponto).

**Versão atual: v1.2** — skills renumeradas 01–05; todas mantidas (conversão, docs, padrões, QA interno, gate).

---

## Funcionalidades

- **Conversão LSP → Java (Skill 1)** — inventário (Fase A), escolha de formato (Fase B), Java consolidado (Fase C)  
- **Bases internas** — links/aliases oficiais (Skill 2) e catálogo/padrões HCM (Skill 3)  
- **Check determinístico (Skill 5)** — gate PASS/FAIL obrigatório antes de publicar a Fase C  
- **QA de treinamento (Skill 4)** — suite interna; não usada no atendimento  

**Fora de escopo:** mentoria genérica, diagnóstico sem conversão, criação/refatoração de LSP sem migrar para Java, engenharia reversa sem objetivo de conversão.

---

## Arquitetura

O **Prompt Router** (`router.md`) controla boas-vindas, escopo, evidência, sigilo, proibição de Senior SQL 2 e o gate Skill 5.

| Papel | Arquivo | Fluxo do usuário? | Necessária? |
| :--- | :--- | :--- | :--- |
| Router (autoridade global) | [`router.md`](router.md) | — | Sim |
| Conversão LSP → Java | [`skill-01-conversao-lsp-java.md`](skill-01-conversao-lsp-java.md) | Sim | Sim — único fluxo |
| Base docs + links + aliases | [`skill-02-base-documentacao-banco.md`](skill-02-base-documentacao-banco.md) | Não | Sim — evidência/links |
| Base conversão HCM/Ponto | [`skill-03-base-conversao-lsp-java.md`](skill-03-base-conversao-lsp-java.md) | Não | Sim — catálogo/padrões |
| QA de comportamento do agente | [`skill-04-testes-comportamento.md`](skill-04-testes-comportamento.md) | Não | Sim — regressão do treinamento |
| Check determinístico (gate) | [`skill-05-check-deterministico.md`](skill-05-check-deterministico.md) | Automático / auditoria | Sim — qualidade da Fase C |

### Contrato operacional

1. Router confirma escopo (conversão) ou recusa fora de escopo.  
2. Skill 1 responde com fases A → B → C e campos `Evidência` / `Bases consultadas`.  
3. Publicação da Fase C só após Skill 5.  
4. Skill 4 só na manutenção do treinamento.  

---

## Estrutura do repositório

| Arquivo | Responsabilidade |
| :--- | :--- |
| [`README.md`](README.md) | Documentação e versão do projeto |
| [`router.md`](router.md) | Regras globais, boas-vindas, escopo e roteamento |
| [`skill-01-conversao-lsp-java.md`](skill-01-conversao-lsp-java.md) | Conversão LSP → Java |
| [`skill-02-base-documentacao-banco.md`](skill-02-base-documentacao-banco.md) | Links autorizados + aliases |
| [`skill-03-base-conversao-lsp-java.md`](skill-03-base-conversao-lsp-java.md) | Padrões, esqueletos e âncoras de conversão |
| [`skill-04-testes-comportamento.md`](skill-04-testes-comportamento.md) | Testes de comportamento |
| [`skill-05-check-deterministico.md`](skill-05-check-deterministico.md) | Check determinístico |
| [`pdf/`](pdf/) | PDFs das skills 01–05 |

---

## Diretrizes críticas

- **Proibido Senior SQL 2** em regras com SQL/cursor.  
- **Sem achismo:** funções, tabelas e equivalências só com evidência verificável.  
- **Conversão consolidada:** canvas, arquivo real ou bloco único (sem fracionar).  
- **Gate Skill 5** obrigatório antes de apresentar Java convertido.  

---

## Versionamento

| Versão | Destaque |
| :--- | :--- |
| **v1.2** | Renumeração skills 05–09 → 01–05; auditoria: as 5 skills permanecem necessárias |
| v1.1 | Agente exclusivo LSP→JAVA; remove menus legados; boas-vindas de conversão |
| v1.0 | Baseline do repositório `LSP--JAVA` |
