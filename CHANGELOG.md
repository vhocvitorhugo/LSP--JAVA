# Changelog — LSP→JAVA

## [v1.10] — Atualização de 06/08/2026
Versão: **v1.9 → v1.10**

### features
- Skill 3 em **progressive disclosure** (Agent Skills): núcleo `skill-03-base-conversao-lsp-java.md` (~367 linhas) + referências `skill-03-referencia-catalogo.md`, `skill-03-referencia-acesso-dados.md`, `skill-03-referencia-exemplos-goldens.md`.

### improvements
- Router: seções **Saída** e **Relacionados**; carga seletiva aponta para `skill-03-referencia-*`.
- Skill 4: **Quando usar / não usar** + **Saída** (folha de corrida).
- AGENTS.md: adaptação explícita do padrão agentskills.io / skills.sh (layout flat, frontmatter, progressive disclosure).

### technicalNotes
- Alinhamento agentskills.io: frontmatter válido; corpo núcleo Skill 3 com menos de 500 linhas; referências sob demanda.
- Layout permanece flat na raiz (adaptação documentada; não migra para pastas `SKILL.md`).
- Suite Skill 4 crítica: PASS (casos 21/23/24/25 — goldens agora em referencia-exemplos-goldens).
- Folha Skill 4: 4/4 casos goldens com evidência de caminho atualizado.
- Links Skill 2: ok (sem alteração de URLs).
- Paridade v1.10; PDFs regenerados (router + skills 01–05 + referências 03).

## [v1.9] — Atualização de 06/08/2026
Versão: **v1.8 → v1.9**

### improvements
- Skill 2: base de links restrita ao projeto LSP→Java HCM/Ponto.

### technicalNotes
- Links Skill 2 removidos (fora de escopo): Integração (WS/HTTP/JSON/FTP); Acesso (usuários/AD/diretórios); Eventos (workflow/relatórios/compromissos/gerais); máscara CBDS; SP/proprietária/arquivos-texto; aliases ERP (`E120NFV`/`E140NFV`).
- Links Skill 2 mantidos: equivalência HCM; índice das funções; sintaxe LSP (comandos/variáveis/limites); SQL em regra; aliases HCM.
- Links Skill 2: ok (lista reduzida revisada; URLs remanescentes alinhadas ao uso em Router/Skill 1/3/4).
- Suite Skill 4 crítica: PASS (casos 6/15 — SQL em regra + citação só da lista restante).
- Folha Skill 4: 2/2 casos tocados (6, 15) com evidência de link único de SQL em regra.
- Paridade v1.9 em router + skills 01–05; PDFs regenerados (skills + router).

## [v1.8] — Atualização de 06/08/2026
Versão: **v1.7 → v1.8**

### features
- Skill 1 / Router: **desempate TODO** (`// TODO: problema — Sugestão:`) — bloco completo sem inventar `confirmada`.
- Skill 3: **índice símbolo LSP → seção** + golden **G-MIX** (HorSit + `R*` + `USU_*`).
- Skill 5: resumo do gate exige **tabela de críticos aplicáveis + evidência observável** (sem evidência → INCOMPLETO).
- Skill 4: **folha de corrida** pós-bump; fixtures **F-TODO / F-MIX / F-LONG**; casos 25–27.
- PDF do **Router** (`pdf/router.pdf`) + carga seletiva de contexto no Router.

### improvements
- Política de regra longa: entrega consolidada; preferir canvas/arquivo real; nunca fragmentar.
- `CHK-STUB`: TODO no formato Skill 1 = PASS (não conta como stub).
- README / AGENTS.md locais alinhados ao pipeline inventário interno → Java → gate → código→análise (sem Fase B).

### technicalNotes
- Paridade v1.8 em router + skills 01–05; PDFs regenerados (skills + router).
- Suite Skill 4 crítica: PASS (folha: 1,4,5,6,8,13,17/21,20/22,23,24,25,26 com evidência de alinhamento textual).
- Folha Skill 4: 12/12 casos da matriz mínima cobertos por revisão de critérios + fixtures.
- Links Skill 2: ok (sem alteração de URLs; paridade de versão).

## [v1.7] — Atualização de 06/08/2026
Versão: **v1.6 → v1.7**

### features
- Skill 1 / Router: entrega pública **código Java primeiro**, inventário/análise depois, na mesma resposta pós-gate.
- Formato omitido → padrão **`bloco único`** (sem Fase B bloqueante / sem perguntar antes do Java).

### improvements
- Skill 4: casos 3/4/11/17/18 alinhados à nova ordem e ao default de formato.
- Skill 5: `CHK-INV` / `CHK-MAP` aceitam inventário/mapeamento **após** o código.
- README: passo a passo usuário/agente e pipeline atualizados.

### technicalNotes
- Paridade v1.7 em router + skills 01–05; PDFs regenerados.
- Suite Skill 4 crítica: PASS (revisão mental matriz mínima + casos 3/4 ordem código→análise).
- Links Skill 2: ok (sem alteração de URLs nesta entrega; paridade de versão apenas).

## [docs] — Atualização de 04/08/2026

### technicalNotes
- `CHANGELOG.md` passa a ser versionado e publicado no GitHub (autorizado pelo mantenedor).
- README: corrige badge v1.6 (404 no shields.io); inclui boas-vindas/como usar canônicos, passo a passo do usuário e do agente, roteamento e capacidades alinhadas ao Router.

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
