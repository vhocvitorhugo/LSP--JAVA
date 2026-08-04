<h1 align="center">LSPCodMind</h1>

<p align="center">
  <b>Framework de Agente de IA para Senior Sistemas: LSP, Engenharia Reversa e Conversão LSP → Java</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/SENIOR_SISTEMAS-HCM_%7C_ERP-blue?style=for-the-badge" alt="Senior Sistemas" />
  <img src="https://img.shields.io/badge/LSP-5.10.4-orange?style=for-the-badge" alt="LSP 5.10.4" />
  <img src="https://img.shields.io/badge/JAVA-17%2B-red?style=for-the-badge" alt="Java 17+" />
  <img src="https://img.shields.io/badge/LSPCodMind-v1.14-success?style=for-the-badge" alt="LSPCodMind v1.14" />
</p>

---

O **LSPCodMind** é um framework de agente em formato modular **Router + Skills**, focado na plataforma **Senior Sistemas**: diagnóstico de regras, engenharia reversa de legado, desenvolvimento orientado e conversão assistida LSP → Java no **Senior HCM** (Controle de Ponto e Refeitório).

**Versão atual: v1.14** — repositório de gravação GitHub alterado para `vhocvitorhugo/LSP--JAVA`; diretrizes e artefatos alinhados à nova origem de push.

---

## Principais funcionalidades

- **Mentoria Técnica** — conceitos, sintaxe LSP, arquitetura Senior, documentação e boas práticas  
- **Diagnóstico e Debug** — erros, logs, exceções, integrações, cursores e performance  
- **Desenvolvimento Orientado** — criação/refatoração de regras LSP com código completo comentado + gate Skill 9  
- **Analisador de Regras** — engenharia reversa, variáveis, fluxo de negócio e riscos  
- **Conversão LSP → Java** — inventário, mapeamento, fases A/B/C, entrega consolidada (HCM 6.10.4 / Gestão do Ponto) + gate Skill 9  
- **Check Determinístico (Skill 9)** — auditoria PASS/FAIL antes de apresentar regra gerada, convertida ou corrigida  

---

## Arquitetura

O **Prompt Router** (`router.md`) controla menu, roteamento, evidência, sigilo, proibição de Senior SQL 2 e o gate Skill 9.

| Papel | Arquivo | Menu? |
| :--- | :--- | :--- |
| Router (autoridade global) | [`router.md`](router.md) | — |
| Skills 1–5 (fluxos do usuário) | [`skill-01`](skill-01-mentoria-tecnica.md) … [`skill-05`](skill-05-conversao-lsp-java.md) | Sim |
| Base docs + links + aliases | [`skill-06-base-documentacao-banco.md`](skill-06-base-documentacao-banco.md) | Não |
| Base conversão HCM/Ponto | [`skill-07-base-conversao-lsp-java.md`](skill-07-base-conversao-lsp-java.md) | Não |
| QA de comportamento do agente | [`skill-08-testes-comportamento.md`](skill-08-testes-comportamento.md) | Não |
| Check determinístico (gate) | [`skill-09-check-deterministico.md`](skill-09-check-deterministico.md) | Automático |

### Contrato operacional

1. Router escolhe o fluxo (árvore de decisão).  
2. Skills 1–5 respondem com `Evidência` / `Bases consultadas`.  
3. Skill 5: fases **A** (inventário) → **B** (formato) → **C** (Java); publicação só após Skill 9.  
4. Skills 2/3 com código de regra: gate Skill 9 antes de publicar.  
5. Skill 8 só na manutenção do treinamento (não no atendimento).  

---

## Estrutura do repositório

| Arquivo | Responsabilidade |
| :--- | :--- |
| [`README.md`](README.md) | Documentação e versão do projeto |
| [`router.md`](router.md) | Regras globais, menu canônico, roteamento |
| [`skill-01-mentoria-tecnica.md`](skill-01-mentoria-tecnica.md) | Mentoria |
| [`skill-02-diagnostico-debug.md`](skill-02-diagnostico-debug.md) | Diagnóstico e debug |
| [`skill-03-desenvolvimento-orientado.md`](skill-03-desenvolvimento-orientado.md) | Desenvolvimento |
| [`skill-04-analisador-regras.md`](skill-04-analisador-regras.md) | Analisador de regras |
| [`skill-05-conversao-lsp-java.md`](skill-05-conversao-lsp-java.md) | Conversão LSP → Java |
| [`skill-06-base-documentacao-banco.md`](skill-06-base-documentacao-banco.md) | Links autorizados + aliases |
| [`skill-07-base-conversao-lsp-java.md`](skill-07-base-conversao-lsp-java.md) | Padrões, esqueletos e âncoras de conversão |
| [`skill-08-testes-comportamento.md`](skill-08-testes-comportamento.md) | Testes de comportamento |
| [`skill-09-check-deterministico.md`](skill-09-check-deterministico.md) | Check determinístico |

---

## Diretrizes críticas

- **Proibido Senior SQL 2** em regras com SQL/cursor.  
- **Sem achismo:** funções, tabelas e equivalências só com evidência verificável.  
- **Conversão consolidada:** canvas, arquivo real ou bloco único (sem fracionar).  
- **Gate Skill 9** obrigatório antes de apresentar regra gerada, convertida ou corrigida.  

---

## Versionamento

| Versão | Destaque |
| :--- | :--- |
| **v1.14** | Remote de gravação: `https://github.com/vhocvitorhugo/LSP--JAVA.git` |
| v1.13 | Menu com identidade; desempate 2×3×4; inventário Skill 4; ritual links; fixtures QA; métrica Skill 9; PDFs sync |
| v1.12 | Router: identidade LSPCodMind — agente especializado em regras de desenvolvimento nos sistemas Senior |
| v1.11 | README obrigatório a cada alteração de skill/router (regra no AGENTS.md) |
| v1.10 | Skills 6–9: fronteira clara, navegação Skill 7, PASS na 8, críticos-primeiro na 9 |
| v1.9 | Fusão do treinamento PDF legado (mecânica/exemplos/protocolo) no framework atual |
| v1.8 | Catálogo oficial de equivalência LSP→Java (doc Senior 6.10.4) na Skill 7 + exemplos práticos |
| v1.7 | Skills e Router em português (Brasil) |
| v1.6 | Skills 6 e 7 em arquivo único (remove `*-reference.md`) |
| v1.5 | README sincronizado no GitHub (remove badge legado v13.0) |
| v1.4 | Estilo skills.sh |
| v1.3 | Skill 9 como gate obrigatório |
| v1.2 | Criação da Skill 9 |
| v1.1 | Treinamento operacional + versionamento minor |
| v1.0 | Baseline |
