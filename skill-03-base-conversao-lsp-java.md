---
name: base-conversao-lsp-java
description: >-
  Núcleo de padrões LSP→Java (HCM 6.10.4 / Gestão do Ponto): restrições,
  workflow, tipagem, esqueletos e armadilhas. Use a partir da Skill 1 após
  Skill 2. Carregue sob demanda skill-03-referencia-catalogo,
  skill-03-referencia-acesso-dados e skill-03-referencia-exemplos-goldens.
  Nunca invente método ausente no catálogo ou na Skill 2.
---

# Skill 3 · Base de Conversão LSP → Java
Versão: v1.11 · Interna · `skill-03-base-conversao-lsp-java.md`

Skill interna — **não** é fluxo de usuário. Aplique as regras globais do Router. Em conflito de assinatura, **revalide na Skill 2 / página oficial**.

**Fronteira:** Skill 2 = links/aliases; **este núcleo** = mecânica + tipagem + esqueletos + armadilhas; catálogo/acesso/exemplos = **referências** `skill-03-referencia-*`.  
**Precedência:** docs oficiais Skill 2 → catálogo (referencia-catalogo) → padrões `padrao_compilacao` (Eclipse) → anexos sanitizados → `validacao_manual`.  
**Crescimento do catálogo `confirmada`:** só com doc oficial / Skill 2. Achados de compilação entram como `padrao_compilacao`, não como inventados.

## Como consultar (ordem obrigatória)

```text
A. Restrições + Regra de ouro + Invariantes   ← nunca pular (neste arquivo)
B. Workflow (6 passos)
C. Tipos / sintaxe / VaPara / Funcao (se necessário)
D. Catálogo — skill-03-referencia-catalogo (só a família)
E. Acesso a dados — skill-03-referencia-acesso-dados (se cursor/SQL/USU_*)
F. Armadilhas Eclipse + checklist (neste arquivo)
G. Exemplos/goldens — skill-03-referencia-exemplos-goldens (só o análogo)
H. Saída tipada para a Skill 1
```

Não leia o catálogo inteiro de ponta a ponta. Localize a **família** no índice. Em conflito de assinatura, **revalide na Skill 2**.

## Índice rápido do arquivo

| Precisa de… | Vá para |
|---|---|
| Proibições / minutos / Sem Situacao.getMinutos | Restrições absolutas |
| Modelo mental LSP→contexto | Regra de ouro |
| Passo a passo | Workflow |
| Tipagem / Se→if / Logico / Escolha / VaPara | Tipos e sintaxe |
| Esqueleto Apuracao / Consistência / BH | Esqueletos + tipos de regra |
| `DatPro`, `HorSit`, `FPxMar`, históricos… | **referencia-catalogo** → família |
| TipCon / MarcacaoRegra / overloads HorSit | **referencia-catalogo** + notas `padrao_compilacao` |
| Cursor `USU_*` / `.sc` / ContextSession | **referencia-acesso-dados** |
| Erros Eclipse / anti-padrões | Armadilhas |
| CalculaQtdMinutos / interjornada / TipCon SQL | **referencia-exemplos-goldens** |
| Templates IEntity / `.sc` / DBCenter | **referencia-acesso-dados** |
| VaPara / operadores | Tipos e sintaxe |
| Goldens G-SIT / G-CUR / G-USU / G-MIX | **referencia-exemplos-goldens** |
| InicioCalculo / AposGravar | Outros pontos |
| ⛔ SDK / ⚠️ pendente | Itens pendentes (SDK) |
| Campos LSP conflitantes | Tabela conflitantes |

### Âncoras 80% (não leia o arquivo inteiro)

| Se a regra tem… | Vá direto para |
|---|---|
| `HorSit` / situações / minutos | Catálogo → Situações + **G-SIT** |
| Marcações / `FPxMar` / `MarcacaoAnterior` | Catálogo → Marcações + Exemplos |
| `TipCon` / `R034FUN` | Campos conflitantes + TipCon via ContextSession |
| Cursor `USU_*` / interface / `.sc` | Acesso a dados + **G-USU** |
| Cursor `R*` / `CriarCursor` | Acesso a dados + **G-CUR** (API primeiro) |
| `VaPara` / labels | Tipos e sintaxe → VaPara |
| INSERT/UPDATE/DELETE | DBCenter (não ContextSession) |
| Situação + `R*` + `USU_*` juntos | exemplos-goldens → **G-MIX** |

### Índice símbolo LSP → seção (busca rápida)

| Símbolo / gatilho LSP | Seção |
|---|---|
| `HorSit` / `setHorSit` / situação / minutos | referencia-catalogo · G-SIT |
| `FPxMar` / `FLeMar` / `MarcacaoAnterior` / marcações | Catálogo → Marcações · Exemplos · `CHK-MARANT` |
| `TipCon` / `R034FUN` | catalogo (Campos) · exemplos TipCon |
| `CriarCursor` / `AbrirCursor` / `R030EMP` / `R014SIN` / `R*` | Acesso a dados · **G-CUR** (sem `.sc`) |
| `USU_*` / tabela custom | Acesso a dados · templates IEntity/`.sc` · **G-USU** |
| `HorSit` + `R*` + `USU_*` na mesma regra | **G-MIX** |
| `DatPro` / `HorSis` / data sistema | Catálogo → Data / sistema |
| `TotSit` / totalizador | Catálogo → Situações / totalizadores |
| `VaPara` / labels | Tipos e sintaxe → VaPara |
| `Escolha` / `Caso` / `Logico` | Tipos e sintaxe |
| `End` / múltiplos retornos | Exemplos End → retorno |
| `ExecSQL` / INSERT/UPDATE/DELETE | DBCenter · **nunca** Senior SQL 2 |
| `Mensagem(` | Restrições · `mensagemLog` / exceção de domínio |
| `InicioCalculo` / `AposGravar` | Outros pontos de customização |
| `TipoHoraExtra` / `@Transactional` | Itens pendentes (SDK) ⛔ |
| Método ausente no catálogo | Skill 2 Índice das Funções → `validacao_manual` + TODO (Skill 1) |


## Progressive disclosure (Agent Skills)

Este arquivo é o **núcleo** (<500 linhas). Detalhes sob demanda:

| Precisa de… | Carregar |
|---|---|
| Catálogo de equivalência / famílias / TipCon / constantes | [`skill-03-referencia-catalogo.md`](skill-03-referencia-catalogo.md) |
| ICursor / `.sc` / ContextSession / DBCenter / IEntity | [`skill-03-referencia-acesso-dados.md`](skill-03-referencia-acesso-dados.md) |
| Exemplos sanitizados + goldens G-SIT/G-CUR/G-USU/G-MIX | [`skill-03-referencia-exemplos-goldens.md`](skill-03-referencia-exemplos-goldens.md) |

**Não** leia as três referências de ponta a ponta — só a âncora necessária (índice símbolo no núcleo).

## Fontes oficiais

| Fonte | URL | Uso |
|---|---|---|
| Equivalência das funções de regras | https://documentacao.senior.com.br/gestao-de-pessoas-hcm/6.10.4/informacoes-adicionais/rotinas/gpo/integracao-controle-ponto-refeitorio/equivalencia-funcoes-regras.htm | Mapa oficial |
| Índice das Funções HCM 6.10.4 | https://documentacao.senior.com.br/gestao-de-pessoas-hcm/6.10.4/customizacoes/funcoes.htm | Assinatura + **contexto** do método |

Catálogo abaixo: evidência `confirmada` (salvo nota). Exemplos: `padrao_anexo`.  
**Assinatura/contexto incompletos no catálogo** → abrir Índice das Funções (Skill 2) antes de gerar código.

## Quando usar / não usar

| Usar | Não usar |
|---|---|
| Converter/mapear variáveis e funções de apuração LSP→Java | Só mentoria; inventar método; só citar link (Skill 2) |

## Restrições absolutas

1. Preferir o catálogo; se faltar → Skill 2 → `validacao_manual` (não inventar).  
2. Horas em APIs de ponto = **minutos inteiros** (`int`, não `double` solto).  
3. SQL/cursor → API semântica do catálogo **antes** de EntitySession/ContextSession — exceto tabela **`USU_*` custom** sem API (aí ICursor+`.sc`).  
4. **Proibido** `getSituacao(...).getMinutos()` / `setMinutos(...)` — use `getHorSit` / `setHorSit` / `zeraHorasSituacao`.  
5. Sanitize nomes de cliente em exemplos anexados; package do projeto é **parâmetro** (ex. sanitizado `gestaopontoCustom`) — nunca vazar cliente.  
6. Sem `Mensagem()`/popup em apuração — preferir `mensagemLog`.  
7. Confirmar se o método existe no **contexto** da regra (apuração ≠ consistência ≠ BH ≠ geral).  
8. `execute()` **sem** `throws Exception`; auxiliares `private` no **nível da classe** (nunca aninhados).  
9. ContextSession/DBCenter da plataforma **≠** Senior SQL 2 (SQL 2 continua proibido).

## Regra de ouro

LSP e Java diferem no **modelo de execução**: variáveis/funções globais LSP → **métodos no objeto de contexto**.  
Quem só troca `Inicio/Fim` por `{ }` produz código que não compila.

## Workflow (6 passos)

1. Identificar contexto (apuração / consistência / bloqueio / fechamento BH / geral).  
2. Inventariar construções LSP.  
3. Mapear no catálogo (nome **e** ordem de parâmetros).  
4. Traduzir mecânica (getters/setters, arrays→métodos, cursor→`List`, `End`→retorno).  
5. Traduzir sintaxe (`Se`→`if`, `=` comparação→`==`/`.isEqual()`, etc.).  
6. Revisar armadilhas.

## Invariantes

1. Toda variável/função de contexto LSP → chamada de método.  
2. Não inventar assinatura.  
3. Conferir ordem de parâmetros.  
4. Horas = minutos inteiros.  
5. Tipagem forte Java.  
6. Sem popup em apuração.  
7. Arrays indexados → métodos/coleções (não `getApuDiu(1)` inventado).  
8. Método deve existir no **contexto** da regra.

## Tipos e sintaxe

| LSP | Java |
|---|---|
| `Numero` inteiro | `int` / `long` |
| `Numero` decimal | `double` |
| `Alfa` | `String` |
| `Logico` / lógico `0`/`1` | `boolean` (`0`→`false`, `1`→`true`) |
| `Data` | `LocalDate` (ou padrão do SDK — não misturar Joda + `java.time` sem necessidade) |
| `Hora` (minutos) | `int` minutos |
| marcação | `MarcacaoRegra` (`padrao_compilacao`; preferir a `Marcacao` genérica) |
| `Se` / `Senao` / `Enquanto` / `Inicio`/`Fim` | `if` / `else` / `while` / `{ }` |
| `Escolha` / `Caso` / `OutroCaso` | `switch` (sem fall-through acidental) **ou** `if/else` encadeado |
| `Vapara` / labels | early `return`; `break`/`continue`; ou flag + `do { } while(false)` |
| `Funcao` sem `end` | `private void` no nível da classe |
| `Funcao` com 1 `end` | retorno tipado do método |
| `Funcao` com vários `end` | `int[]` / objeto (não closures aninhadas) |
| `Numero[n]` array | `int[n+1]` ou `double[n+1]` (LSP 1-based → Java 0-based) |
| `Tabela` | `List<record>` / classe interna |
| `@ ... @` | `//` |
| `=` comparação | `==` / `.isEqual()` / `.equals()` |
| `<>` | `!=` |
| decimal `,` | `.` |
| `e` / `ou` / `nao` | `&&` / `||` / `!` |
| `RestoDivisao(a,b)` | `a % b` |
| `Mensagem(...)` em regra | exceção de domínio (`BusinessException` / `RegraApuracaoException`) — não popup |

### Escolha / Caso (`padrao_compilacao`)

```lsp
Escolha (nOpcao)
  Caso 1
    @ ...
  Caso 2
    @ ...
  OutroCaso
    @ ...
FimEscolha;
```

```java
switch (nOpcao) {
    case 1:
        // ...
        break;
    case 2:
        // ...
        break;
    default:
        // OutroCaso
        break;
}
```

Alfa/`String`: preferir `if/else` com `.equals()` (ou `switch` em Java 17+ com cuidado). **Não** copiar fall-through do `switch` sem `break` a menos que o LSP caia propositalmente no próximo `Caso`.

### VaPara — 3 padrões (`padrao_compilacao`)

**1. Early return**
```lsp
Se (condicao) { VaPara FimRegra; }
@ lógica
FimRegra:
```
```java
if (condicao) return;
// lógica
```

**2. Flag + do-while false** (bloco “pulado” com label)
```java
boolean fezProrrogacao = false;
do {
    // bloco principal
    fezProrrogacao = true;
} while (false);
if (!fezProrrogacao) { /* bloco do label */ }
```

**3. Break de loop**
```java
while (condicao) {
    if (encerrar) break;
}
```

### Para (0-based em Java)
```java
for (int i = 0; i < n; i++) { /* LSP Para costuma 1..n */ }
```

## Instruções

```text
1. Seguir “Como consultar” (A→H)
2. Identificar contexto
3. Buscar item só na família do Catálogo
4. Assinatura/contexto duvidosos → Índice das Funções (Skill 2)
5. Ausente → validacao_manual
```

## Tipos de regra e esqueletos (`padrao_compilacao`)

| Tipo LSP | Classe base | Contexto | Exceção |
|---|---|---|---|
| Apuração | `custom.senior.apuracao.Apuracao` | `getContextoApuracao()` | `RegraApuracaoException` |
| Consistência | `custom.senior.apuracao.ConsistenciaAcertos` | `getContextoConsistenciaAcerto()` | `RegraConsistenciaAcertoException` |
| Manutenção BH | `custom.senior.bancohoras.RegraManutencaoBH` | `getContextoManutencaoBH()` | `RegraBancoHorasException` |
| Fechamento BH | `custom.senior.bancohoras.RegraFechamentoBH` | `getContextoFechamentoBH()` | `RegraBancoHorasException` |

Package: o informado pelo usuário/projeto. Exemplo sanitizado: `gestaopontoCustom` (não `gestaoDoPontoCustom`).

### Apuração

```java
@Rule(description = "Regra de Apuracao")
public class RegraApuracao extends Apuracao {
    @Override
    public void execute() { // SEM throws Exception
        ContextoGeralRH ctxGeral = getContainer().getContextoGeral();
        ContextoApuracao ctx = getContainer().getContextoApuracao();
    }

    private void auxiliar(ContextoApuracao ctx, int param) { /* nível da classe */ }
}
```

### Consistência de Acertos

```java
@Rule(description = "Consistencia de Acertos")
public class RegraConsistencia extends ConsistenciaAcertos {
    @Override
    public void execute() {
        ContextoConsistenciaAcerto ctx = getContainer().getContextoConsistenciaAcerto();
        // extras: getHorSitAnterior, getDataInicial/Final, getHorSitAnteriorFaixa
    }
}
```

### Fechamento BH

```java
@Rule(description = "Fechamento BH")
public class RegraFechamentoBH extends custom.senior.bancohoras.RegraFechamentoBH {
    @Override
    public void execute() {
        ContextoFechamentoBH ctx = getContainer().getContextoFechamentoBH();
    }
}
```

Imports frequentes (`padrao_compilacao`): `java.time.LocalDate`/`LocalDateTime`, `com.senior.rule.Rule`, `com.senior.dataset.ICursor`, `MappedParamProvider`, `Colaborador`, `MarcacaoRegra`, `TipoIntervalo`, `TipoHoraExtra`, `ContextSession`, `DBCenter`, `IResultSet`, `com.senior.dataset.IEntity` (+ `@Entity`/`@Field`), readonly `IR030EMP`/`IR060DSI`/…

---


## Armadilhas práticas

| Armadilha / erro Eclipse | Correção |
|---|---|
| Só trocar sintaxe sem mapear variáveis | Inventário + getters/setters primeiro |
| Copiar ordem de parâmetros LSP | Confirmar no Índice das Funções |
| `getSituacao().get/setMinutos` | `getHorSit` / `setHorSit` / `zeraHorasSituacao` |
| Cursor SQL por reflexo | Buscar família no catálogo; USU_* → ICursor |
| `getHorSit(variavelDeMinutos)` | 1º arg = **código da situação** |
| Inventar `getApuDiu(1)` | `getHoras` / `getHorasSeparadas` |
| `execute() throws Exception` | Remover throws (`IRulePoint`) |
| Método aninhado / código solto | Auxiliares no nível da classe |
| `col.getTipCon()` | SQL `R034FUN.TIPCON` |
| `MarcacaoAnterior.getHora/getData` | `diferencaMinutos` |
| `LocalDateTime` → `LocalDate` | `.toLocalDate()` em `MarcacaoRegra.getData()` |
| `.sc` em tabela `R*` | Remover `.sc`; ContextSession |
| `.sc` não-JSON / BOM | Reescrever começando com `{` |
| `import com.senior.g5…IEntity` | `com.senior.dataset.IEntity` |
| Package `gestaoDoPontoCustom` | Package do projeto (ex. `gestaopontoCustom`) |
| `IResultSet` base-1 | base-0 |
| Filename ≠ classe pública | Renomear arquivo (Windows: temp rename) |
| Inventar método | `validacao_manual` |
| Misturar `java.time` e Joda | Preferir `java.time` / SDK |

### Mensagens Eclipse literais (referência)

| Mensagem | Correção |
|---|---|
| `The import com.senior.g5 cannot be resolved` | `import com.senior.dataset.IEntity` |
| `execute() throws Exception not declared by IRulePoint` | Remover `throws Exception` |
| `The method getTipCon() is undefined for the type Colaborador` | SQL `R034FUN.TIPCON` |
| `The method getHora() is undefined for the type MarcacaoAnterior` | `diferencaMinutos` |
| `Type mismatch: cannot convert LocalDateTime to LocalDate` | `.toLocalDate()` |
| `Expected BEGIN_OBJECT but was STRING` | `.sc` JSON puro começando com `{` |
| `Tabela Rxxx inválida. É permitido mapear somente tabelas de usuário` | Sem `.sc` em `R*` |
| `The public type X must be defined in its own file` | Filename = nome da classe |

**Windows (case):** Refactor → nome temporário → nome correto (ou `ren` em duas etapas no CMD).


## Saída para a Skill 1

```text
contexto: Apuracao | FechamentoBH | outro | indefinido
item_lsp: ...
equivalente_java: ...
evidencia: confirmada | padrao_compilacao | padrao_anexo | validacao_manual
fonte: equivalencia-funcoes-regras | indice-funcoes | compilacao | anexo
limite: ...
```

## Relacionados

Skill 2 (URLs/aliases) · Skill 1 · Skill 5 · referências `skill-03-referencia-catalogo.md` · `skill-03-referencia-acesso-dados.md` · `skill-03-referencia-exemplos-goldens.md`
