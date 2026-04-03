# 📊 Análise de Dados de RH (Power BI)

## 🎯 Objetivo

Este projeto tem como objetivo apresentar uma introdução à análise de dados de Recursos Humanos (RH) utilizando o Power BI, com foco na geração de insights estratégicos para gestão de pessoas.

## 📌 Sobre o Projeto

Durante o desenvolvimento, foram explorados dados fictícios de funcionários, permitindo simular cenários reais de uma empresa.

Além da construção de dashboards, o projeto também aborda recursos importantes do Power BI, como:

* Criação de tabela de medidas
* Colunas condicionais
* Modelagem de dados
* Construção de indicadores (KPIs)

---

📊 Problemas de Negócio

O dashboard foi desenvolvido para responder às seguintes perguntas:

👥 Total de funcionários
→ Quantidade atual de colaboradores na empresa
⏳ Tempo médio de experiência
→ Média de anos de experiência dos funcionários
🚻 Distribuição por gênero
→ Total e percentual de funcionários masculinos e femininos
💰 Média salarial mensal
→ Valor médio dos salários dos colaboradores
🧑‍💼 Funcionários por função
→ Quantidade de funcionários por cargo
⏱️ Disponibilidade para hora extra
→ Percentual de funcionários disponíveis para horas extras
📊 Nível de envolvimento no trabalho
→ Classificação dos funcionários em quatro categorias:
Ruim
Baixo
Médio
Alto

💡 Principais Insights (Exemplo)
Distribuição equilibrada (ou não) entre gêneros
Identificação de funções com maior concentração de colaboradores
Análise de engajamento dos funcionários
Avaliação da média salarial da empresa
Identificação de possíveis candidatos à promoção

## 🧠 Medidas DAX e Aplicações

### 👥 Total de Funcionários

```dax
Totalfun = COUNTROWS(DatasetRH)
```

📌 **Uso no negócio:**
Representa o headcount atual da empresa, sendo essencial para análises de capacidade operacional e crescimento.

---

### ⏳ Média de Experiência

```dax
Média ExperiênciaAnos = AVERAGE(DatasetRH[AnosExperiencia])
```

📌 **Uso no negócio:**
Permite avaliar o nível de senioridade da equipe, ajudando na tomada de decisão sobre treinamentos e contratações.

---

### 🚹 Total de Funcionários Masculinos

```dax
TotalMasculino = CALCULATE(COUNTROWS(DatasetRH), DatasetRH[Genero] = "Masculino")
```

📌 **Uso no negócio:**
Ajuda na análise de diversidade e composição da força de trabalho.

---

### 📊 % de Funcionários Masculinos

```dax
% Masculino = DIVIDE([TotalMasculino], [Totalfun])
```

📌 **Uso no negócio:**
Permite avaliar proporcionalmente a distribuição de gênero na empresa.

---

### 🚺 Total de Funcionárias Femininas

```dax
TotalFeminino = CALCULATE(COUNTROWS(DatasetRH), DatasetRH[Genero] = "Feminino")
```

📌 **Uso no negócio:**
Complementa a análise de diversidade organizacional.

---

### 📊 % de Funcionárias Femininas

```dax
% Feminino = DIVIDE([TotalFeminino], [Totalfun])
```

📌 **Uso no negócio:**
Fundamental para indicadores de equidade e inclusão.

---

### 💰 Média Salarial

```dax
Média Salarial = AVERAGE(DatasetRH[SalarioMensal])
```

📌 **Uso no negócio:**
Permite avaliar o custo médio da força de trabalho e apoiar decisões de orçamento e remuneração.

---

### 📈 Total de Funcionários Elegíveis para Promoção *(Backoffice)*

```dax
TotalPromocao = CALCULATE(COUNTROWS(DatasetRH), DatasetRH[Ano] >= 5)
```

📌 **Uso no negócio:**
Identifica colaboradores com maior tempo de empresa, auxiliando na definição de planos de carreira e retenção de talentos.

---

### 📊 % de Funcionários Elegíveis para Promoção *(Backoffice)*

```dax
% Promocao = DIVIDE([TotalPromocao], [Totalfun])
```

📌 **Uso no negócio:**
Mostra o percentual da equipe pronta para evolução, ajudando no planejamento estratégico de crescimento interno.

---

## 💡 Resultado Esperado

O projeto entrega uma visão completa sobre:

* Estrutura organizacional
* Perfil dos colaboradores
* Indicadores de diversidade
* Potencial de crescimento interno

Permitindo que gestores tomem decisões mais assertivas baseadas em dados.

## 🛠️ Ferramentas Utilizadas

* Power BI
* DAX
* Modelagem de Dados

---

✍️ Projeto desenvolvido para fins de estudo e aprimoramento em análise de dados.
