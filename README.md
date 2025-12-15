# Forecasting-de-Vendas
Prever demanda de estoque para varejo.


# 📈 Forecast AI: Previsão de Demanda para Varejo

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Status](https://img.shields.io/badge/Status-Concluído-success)
![Focus](https://img.shields.io/badge/Foco-Business_Insights-orange)

## 💼 O Desafio de Negócio
Uma grande rede de varejo (Superstore) enfrenta o desafio clássico de **balanceamento de estoque**:
* **Excesso de estoque:** Custo de armazenamento e capital parado.
* **Falta de estoque (Stockout):** Perda de receita e insatisfação do cliente.

**Objetivo:** Desenvolver um modelo de Machine Learning (Time Series) capaz de prever a demanda futura com precisão suficiente para orientar a logística, validando os resultados com dados reais de 2023 antes de projetar 2024.

---

## 🔍 A Jornada do Projeto (Storytelling)

Este projeto não seguiu apenas uma linha reta. Ele foi construído através de ciclos de **testes de hipóteses e descobertas estatísticas**.

### Fase 1: A Escolha do Modelo Global (Aditivo vs Multiplicativo)
Minha primeira hipótese era que, devido ao crescimento da empresa, um modelo **Multiplicativo** (que amplia a sazonalidade conforme o volume cresce) seria superior.
* **Resultado:** Os testes mostraram que o modelo **Aditivo** (sazonalidade fixa) foi mais robusto e estável para os dados de teste.
* **Decisão:** Seguir com o modelo Aditivo como base (Baseline).

![Batalha de Modelos](grafico_1_global.png)

### Fase 2: O Mistério Regional (A Armadilha do MAPE)
Ao quebrar a previsão por regiões (Norte, Sul, Leste, Oeste), os dados indicaram um **erro catastrófico de ~57% na região Sul**.
* **Investigação:** Aprofundando a análise, descobri que o erro percentual (MAPE) estava distorcido pelo **baixo volume de vendas** dessa região (efeito do "denominador pequeno").
* **Solução:** Alterei a métrica de avaliação para **MAE (Erro Absoluto em Unidades)**.
* **Insight de Negócio:** O erro operacional do Sul (~27 caixas) é, na verdade, idêntico ao das outras regiões. O verdadeiro risco logístico foi identificado na região **Oeste**, que possui o maior desvio absoluto de estoque.

![Analise Regional](grafico_2_regional.png)

### Fase 3: Otimização e Prova Real (2023)
Utilizei **Grid Search** para testar todas as combinações possíveis de hiperparâmetros (Tendência, Sazonalidade, Amortecimento) automaticamente.
* O modelo vencedor foi confrontado com os dados reais de 2023 (que o modelo não tinha visto durante o treino).
* **Resultado:** O modelo seguiu a tendência real com alta aderência, validando sua confiança para produção.

![Prova Real 2023](grafico_3_validacao_real.png)

---

##  O Futuro: Previsão 2024
Com o modelo validado, geramos a projeção final de demanda para o próximo ano fiscal.

![Previsão Final](grafico_4_futuro_final.png)

> **Entrega Final:** Os dados previstos foram exportados para `data/forecast_final_2024.csv` para consumo da equipe de planejamento.

---

## 🛠️ Tecnologias Utilizadas
* **Linguagem:** Python
* **Manipulação de Dados:** Pandas, Numpy
* **Visualização:** Matplotlib, Seaborn
* **Modelagem Estatística:** Statsmodels (Holt-Winters Exponential Smoothing)
* **Métricas de Performance:** Scikit-Learn (MAE, MAPE)

## ⚙️ Como Executar
1. Clone o repositório:
```bash
git clone [https://github.com/pedropaivasanrj-alt/Forecasting-de-Vendas.git](https://github.com/pedropaivasanrj-alt/Forecasting-de-Vendas.git)