---
name: base-conversao-lsp-java
description: >-
  Padrões e catálogo oficial de equivalência LSP→Java (HCM 6.10.4 / Gestão do
  Ponto): variáveis, funções, âncoras, armadilhas e exemplos. Use a partir da
  Skill 1 após Skill 2. Fonte prioritária: documentação Senior de equivalência
  das funções de regras. Nunca invente método ausente neste catálogo e na Skill 2.
---

# Skill 3 · Base de Conversão LSP → Java
Versão: v1.2 · Interna · `skill-03-base-conversao-lsp-java.md`

Skill interna — **não** é fluxo de usuário. Aplique as regras globais do Router. Em conflito de assinatura, **revalide na Skill 2 / página oficial**.

**Fronteira:** Skill 2 = links/aliases; **esta skill** = mecânica + catálogo + exemplos de conversão.  
**Crescimento do catálogo:** só incluir equivalência **confirmada** (doc oficial / Skill 2). Proibido expandir por inferência.

## Como consultar (ordem obrigatória)

```text
A. Restrições + Regra de ouro + Invariantes   ← nunca pular
B. Workflow (6 passos)
C. Tipos / sintaxe (se necessário)
D. Catálogo — só a família do item LSP
E. Armadilhas (checklist rápido)
F. Exemplos — só o padrão análogo
G. Saída tipada para a Skill 1
```

Não leia o catálogo inteiro de ponta a ponta em toda conversão. Localize a **família** no índice abaixo.

## Índice rápido do arquivo

| Precisa de… | Vá para |
|---|---|
| Proibições / minutos / Sem Situacao.getMinutos | Restrições absolutas |
| Modelo mental LSP→contexto | Regra de ouro |
| Passo a passo | Workflow |
| Tipagem / Se→if / Vapara | Tipos e sintaxe |
| Esqueleto Apuracao / FechamentoBH | Esqueletos |
| `DatPro`, `HorSit`, `FPxMar`, históricos… | Catálogo → família |
| Erros comuns | Armadilhas |
| Par LSP/Java pronto | Exemplos sanitizados |

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
2. Horas em APIs de ponto = **minutos inteiros**.  
3. SQL/cursor → API semântica do catálogo antes de EntitySession.  
4. **Proibido** `getSituacao(...).getMinutos()` / `setMinutos(...)` — use `getHorSit` / `setHorSit` / `zeraHorasSituacao`.  
5. Sanitize nomes de cliente em exemplos anexados.  
6. Sem `Mensagem()`/popup em apuração — preferir `mensagemLog`.  
7. Confirmar se o método existe no **contexto** da regra (apuração ≠ geral ≠ BH).

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
| lógico `0`/`1` | `boolean` |
| `Data` | `LocalDate` (ou padrão do SDK — não misturar Joda + `java.time` sem necessidade) |
| `Hora` (minutos) | `int` minutos |
| marcação | `Marcacao` |
| `Se` / `Senao` / `Enquanto` / `Inicio`/`Fim` | `if` / `else` / `while` / `{ }` |
| `Vapara` / labels | `while`/`for` + `break`/`continue` |
| `@ ... @` | `//` |
| `=` comparação | `==` / `.isEqual()` / `.equals()` |
| `<>` | `!=` |

## Instruções

```text
1. Seguir “Como consultar” (A→G)
2. Identificar contexto
3. Buscar item só na família do Catálogo
4. Assinatura/contexto duvidosos → Índice das Funções (Skill 2)
5. Ausente → validacao_manual
```

## Esqueletos de classe

### Apuração

```java
@Rule(description = "Regra de Apuracao")
public class RegraApuracao extends Apuracao {
    @Override
    public void execute() {
        ContextoGeralRH contextoGeral = getContainer().getContextoGeral();
        ContextoApuracao contextoApuracao = getContainer().getContextoApuracao();
    }
}
```

### Fechamento BH

```java
@Rule(description = "Regra de Fechamento de Banco de Horas")
public class RegraFechamentoBH extends FechamentoBH {
    @Override
    public void execute() {
        ContextoGeralRH contextoGeral = getContainer().getContextoGeral();
        ContextoFechamentoBH contextoFechamentoBH = getContainer().getContextoFechamentoBH();
    }
}
```

---

## Catálogo de equivalência (oficial Senior 6.10.4)

Fonte: [Equivalência das funções de regras](https://documentacao.senior.com.br/gestao-de-pessoas-hcm/6.10.4/informacoes-adicionais/rotinas/gpo/integracao-controle-ponto-refeitorio/equivalencia-funcoes-regras.htm).  
Métodos tipicamente em `contextoApuracao` / container — **confirmar contexto e assinatura** no Índice das Funções.

### Famílias (âncora de busca)

| Família | Itens típicos LSP |
|---|---|
| Data / sistema | `DatPro`, `HorSis`, `DiaSem`, `DatIni`… |
| Situações | `HorSit[]`, `SitAnt[]`, `TotSit[]`, `MotSit` |
| Horas apuradas/previstas | `ApuDiu[]`, `ApuNot[]`, `TraDiu`, `PrvTra[]`… |
| Marcações | `FPxMar`, `FLeMar`, `DatMar`, `QtdMar`… |
| Escala / horário / feriado | `EscAtu`, `CodHor`, `FerFil`… |
| Históricos / usuário | `CarEmp`, `CodSinEmp`, `CodUsu`… |
| Compensação / BH / log | `TemCmp[]`, `RetBHRDat`, `MensagemLog`… |

### Data / sistema

| LSP (Controle de Ponto) | Java (Gestão do Ponto) |
|---|---|
| `DatPro` (implícito via Ano/Dia/MesPro) | `getData()` |
| `AnoPro` | `getAnoData(Date data)` / `getData()` |
| `MesPro` | `getMesData(Date data)` |
| `DiaPro` | `getDiaData(Date data)` |
| `AnoSis` / `MesSis` / `DiaSis` | `getAnoData` / `getMesData` / `getDiaData` |
| `HorSis` / `ExtSis` | Nativo em Java |
| `DatIni` / `Datfim` | `getDataInicial()` / `getDataFinal()` |
| `DiaSem`, `DiaDom`…`DiaSab` | `getDiaSem(Date data)` |
| `MesAtu` | `getMesData(Date data)` |
| `RetornaAnoData` / `RetornaDiaData` / `RetornaMesData` | `getAnoData` / `getDiaData` / `getMesData` |

### Situações / HorSit

| LSP | Java |
|---|---|
| `HorSit[]` | `getHorSit(int codSit)` / `getHorSit(LocalDate data, int codSit)`, `setHorSit(int codSit, int horas)`, `somaHorasSituacao(...)`, `zeraHorasSituacao(...)`, `zeraHorasSituacaoFaixa(...)`, `getHorSitFaixa(...)`, `getHorSitAnterior(int... codSit)` |
| `SitAnt[]` | `getHorSitAnterior(int codSit)` |
| `TotSit[]` / `BuscaTotalizadoresSituacoes` | `getTotalSituacoes(int codigoTotalizador, date data)` (e overload com intervalo) |
| `MotSit` | `getMotivoAcerto(int situacao)` |

### Apuração diurna/noturna / trabalhadas / previstas

| LSP | Java |
|---|---|
| `ApuDiu[]` / `ApuNot[]` | `getHorasSeparadas(...)` / `getHoras(Marcacao, Marcacao, ...)` |
| `HrtRaD[]` / `HrtRan[]` / `TraDiu` / `TraNot` | `getHorasTrabalhadas(int parte)` |
| `MinPvd[]` / `MinPvn[]` / `PrvTra[]` / `PrvTrd` / `PrvTrn` / `VprVho` / `VprVin` / `VprVtr` | `getTotalMinutosPrevisto(...)` / `getHorasPrevistas(...)` / `getTotalMinutosPrevistoProrrogado(...)` |
| `FatRed` | `getHorarioPrevistoColaborador(...)` |
| `ExtrasIntervalo` | `getExtrasIntervalo` / `getExtrasIntervaloAnterior` / `getExtrasIntervaloPosterior` |
| `MinExD[]` / `MinExn[]` / `MsaInd[]` / `MsaInn[]` / `IniExt` / `FimExt` / `PerExt` / `PriExt` / `QtdExt` / `TipExt` / `DiaExt` | `getIntervalosCalculados()` / `getIntervaloCalculado(int indice)` |

### Marcações

| LSP | Java |
|---|---|
| `FPxMar` / `FLeMar` / `ConGer` / `DatMar` / `HorMar` / `FncMar` / `OriMar` / `RlgMar` / `UsoMar` | `getMarcacoesRealizadas(boolean conger)` |
| `QtdMar` / `TotMar` | `getQtdMarcacoesRealizadas(boolean conger)` |
| `DulMar` / `HulMar` | `getMarcacaoAnterior()` |
| `MinJor` | `getHorasInterjornadaRealizada()` |
| `MinMJo` | `getHorasInterjornadaPrevista()` |

### Escala / horário / filial / feriado

| LSP | Java |
|---|---|
| `EscAtu` | `getEscala()` |
| `EscEmp` / `RetEscEmp` | `getHistoricoEscala()` |
| `EscTrf` | `getEscalaHistorico()` |
| `TemTes` | `getTrocaEscala(Date data)` |
| `TemThr` | `getTrocaHorario(Date data)` |
| `RetornaEscala` | `getEscalaPrevistaColaborador(...)` |
| `CodHor` / `RetornaHorarioApurado` | `getHorario()` |
| `HorEsc` / `HorTrf` | `getHorarioEscala()` |
| `HorDFe` | `getHorarioOriginalEscala()` |
| `HorFol` | `getCodigoHorarioFolga()` / `getHorarioFolga()` |
| `HorPfo` | `getHorarioProjecaoFolga()` |
| `RetornaHorario` / `RetornaBatidaHorario` | `getHorarioPrevistoColaborador(...)` |
| `NumPer` | `getNumeroPeriodos(int codHor)` |
| `NumInt` | `getNumeroIntervalos()` |
| `NinRef` | `getNumeroIntervaloRefeicao()` |
| `TurInt` | `getTurmaIntervalo()` |
| `RetMinRefHTr` | `getMinutosRefeicaoPrevisto()` |
| `FilEmp` / `RetFilEmp` / `DatAltFil` / `EmpAltFil` | `getHistoricoFilial()` |
| `FerFil` | `getFeriadoFilial(Date data)` |
| `VerDatFer` | `getFeriado(Date data)` |

### Históricos colaborador / usuário

| LSP | Java |
|---|---|
| `CarEmp` / `EstCarEmp` / `RetCarEmp` | `getHistoricoCargo()` |
| `CcuEmp` / `DatAltCcu` / `RetCcuEmp` | `getHistoricoCentrodeCusto()` |
| `CodSinEmp` / `RetSinEmp` | `getHistoricoSindicato()` |
| `CodVinEmp` / `RetVinEmp` | `getHistoricoVinculo()` |
| `LocEmp` / `RetLocEmp` | `getHistoricoLocal(...)` |
| `CodAfs` / `IniAfs` / `FimAfs` / `TemAfs` / `QtdAfs[]` | `getHistoricosAfastamento()` |
| `BusCraTit` | `getHistoricosCracha()` / `getHistoricosCrachaProvisorio()` |
| `RetApuPon` | `getHistoricoApuracao(colaborador, data)` |
| `CodUsu` | `getUsuarioAtivo()` |
| `NomUsu` | `getUsuario(long codigoUsuario)` |
| `RetornaDesGrupo` / `RetornaQtdGrupos` | `getGrupos(long codigoUsuario)` |
| `AssociaUsuColab` | `associarUsuarioColaborador(...)` |
| `RetColabPorCodUsu` | `getUsuarioColaborador(...)` |

### Compensação / banco de horas / cálculo

| LSP | Java |
|---|---|
| `TemCmp[]` / `DtICmp[]` / `DtFCmp[]` / `PerCmp[]` / `QtdCmp[]` / `SitCmD[]` / `SitCmN[]` / `TipCmp[]` | `getCompensacoes()` / `getCompensacoes(LocalDate data)` |
| `LimBa1` / `LimBa2` | `getEscala()` |
| `RetBHRDat` | `getSaldoBanco(int banco, int empresa, int tipo, int cadastro, LocalDate data)` |
| `TipCal` | `getTipoCalculo()` |
| `MensagemLog` | `mensagemLog(String mensagem)` |
| `VerificaAbrangenciaNumero` | `getAbrangencia(string abrangencia, int numero)` |
| `RetornaCodLoc` / `RetornaNumLoc` / `RetNivLoc` | `getCodigoLocal` / `getNumeroLocal` / `getQtdNiveisLocal` |

### Definição de situações (padrão complementar)

Cursor `R014SIN`/`R030EMP` para `CodDsi` → preferir API (`padrao_anexo` até confirmar na doc):

```java
int codDsi = contextoApuracao.getDefinicaoSituacoes().getCodigo();
```

---

## Armadilhas práticas

| Armadilha | Correção |
|---|---|
| Só trocar sintaxe sem mapear variáveis | Inventário + getters/setters primeiro |
| Copiar ordem de parâmetros LSP | Confirmar no Índice das Funções |
| `getSituacao().get/setMinutos` | `getHorSit` / `setHorSit` / `zeraHorasSituacao` |
| Cursor SQL por reflexo | Buscar família no catálogo |
| `getHorSit(variavelDeMinutos)` | 1º arg = **código da situação** |
| Inventar `getApuDiu(1)` | `getHoras` / `getHorasSeparadas` |
| Método de apuração em contexto geral | Confirmar contexto |
| Inventar método | `validacao_manual` |
| Misturar `java.time` e Joda | Seguir SDK / `validacao_manual` |

## Exemplos sanitizados (use só o análogo)

### HorSis + setHorSit

```lsp
Se (HorSis > 870) Inicio
  HorSit = 120;   @ situação 100 @
Fim;
```

```java
LocalTime agora = new LocalTime(); // ou padrão do projeto
int minutos = agora.getHourOfDay() * 60 + agora.getMinuteOfHour();
if (minutos > 870) {
    contextoApuracao.setHorSit(100, 120);
}
```

### HorSit — errado vs certo

```java
// ERRADO
contexto.getSituacao(xNorAnt).setMinutos(0);
// CERTO
contexto.zeraHorasSituacao(xNorAnt);
double v = contexto.getHorSit(xExDDsr);
contexto.setHorSit(xExDDsr, v + vNorDes);
```

### Marcações FLeMar/FPxMar → List

```java
for (Marcacao m : contextoApuracao.getMarcacoesRealizadas(false)) {
    if (m.getData().isAfter(contextoApuracao.getData())) { /* ... */ }
}
```

### End → retorno (`RetBHRDat`)

```java
// ordem Java ≠ LSP — confirmar no índice
int saldo = contextoApuracao.getSaldoBanco(codbhr, numemp, tipcol, numcad,
        new LocalDate(2014, 9, 24));
```

### Múltiplos End → objeto

```java
private ResultadoDiurnoNoturno calculaDiurnoNoturno(...) {
    return new ResultadoDiurnoNoturno(minutosDiurnos, minutosNoturnos);
}
```

### Troca de situação

```java
private int trocarSituacao(ContextoApuracao ctx, int origem, int destino, int minutosPendentes) {
    int minutosOrigem = ctx.getHorSit(origem);
    if (minutosOrigem >= minutosPendentes && minutosOrigem > 0 && minutosPendentes > 0) {
        ctx.setHorSit(destino, minutosPendentes);
        ctx.setHorSit(origem, minutosOrigem - minutosPendentes);
        return 0;
    }
    if (minutosOrigem < minutosPendentes && minutosOrigem > 0 && minutosPendentes > 0) {
        ctx.setHorSit(destino, minutosOrigem);
        ctx.setHorSit(origem, 0);
        return minutosPendentes - minutosOrigem;
    }
    return minutosPendentes;
}
```

### EntitySession (último recurso)

```java
ICursor<IEntidadeCustom> cursor = EntitySessionProvider.getSession()
        .newCursor(IEntidadeCustom.class);
try {
    cursor.addFilter("campoA = :campoA", new MappedParamProvider("campoA", valorA));
    cursor.open();
    if (cursor.next()) { /* read */ }
} finally {
    cursor.close();
}
```

Justificar ausência de API; marcar `validacao_manual` se entidade custom.

## Saída para a Skill 1

```text
contexto: Apuracao | FechamentoBH | outro | indefinido
item_lsp: ...
equivalente_java: ...
evidencia: confirmada | padrao_anexo | validacao_manual
fonte: equivalencia-funcoes-regras | indice-funcoes | anexo
limite: ...
```

## Relacionados

Skill 2 (URLs/aliases) · Skill 1 · Skill 5 (`CHK-SITAPI`, `CHK-ORDEM`, `CHK-FIN`, `CHK-CTXOK`)
