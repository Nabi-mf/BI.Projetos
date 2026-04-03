# 📊 Balanço Patrimonial (Power BI)

## 🎯 Objetivo

Este projeto tem como objetivo demonstrar, na prática, a construção de um **Balanço Patrimonial no Power BI**, utilizando o visual de **Matriz** para organização contábil dos dados e criação de indicadores financeiros estratégicos.

---

## 📌 Sobre o Projeto

Neste laboratório, é apresentada uma abordagem passo a passo para representar dados contábeis no Power BI, explorando funcionalidades importantes da ferramenta, com foco na visualização estruturada de informações financeiras.

O principal destaque do projeto é a construção de uma **matriz hierárquica**, permitindo a leitura do balanço patrimonial de forma semelhante aos modelos utilizados em empresas.

---

## 📊 Problemas de Negócio

O dashboard foi desenvolvido para responder às seguintes perguntas:

* 💰 Qual o **total de ativos da empresa**?
* 💸 Qual o **total de passivos**?
* 📈 Qual o **valor do patrimônio líquido**?
* 📊 Como os valores estão distribuídos entre **circulante e não circulante**?

---

## 🧩 Estrutura do Dashboard

### 📋 Matriz do Balanço Patrimonial

* Organização hierárquica das contas contábeis
* Estrutura baseada em níveis:

  * Conta Nível 1 (Ativo / Passivo)
  * Conta Nível 2 (Circulante / Não Circulante / Patrimônio Líquido)
* Visualização por múltiplos anos

📌 **Objetivo:**
Permitir uma leitura clara e estruturada do balanço patrimonial diretamente no Power BI.

---

### 📊 Indicadores (Cards)

Foram criados três KPIs principais para análise rápida:

* 💰 **Total Circulante**
* 💸 **Total Não Circulante**
* 📈 **Total Patrimônio Líquido**

📌 Esses indicadores são fundamentais para avaliar a saúde financeira da empresa e representam uma das principais análises de negócio do projeto.

---

## 🧠 Medidas DAX e Aplicações

### 💰 Total Ativo

```dax id="bal1"
Total Ativo = 
CALCULATE(
    SUM(DadosContabeis[Ano_2019]) +
    SUM(DadosContabeis[Ano_2020]) +
    SUM(DadosContabeis[Ano_2021]) +
    SUM(DadosContabeis[Ano_2022]) +
    SUM(DadosContabeis[Ano_2023]),
    PlanoContas[Conta Nível 1] = "Ativo"
)
```

📌 **Uso no negócio:**
Representa todos os bens e direitos da empresa, sendo essencial para análise patrimonial.

---

### 💵 Total Circulante

```dax id="bal2"
Total Circulante = 
CALCULATE(
    SUM(DadosContabeis[Ano_2019]) +
    SUM(DadosContabeis[Ano_2020]) +
    SUM(DadosContabeis[Ano_2021]) +
    SUM(DadosContabeis[Ano_2022]) +
    SUM(DadosContabeis[Ano_2023]),
    PlanoContas[Conta Nível 2] = "Circulante"
)
```

📌 **Uso no negócio:**
Mostra os recursos de curto prazo, fundamentais para avaliar liquidez da empresa.

---

### 💸 Total Não Circulante

```dax id="bal3"
Total Não Circulante = 
CALCULATE(
    SUM(DadosContabeis[Ano_2019]) +
    SUM(DadosContabeis[Ano_2020]) +
    SUM(DadosContabeis[Ano_2021]) +
    SUM(DadosContabeis[Ano_2022]) +
    SUM(DadosContabeis[Ano_2023]),
    PlanoContas[Conta Nível 2] = "Não Circulante"
)
```

📌 **Uso no negócio:**
Representa ativos e obrigações de longo prazo, importantes para análise estratégica.

---

### 💰 Total Passivo

```dax id="bal4"
Total Passivo = 
CALCULATE(
    SUM(DadosContabeis[Ano_2019]) +
    SUM(DadosContabeis[Ano_2020]) +
    SUM(DadosContabeis[Ano_2021]) +
    SUM(DadosContabeis[Ano_2022]) +
    SUM(DadosContabeis[Ano_2023]),
    PlanoContas[Conta Nível 1] = "Passivo"
)
```

📌 **Uso no negócio:**
Representa todas as obrigações da empresa.

---

### 📈 Total Patrimônio Líquido

```dax id="bal5"
Total Patrimonio Liquido = 
CALCULATE(
    SUM(DadosContabeis[Ano_2019]) +
    SUM(DadosContabeis[Ano_2020]) +
    SUM(DadosContabeis[Ano_2021]) +
    SUM(DadosContabeis[Ano_2022]) +
    SUM(DadosContabeis[Ano_2023]),
    PlanoContas[Conta Nível 2] = "Patrimônio Líquido"
)
```

📌 **Uso no negócio:**
Indica o valor líquido da empresa, sendo um dos principais indicadores financeiros.

---

## 📈 Metodologia

* Modelagem de dados contábeis
* Uso de hierarquia de contas
* Construção de matriz no Power BI
* Criação de medidas DAX financeiras
* Desenvolvimento de KPIs

---

## 💡 Resultado Esperado

O projeto permite:

* Visualização estruturada do balanço patrimonial
* Análise de liquidez e estrutura financeira
* Compreensão clara entre ativos, passivos e patrimônio
* Apoio à tomada de decisão financeira

---

## 🛠️ Ferramentas Utilizadas

* Power BI
* DAX
* Modelagem de Dados

---

## 🚀 Aprendizados

* Construção de balanço patrimonial no Power BI
* Uso avançado de matriz e hierarquias
* Criação de indicadores financeiros
* Análise contábil aplicada a dados

---

✍️ Projeto desenvolvido para fins de estudo e aprimoramento em análise de dados financeiros.
