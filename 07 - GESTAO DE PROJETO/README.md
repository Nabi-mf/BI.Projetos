# 📊 Power BI — Gestão de Projetos

> Dashboard de acompanhamento financeiro e operacional de projetos, com controle de orçamento, custos realizados e variações por período, equipe e gerente.

---

## 📁 Estrutura do Projeto

```
PBIX_3_-_Gestão_de_Projetos.pbix
│
├── dProjeto.csv          ← Dimensão: cadastro dos projetos
├── fCustos.csv           ← Fato: lançamentos de custos realizados
├── fOrcamento.csv        ← Fato: distribuição mensal do orçamento
└── dCalendario           ← Dimensão de datas (criada via DAX no Power BI)
```

---

## 🗂️ Fontes de Dados

### `dProjeto.csv` — Dimensão Projeto

Tabela de dimensão com o cadastro de todos os projetos. Contém **10 projetos** no total.

| Coluna | Tipo | Descrição |
|---|---|---|
| `Id_Projeto` | Texto | Chave primária (ex: `PROJ-001`) |
| `Descrição` | Texto | Nome do projeto |
| `Orçamento` | Numérico | Orçamento total aprovado (R$) |
| `Data Aprovação` | Data | Data de início/aprovação do projeto |
| `Data Conclusão` | Data | Data prevista de conclusão |
| `Data Última Atualização` | Data | Última atualização do status |
| `Status` | Texto | `Finalizado` ou `Em andamento` |
| `Gerente Projeto` | Texto | Responsável pelo projeto |
| `Equipe` | Texto | Equipe alocada (Alpha, Beta, Gamma...) |

**Projetos cadastrados:**

| Id | Projeto | Orçamento Total | Status | Gerente |
|---|---|---|---|---|
| PROJ-001 | Expansão de Armazém | R$ 2.218.845,87 | Finalizado | Carlos Silva |
| PROJ-002 | Modernização de Frota | R$ 3.780.184,81 | Em andamento | Ana Pereira |
| PROJ-003 | Automação de Processos | R$ 1.733.425,96 | Finalizado | Roberto Souza |
| PROJ-004 | Implementação de ERP | R$ 1.191.832,27 | Em andamento | Mariana Lima |
| PROJ-005 | Otimização de Rotas | R$ 319.025,82 | Finalizado | João Fernandes |
| PROJ-006 | Construção de Centro de Distribuição | R$ 4.157.179,21 | Finalizado | Renata Alves |
| PROJ-007 | Upgrade de Sistemas | R$ 2.978.826,91 | Finalizado | Fernando Costa |
| PROJ-008 | Treinamento de Equipe | R$ 2.593.783,56 | Em andamento | Patrícia Ribeiro |
| PROJ-009 | Instalação de Equipamentos | R$ 753.337,90 | Finalizado | José Santos |
| PROJ-010 | Melhoria de Infraestrutura | R$ 1.840.651,99 | Em andamento | Luciana Martins |

**Orçamento total consolidado: R$ 21.567.088,30**

---

### `fCustos.csv` — Fato Custos Realizados

Tabela de fatos com os lançamentos de **600 registros** de custos reais incorridos nos projetos, cobrindo o período de **janeiro/2020 a dezembro/2024**.

| Coluna | Tipo | Descrição |
|---|---|---|
| `Data` | Data | Data do lançamento do custo |
| `Valor` | Numérico | Valor do custo (R$) |
| `Descricao do Item` | Texto | Descrição do item adquirido/contratado |
| `Id_Projeto` | Texto | Chave estrangeira → `dProjeto` |
| `Classificação` | Texto | `Serviço` ou `Material` |
| `Fornecedor` | Texto | Nome do fornecedor |

**Resumo:**
- **Total realizado:** R$ 13.091.138,93
- **Período:** Jan/2020 a Dez/2024
- **Fornecedores únicos:** 20
- **Classificações:** Serviço e Material
- **Exemplos de itens:** Serviços de Terceirização, Compra de Equipamentos, Treinamento de Funcionários, Compra de Materiais de Construção

**Custos realizados por projeto (top ranking):**

| Projeto | Custo Realizado |
|---|---|
| PROJ-007 | R$ 1.381.600,71 |
| PROJ-002 | R$ 1.379.355,71 |
| PROJ-006 | R$ 1.372.142,26 |
| PROJ-005 | R$ 1.315.973,69 |
| PROJ-004 | R$ 1.305.164,46 |
| PROJ-010 | R$ 1.284.762,81 |
| PROJ-003 | R$ 1.273.009,13 |
| PROJ-001 | R$ 1.267.348,78 |
| PROJ-008 | R$ 1.256.064,13 |
| PROJ-009 | R$ 1.255.717,25 |

---

### `fOrcamento.csv` — Fato Orçamento Distribuído

Tabela de fatos com **600 registros** representando a distribuição mensal do orçamento por projeto, cobrindo o período de **janeiro/2022 a dezembro/2023**.

| Coluna | Tipo | Descrição |
|---|---|---|
| `Id_Projeto` | Texto | Chave estrangeira → `dProjeto` |
| `Descrição` | Texto | Rótulo do lançamento (ex: "Despesa de Expansão de Armazém no mês 1/2020") |
| `Data` | Data | Mês de referência da parcela orçada |
| `Valor` | Numérico | Valor orçado para o período (R$) |

> 💡 O orçamento está distribuído mensalmente, o que permite análises de **planejado vs. realizado** no mesmo eixo de tempo.

---

## 📅 dCalendario — Tabela de Datas (DAX)

### Por que foi criada?

Em qualquer modelo analítico no Power BI, é uma **boa prática obrigatória** ter uma tabela de datas desconectada e centralizada. Sem ela:

- Filtros de ano/mês/trimestre não funcionam corretamente entre tabelas de fatos diferentes.
- A inteligência de tempo do DAX (`TOTALYTD`, `SAMEPERIODLASTYEAR`, `DATEADD` etc.) não opera de forma confiável.
- Slicers de período não cruzam as duas tabelas de fato ao mesmo tempo.

### Como foi criada

A `dCalendario` foi gerada via DAX com a função `CALENDAR()` ou `CALENDARAUTO()`, cobrindo todo o intervalo de datas presente nos dados (2020–2024), e enriquecida com colunas calculadas como:

```dax
dCalendario = 
ADDCOLUMNS(
    CALENDAR(DATE(2020,1,1), DATE(2024,12,31)),
    "Ano",           YEAR([Date]),
    "Mês Número",    MONTH([Date]),
    "Mês Nome",      FORMAT([Date], "MMMM", "pt-BR"),
    "Trimestre",     "T" & FORMAT([Date], "Q"),
    "Ano-Mês",       FORMAT([Date], "YYYY-MM"),
    "Semana",        WEEKNUM([Date]),
    "Dia Semana",    FORMAT([Date], "dddd", "pt-BR")
)
```

### Por que isso importa para o modelo

Com a `dCalendario` como eixo central de tempo, o modelo consegue:

- Cruzar `fCustos` e `fOrcamento` **no mesmo período** sem ambiguidade.
- Permitir que slicers de Ano e Mês filtrem ambas as tabelas de fato simultaneamente.
- Habilitar cálculos de variação acumulada (YTD), comparação com períodos anteriores e projeções.

---

## 🔗 Relacionamentos do Modelo (Star Schema)

O modelo segue o padrão **Star Schema**, com a `dProjeto` e `dCalendario` como dimensões centrais e as duas tabelas de fatos na periferia.

```
                    ┌─────────────────┐
                    │   dCalendario   │
                    │  (Data [PK])    │
                    └────────┬────────┘
                             │ 1:N (ativo)
              ┌──────────────┼──────────────┐
              │                             │
     ┌────────▼────────┐         ┌──────────▼──────────┐
     │    fCustos      │         │     fOrcamento       │
     │  Data (FK)      │         │   Data (FK)          │
     │  Id_Projeto (FK)│         │   Id_Projeto (FK)    │
     └────────┬────────┘         └──────────┬──────────┘
              │                             │
              └──────────────┬──────────────┘
                             │ N:1 (ativo)
                    ┌────────▼────────┐
                    │    dProjeto     │
                    │  Id_Projeto[PK] │
                    └─────────────────┘
```

| De | Para | Cardinalidade | Direção do Filtro |
|---|---|---|---|
| `fCustos[Id_Projeto]` | `dProjeto[Id_Projeto]` | Muitos para Um | Único (→) |
| `fOrcamento[Id_Projeto]` | `dProjeto[Id_Projeto]` | Muitos para Um | Único (→) |
| `fCustos[Data]` | `dCalendario[Date]` | Muitos para Um | Único (→) |
| `fOrcamento[Data]` | `dCalendario[Date]` | Muitos para Um | Único (→) |

---

## 📐 Métricas e Análises Habilitadas

Com esse modelo, é possível construir as seguintes análises:

**Financeiras:**
- Orçamento Total por Projeto
- Custo Realizado por Projeto
- Variação (Orçado vs. Realizado) em valor e percentual
- Saldo disponível por projeto

**Temporais:**
- Evolução mensal de custos e orçamento
- Acumulado no ano (YTD)
- Comparativo entre anos/períodos

**Operacionais:**
- Distribuição de custos por Classificação (Serviço vs. Material)
- Ranking de fornecedores por valor
- Performance por Gerente de Projeto
- Performance por Equipe

**Status:**
- Projetos finalizados vs. em andamento
- Projetos dentro e acima do orçamento

---

## 🛠️ Tecnologias

- **Power BI Desktop** — modelagem, DAX e visualizações
- **CSV** — fonte de dados primária
- **DAX** — cálculos e tabela de calendário
- **Star Schema** — padrão de modelagem dimensional

---

## 📌 Observações

- O período de `fCustos` (2020–2024) é mais amplo que o de `fOrcamento` (2022–2023), o que significa que há meses com custo realizado mas sem orçamento distribuído — esses casos devem ser tratados nas métricas com `COALESCE` ou verificação de `BLANK()`.
- Os projetos com Status `Em andamento` ainda estão acumulando custos, o que torna o comparativo orçado/realizado dinâmico.
- A `dCalendario` deve ser marcada como **Tabela de Datas** nas configurações do Power BI para que a inteligência de tempo funcione corretamente.
