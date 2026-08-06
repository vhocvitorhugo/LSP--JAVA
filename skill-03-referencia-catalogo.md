---
name: base-conversao-catalogo
description: >-
  Catálogo oficial de equivalência LSP→Java (HCM 6.10.4), campos conflitantes e constantes de domínio. Use sob demanda a partir da Skill 3 quando mapear família de função, TipCon ou constantes.
---

# Skill 3 · Referência — Catálogo de equivalência
Versão: v1.11 · Referência da Skill 3 · Progressive disclosure

Skill interna — carregar **somente** quando o núcleo (`skill-03-base-conversao-lsp-java.md`) indicar esta âncora. Aplique as regras globais do Router.

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
| `DiaSem`, `DiaDom`…`DiaSab` | Preferir `getDiaSem(Date)`; alt. `getData().getDayOfWeek().getValue()` (`padrao_compilacao`) |
| `MesAtu` | `getMesData(Date data)` |
| `RetornaAnoData` / `RetornaDiaData` / `RetornaMesData` | `getAnoData` / `getDiaData` / `getMesData` |

### Situações / HorSit

| LSP | Java |
|---|---|
| `HorSit[]` | `getHorSit(int)` / `getHorSit(LocalDate, int)`, `setHorSit`, `somaHorasSituacao`, `zeraHorasSituacao`, `zeraHorasSituacaoFaixa`, `getHorSitFaixa` — overloads `padrao_compilacao`: `getHorSit(int[])`, `zeraHorasSituacao(varargs)` |
| `SitAnt[]` | `getHorSitAnterior(int)` / `getHorSitAnteriorFaixa` (consistência) |
| `TotSit[]` / `BuscaTotalizadoresSituacoes` | `getTotalSituacoes(int codigoTotalizador, date data)` (e overload com intervalo) |
| `MotSit` | `getMotivoAcerto(int situacao)` |

### Apuração diurna/noturna / trabalhadas / previstas

| LSP | Java |
|---|---|
| `ApuDiu[]` / `ApuNot[]` | `getHorasSeparadas(TipoIntervalo\|TipoHoraExtra)` → `ISeparacaoHoras` (`getHorasDiurnas`/`Noturnas`/`TotalHoras`); ou `getHoras(MarcacaoRegra, …)` |
| `HrtRaD[]` / `HrtRan[]` / `TraDiu` / `TraNot` | `getHorasTrabalhadas(int parte)` |
| `MinPvd[]` / `MinPvn[]` / `PrvTra[]` / `PrvTrd` / `PrvTrn` / `VprVho` / `VprVin` / `VprVtr` | `getTotalMinutosPrevisto(...)` / `getHorasPrevistas(...)` / `getTotalMinutosPrevistoProrrogado(...)` |
| `FatRed` | `getHorarioPrevistoColaborador(...)` |
| `ExtrasIntervalo` | `getExtrasIntervalo` / `getExtrasIntervaloAnterior` / `getExtrasIntervaloPosterior` |
| `MinExD[]` / `MinExn[]` / `MsaInd[]` / `MsaInn[]` / `IniExt` / `FimExt` / `PerExt` / `PriExt` / `QtdExt` / `TipExt` / `DiaExt` | `getIntervalosCalculados()` / `getIntervaloCalculado(int indice)` |

### Marcações

| LSP | Java |
|---|---|
| `FPxMar` / `FLeMar` / … | `List<MarcacaoRegra> getMarcacoesRealizadas(boolean)` — `getData()` → **`.toLocalDate()`**; índice Java **0-based** |
| `QtdMar` / `TotMar` | Preferir `getQtdMarcacoesRealizadas(boolean)`; alt. `.size()` (`padrao_compilacao`) |
| `DulMar` / `HulMar` | `getMarcacaoAnterior()` → tipo `MarcacaoAnterior`: **só** `diferencaMinutos(data, hora)` — sem `getHora`/`getData` |
| `MinJor` | Preferir `getHorasInterjornadaRealizada()`; alt. `diferencaMinutos` se só MarcacaoAnterior |
| `MinMJo` | `getHorasInterjornadaPrevista()` |
| `TipCon` | **Não** existe `Colaborador.getTipCon()` — SQL `SELECT TIPCON FROM R034FUN …` via ContextSession (`padrao_compilacao`) |
| `ApuDiu`/`ApuNot` tipados | Também `getHorasSeparadas(TipoIntervalo\|TipoHoraExtra)` → `ISeparacaoHoras` |
| log / pendência / alerta | `mensagemLog`, `setGerarPendencia`, `criarAlerta` (try/catch) |

### Escala / horário / filial / feriado

| LSP | Java |
|---|---|
| `EscAtu` | `getEscala()` |
| `EscEmp` / `RetEscEmp` | `getHistoricoEscala()` |
| `EscTrf` | `getEscalaHistorico()` |
| `TemTes` | `getTrocaEscala(Date data)` |
| `TemThr` | `getTrocaHorario(Date data)` |
| `RetornaEscala` | `getEscalaPrevistaColaborador(...)` |
| `CodHor` / `RetornaHorarioApurado` | `getHorario()` / `getHorario().getCodigo()` — especiais 9996–9999 (folga/feriado/comp/DSR) |
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

## Campos LSP conflitantes (`padrao_compilacao`)

| LSP | Erro comum | Correto |
|---|---|---|
| `TipCon` | `col.getTipCon()` | SQL `R034FUN.TIPCON` |
| `nMar` / marcações | índice 1-based / tipo errado | `List<MarcacaoRegra>` 0-based + `.toLocalDate()` |
| `MarcacaoAnterior` | `getHora()` / `getData()` | só `diferencaMinutos` |
| `HorSit[n]` | tratar como array Java | `get/setHorSit(codSit, minutos)` |
| `SitAnt` | getter inventado | `getHorSitAnterior` no contexto de consistência |
| `QtdMar` | inventar campo | API oficial ou `.size()` |

## Domínio HCM — constantes úteis

| Valor | Uso |
|---|---|
| CodHor `9996`–`9999` | Folga / feriado / compensado / DSR (`<9996` = horário normal) |
| `1320` / `300` | Janela noturna 22h–05h (minutos) |
| `660` / `360` | Limites CLT interjornada / sem intervalo |
| `1440` | Virada de dia em `CalculaQtdMinutos` |



## Relacionados

Núcleo Skill 3 · Skill 1 · Skill 2 · Skill 5
