# 📊 Reestruturação de Dashboard Logístico (Power BI)

## 🎯 Objetivo

Este mini-projeto tem como objetivo revisar, corrigir e reconstruir um dashboard logístico com problemas, aplicando boas práticas de análise de dados e visualização no Power BI.

---

## 📌 Contexto do Projeto

Uma empresa de logística solicitou a criação de um dashboard para acompanhar o desempenho do processo de entrega de produtos.

O dashboard inicial apresentava diversos erros técnicos e analíticos, exigindo uma reestruturação completa para garantir confiabilidade e clareza na tomada de decisão.

---

## 📊 KPIs de Negócio

O dashboard foi desenvolvido para responder às seguintes métricas:

* 📦 Total de Entregas no Prazo por Canal
* ⚡ Percentual de Entregas Antecipadas por Equipe
* 📅 Total de Entregas por Mês
* 🏆 Entregas dos Top 5 Vendedores
* 🚨 Entregas com Atraso por Cidade
* 📊 Percentual por Status de Entrega

---

## 🧠 Medidas DAX e Aplicações

### 📦 Total de Entregas

```dax id="log1"
Total Entregas = COUNTROWS(Logistica)
```

📌 **Uso no negócio:**
Representa o volume total de entregas realizadas, sendo a base para todos os indicadores logísticos.

---

### ⏱️ Entregas no Prazo

```dax id="log2"
EntregasNoPrazo = 
CALCULATE(
    [Total Entregas],
    FILTER(
        Logistica,
        Logistica[Status_Entrega] = "Antecipado" 
        || Logistica[Status_Entrega] = "No Prazo"
    )
)
```

📌 **Uso no negócio:**
Permite medir a eficiência operacional, agrupando entregas realizadas dentro ou antes do prazo esperado.

---

### ⭐ Rating de Performance

```dax id="log3"
Rating = 
VAR __MAX_NUMBER_OF_STARS = 5
VAR __MIN_RATED_VALUE = 1500
VAR __MAX_RATED_VALUE = 2500
VAR __BASE_VALUE = [Total Entregas]
VAR __NORMALIZED_BASE_VALUE =
    MIN(
        MAX(
            DIVIDE(
                __BASE_VALUE - __MIN_RATED_VALUE,
                __MAX_RATED_VALUE - __MIN_RATED_VALUE
            ),
            0
        ),
        1
    )
VAR __STAR_RATING = ROUND(__NORMALIZED_BASE_VALUE * __MAX_NUMBER_OF_STARS, 0)
RETURN
    IF(
        NOT ISBLANK(__BASE_VALUE),
        REPT(UNICHAR(9733), __STAR_RATING)
        & REPT(UNICHAR(9734), __MAX_NUMBER_OF_STARS - __STAR_RATING)
    )
```

📌 **Uso no negócio:**
Transforma o volume de entregas em uma avaliação visual (estrelas), facilitando a interpretação rápida da performance operacional por gestores.

---

## 🛠️ Abordagem da Solução

* Análise do dashboard original
* Identificação e correção de erros
* Criação e ajuste de medidas DAX
* Reestruturação dos visuais
* Aplicação de boas práticas de BI

---

## 💡 Resultado Esperado

A nova versão do dashboard permite:

* Monitoramento eficiente das entregas
* Identificação de gargalos logísticos
* Avaliação de performance por equipe e canal
* Tomada de decisão baseada em dados confiáveis

---

## 📂 Estrutura do Projeto

* `Mini-Projeto4-Parte1.pbix` → Versão com erros
* `LAB 4 - Logistica.pbix` → Versão otimizada
* `README.md` → Documentação do projeto

---

## 🛠️ Ferramentas Utilizadas

* Power BI
* DAX
* Modelagem de Dados

---

✍️ Projeto desenvolvido para fins de estudo e aprimoramento em análise de dados.
