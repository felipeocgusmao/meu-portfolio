---
title: "Análise Exploratória: Airbnb em Barcelona"
description: "Análise de 300 acomodações do Airbnb em Barcelona para identificar padrões de preço, distribuição por bairros e correlação entre avaliações e valor da diária."
publishDate: "14 May 2026"
tags: ["python", "data-analysis", "pandas", "matplotlib", "jupyter", "eda"]
---

## Sobre o projeto

Esse projeto nasceu de uma pergunta simples: **o que determina o preço de uma acomodação no Airbnb em Barcelona?**

Usando um dataset público do Kaggle com 300 listagens, realizei uma análise exploratória completa para identificar padrões de preço, entender a distribuição geográfica das acomodações e investigar se avaliações altas realmente influenciam o valor cobrado.

## Dataset

- **Fonte:** Kaggle — Comparative Analysis of Airbnb Prices in Barcelona
- **Volume:** 300 acomodações
- **Variáveis:** preço, bairro, tipo de acomodação, avaliações dos hóspedes

## Perguntas que guiaram a análise

1. Quais bairros têm os maiores preços médios por diária?
2. Qual é o tipo de acomodação mais comum na cidade?
3. Existe correlação entre a nota dos hóspedes e o preço cobrado?

## Principais descobertas

### Preço por bairro
Bairros como **Eixample** lideram em valor médio de diária, refletindo sua localização central e alta demanda turística. A variação de preços entre bairros é significativa — o que mostra que localização é o fator dominante na precificação.

### Tipo de acomodação
Quartos individuais representam cerca de **63% das listagens**, sendo o tipo mais comum. Isso indica que o mercado de Barcelona é dominado por anfitriões que alugam um cômodo da própria casa, e não propriedades inteiras.

### Avaliação vs. Preço
A análise de correlação revelou algo contraintuitivo: **avaliações altas não implicam preços altos**. A relação entre nota dos hóspedes e valor da diária é fraca, sugerindo que qualidade percebida e preço são dimensões independentes nesse mercado.

## Stack utilizada

```python
import pandas as pd
import matplotlib.pyplot as plt
import jupyter
```

| Ferramenta | Uso |
|---|---|
| Python 3.13 | Linguagem principal |
| Pandas | Limpeza e manipulação dos dados |
| Matplotlib | Visualizações e gráficos |
| Jupyter Notebook | Ambiente de análise e documentação |

## Estrutura do projeto

```
projeto_1/
├── data/          # Dataset original do Kaggle
├── notebooks/     # Análises em Jupyter
├── outputs/       # Gráficos e resultados exportados
├── src/           # Funções reutilizáveis
└── requirements.txt
```

## O que aprendi

Esse projeto consolidou minha prática com o ciclo completo de uma EDA:

- **Limpeza de dados** — tratar valores nulos, padronizar tipos e remover outliers sem perder informação relevante
- **Visualização orientada a perguntas** — cada gráfico responde uma hipótese específica, não é decorativo
- **Interpretação de correlação** — a ausência de correlação entre avaliação e preço é tão informativa quanto uma correlação forte

## Código

Repositório completo disponível no GitHub:

[github.com/felipeocgusmao/projeto_1](https://github.com/felipeocgusmao/projeto_1)
