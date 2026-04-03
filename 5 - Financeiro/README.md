# 📊 Análise Financeira (Power BI)

## 🎯 Objetivo

Este projeto tem como objetivo desenvolver um dashboard financeiro no Power BI, permitindo a análise de receitas, despesas e lucratividade, com foco na geração de insights estratégicos para tomada de decisão.

---

## 📌 Contexto do Projeto

Neste mini-projeto, foram exploradas funcionalidades do Power BI aplicadas ao contexto financeiro.

A empresa deseja obter uma visão clara sobre seu desempenho financeiro, analisando receitas e despesas de forma estruturada, com o objetivo de identificar oportunidades e definir estratégias.

---

## 📊 Indicadores de Negócio

O dashboard foi desenvolvido para responder às seguintes métricas:

* 💰 **Total de Receitas**
* 💸 **Total de Despesas**
* 📈 **Margem de Lucro**
* 📊 **Receitas por Componente**
* 📉 **Despesas por Componente (comparadas à média)**
* 📅 **Receitas e Despesas por Ano e Componente (hierarquia Tipo/Componente)**

Além disso, o projeto permite identificar:

* Segmentos com **maiores receitas e despesas**
* Segmentos com **menores receitas e despesas**

---

## 🧠 Medidas DAX e Aplicações

### 💵 Valor Total

```dax id="fin1"
Volor Total = SUM(DadosFinanceiros[Valor])
```

📌 **Uso no negócio:**
Representa o valor consolidado das transações financeiras, servindo como base para todos os cálculos do projeto.

---

### 💰 Valor de Receitas

```dax id="fin2"
Valor Receitas = 
CALCULATE(
    Medidas[Volor Total],
    DadosFinanceiros[Tipo] = "Receitas"
)
```

📌 **Uso no negócio:**
Permite analisar exclusivamente as entradas financeiras da empresa.

---

### 💸 Valor de Despesas

```dax id="fin3"
Valor Despesas = 
CALCULATE(
    Medidas[Volor Total],
    DadosFinanceiros[Tipo] = "Despesas"
)
```

📌 **Uso no negócio:**
Permite avaliar os custos e saídas financeiras, fundamentais para controle e redução de gastos.

---

### 📈 Lucro

```dax id="fin4"
Lucro = [Valor Receitas] - [Valor Despesas]
```

📌 **Uso no negócio:**
Indicador principal de desempenho financeiro, mostrando o resultado líquido da empresa.

---

### 📊 Margem de Lucro

```dax id="fin5"
MargemLucro = DIVIDE([Lucro], [Valor Receitas], 0)
```

📌 **Uso no negócio:**
Mede a eficiência financeira da empresa, indicando quanto do faturamento se converte em lucro.

---

## 📈 Metodologia

Durante o desenvolvimento foram aplicadas as seguintes práticas:

* Modelagem de dados financeiros
* Criação de medidas DAX para KPIs
* Construção de dashboards interativos
* Uso de hierarquias (Tipo → Componente)
* Análise comparativa entre receitas e despesas

---

## 💡 Principais Insights (Exemplo)

* Identificação de componentes mais lucrativos
* Detecção de áreas com alto custo
* Análise da evolução financeira ao longo do tempo
* Avaliação da eficiência operacional através da margem de lucro

---

## 🛠️ Ferramentas Utilizadas

* Power BI
* DAX
* Modelagem de Dados

---

## 🚀 Aprendizados

* Construção de indicadores financeiros
* Uso de DAX para análise de negócio
* Interpretação de dados financeiros
* Criação de dashboards estratégicos

---

✍️ Projeto desenvolvido para fins de estudo e aprimoramento em análise de dados.
