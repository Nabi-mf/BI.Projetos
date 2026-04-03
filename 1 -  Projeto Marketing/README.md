# 📊 Análise de Campanhas de Marketing (Power BI)

## 🎯 Objetivo

Este mini-projeto apresenta uma introdução prática à análise de campanhas de marketing utilizando o Power BI, seguindo uma abordagem estruturada focada em geração de insights para tomada de decisão.

## 📌 Sobre o Projeto

O projeto foi desenvolvido com dados customizados que representam informações sobre clientes e campanhas de marketing realizadas por uma empresa.

Ao longo da análise, foram construídos:

* 4 dashboards interativos
* Mais de 10 elementos visuais
* Customizações e formatações avançadas
* Tratamento e correção de dados
* Aplicação de diferentes recursos do Power BI

## 📊 Estrutura das Análises

Os relatórios foram organizados em quatro visões principais:

### 👤 Visão do Cliente

Análise do perfil dos clientes, identificando características relevantes para segmentação.

### 🛒 Comportamento de Compra

Exploração dos hábitos de consumo, frequência de compras e preferências dos clientes.

### 📢 Performance das Campanhas

Avaliação da efetividade das campanhas de marketing, medindo impacto e resultados.

### 🌍 Padrões de Compra por País

Identificação de tendências de compra no ponto de venda com base na localização geográfica.

## 📈 Metodologia

Para cada visão foram realizadas:

* Análise das variáveis
* Criação de gráficos e dashboards
* Desenvolvimento de medidas (DAX)
* Extração de métricas relevantes
* Cruzamento de dados para geração de insights

## 🧠 Medidas DAX Criadas

### 💰 Total Gasto por Cliente

Medida responsável por calcular o valor total gasto por cliente, somando diferentes categorias de consumo.

```dax
TotalGasto = 
SUMX(
    dados_marketing,
    dados_marketing[Gasto com Alimentos] +
    dados_marketing[Gasto com Brinquedos] +
    dados_marketing[Gasto com Eletronicos] +
    dados_marketing[Gasto com Moveis] +
    dados_marketing[Gasto com Utilidades] +
    dados_marketing[Gasto com Vestuario]
)
```

📌 **Insight técnico:**
Essa medida utiliza `SUMX` para iterar linha a linha na tabela, garantindo o cálculo correto do total gasto considerando múltiplas colunas de consumo.

📊 **Aplicação no projeto:**

* Identificação dos clientes com maior valor agregado
* Segmentação por nível de consumo
* Base para análise de comportamento e campanhas

## 💡 Resultado Esperado

O projeto entrega uma visão completa sobre:

* Perfil dos clientes
* Padrões de compra
* Efetividade das campanhas de marketing

Permitindo que tomadores de decisão utilizem os dados de forma estratégica.

## 🛠️ Ferramentas Utilizadas

* Power BI
* DAX
* Modelagem de Dados

---

✍️ Projeto desenvolvido para fins de estudo e aprimoramento em análise de dados.
