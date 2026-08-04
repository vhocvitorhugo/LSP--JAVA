# Changelog — LSP→JAVA

## [docs] — Atualização de 04/08/2026

### technicalNotes
- `CHANGELOG.md` passa a ser versionado e publicado no GitHub (autorizado pelo mantenedor).

## [v1.6] — Atualização de 04/08/2026
Versão: **v1.5 → v1.6**

### features
- Skill 3: goldens ponta a ponta **G-SIT**, **G-CUR**, **G-USU**.
- Skill 1: cartão de decisão (contexto → API → USU_* → R*/TipCon → manual) + anti-stub.
- Skill 5: check crítico **CHK-STUB**.

### improvements
- Skill 3: mapeamento fechado `Logico` / `Escolha`/`Caso`; âncoras 80%; stubs removidos (`DiferencaMarcacaoDiurnoNoturno`, `MarcacoesInvalidas`); norma capitalização `USU_*`.
- Skill 3: itens SDK (`TipoHoraExtra`, `@Transactional`, null `LocalDate`) **bloqueados até SDK** (não `confirmada` inventada).
- Skill 4: protocolo pós-bump + matriz mínima + casos 21–24 (goldens / CHK-STUB).
- README: v1.6 e nota de teto ~9.x sem SDK.

### technicalNotes
- `.agents/AGENTS.md`: ritual links Skill 2 + registro Suite Skill 4 no Changelog; texto de versionamento atualizado.
- Suite Skill 4 crítica: PASS (revisão mental matriz mínima + alinhamento goldens/CHK-STUB).
- Links Skill 2: ok (sem alteração de URLs nesta entrega; paridade de versão apenas).
- Paridade v1.6 em router + skills 01–05; PDFs regenerados.

## [v1.5] — Atualização de 04/08/2026
Versão: **v1.4 → v1.5**

### improvements
- README público: quick start, pipeline A/B/C, papéis das skills, links PDF, escopo/fora de escopo.
- Router: checklist final corrigido (`Skill 2/7` → Skills 2/3 + gate Skill 5 na Fase C).

### technicalNotes
- Paridade de versão v1.5 em `router.md` e skills 01–05; PDFs regenerados.

## [v1.4] — Atualização de 04/08/2026
Versão: **v1.3 → v1.4**

### improvements
- Skill 3: templates IEntity + `.sc` JSON; DBCenter INSERT; ICursor multilinha/`setOrder`/CursorUtil; getters encadeados + `ISeparacaoHoras`; VaPara (3 padrões) + operadores; helpers sanitizados; mensagens Eclipse literais; checklist pré-entrega; tabela ⚠️ pendente; pontos InicioCalculo/AposGravar.
- Skill 5: `CHK-SCID`, `CHK-USULONG`.
- Skill 1: checklist C com templates/`.sc` id=filename.
- Skill 4: caso `CHK-SCID` / `.sc` JSON válido após inventário.

### technicalNotes
- Fecha gaps P0/P1 da análise pós-v1.3 vs pasta local `Treinamento/` (sem schemas/sits Engelmig como `confirmada`).

## [v1.3] — Atualização de 04/08/2026
Versão: **v1.2 → v1.3**

### features
- Mescla núcleo do playbook Treinamento (TipCon, MarcacaoRegra, USU_*/`.sc`, gate ampliado).

## [v1.2] — Atualização de 04/08/2026
Versão: **v1.1 → v1.2**

### improvements
- Renumeração skills `01–05`.

## [v1.1] — Atualização de 04/08/2026
Versão: **v1.0 → v1.1**

### features
- Agente exclusivo LSP → Java.

## [v1.0] — Atualização de 04/08/2026
Versão: **baseline v1.0**
