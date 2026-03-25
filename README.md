# Previsão de Séries Temporais — Holt‑Winters

Este projeto cria e analisa **dados sintéticos** que simulam a temperatura operacional de um motor ao longo do tempo, com **tendência**, **sazonalidade diária** e **ruído**. O objetivo é aplicar um modelo de previsão de séries temporais (Holt‑Winters / Suavização Exponencial) e **comparar o desempenho** com um modelo **baseline ingênuo**.

> Observação: este notebook foi construído aplicando conhecimentos do curso da capacitação do **PNAAT — Análise Preditiva de Dados de Sensores**.

---

## Visão geral

A série temporal é gerada com:
- **Tendência (trend):** crescimento gradual (ex.: 30°C → 35°C ao longo do período).
- **Sazonalidade (seasonality):** ciclo diário simulado com seno (período de 96 pontos = 24h com amostragem a cada 15 min).
- **Ruído (noise):** variação aleatória (distribuição normal).

Em seguida:
1. O dataset é dividido em **treino** e **teste** (últimas 24h como teste).
2. Treina-se um modelo **Holt‑Winters** com tendência e sazonalidade aditivas.
3. Cria-se uma **baseline sazonal ingênua (Seasonal Naive)** para comparação.
4. Avalia-se o desempenho com métricas de erro.

---

## Estrutura do notebook (pipeline)

1. **Geração do índice temporal** (7 dias em intervalos de 15 minutos)  
2. **Construção da série sintética**
   - trend + seasonality + noise
3. **DataFrame**
4. **Split treino/teste**
5. **Modelo Holt‑Winters (ExponentialSmoothing)**
6. **Baseline (Seasonal Naive)**
7. **Comparação de métricas**
8. **Gráficos de validação** (real x previsto x baseline)

---

## Modelos usados

### 1) Holt‑Winters (Suavização Exponencial)
Configurado com:
- `trend='add'`
- `seasonal='add'`
- `seasonal_periods=96` (ciclo diário de 24h)

### 2) Baseline — Seasonal Naive
Assume que as próximas 24h serão iguais às últimas 24h do conjunto de treino (repete o padrão sazonal mais recente), **sem aprender tendência**.

---

## Métricas de avaliação

O projeto utiliza:
- **MAE** (Erro Médio Absoluto) — em °C
- **RMSE** (Raiz do Erro Quadrático Médio) — em °C
- **MAPE** (Erro Percentual Absoluto Médio) — em %

A expectativa é o Holt‑Winters ter erros menores que a baseline (o que indica ganho real do modelo).

---

## Principais bibliotecas

- **NumPy** — geração de dados e ruído
- **Pandas** — index temporal e DataFrame
- **Matplotlib** — visualizações
- **Statsmodels** — Holt‑Winters (ExponentialSmoothing)
- **Scikit-learn** — métricas (MAE, RMSE, MAPE)

---

## Como executar

1. Abra o notebook `time_series_forecasting.ipynb` no Jupyter/Colab.
2. Execute as células em ordem.
3. Verifique:
   - saída das métricas (Holt‑Winters vs baseline)
   - gráfico final com as três curvas (treino, teste, previsão e baseline)

---

## Observações e possíveis melhorias

- Testar **intervalos maiores** (mais semanas/meses) para avaliar estabilidade do modelo.
- Fazer **validação temporal** (ex.: walk-forward / rolling forecast origin) ao invés de uma única divisão treino/teste.
- Avaliar outras abordagens (ARIMA/SARIMA, Prophet, modelos ML com features de tempo, etc.).

---

## Autor

Projeto desenvolvido para prática de previsão de séries temporais com dados de sensores, aplicando os conhecimentos da capacitação do **PNAAT — Análise Preditiva de Dados de Sensores**.
