---
title: "80% do tempo em dados é limpeza — e está certo"
publishDate: "2026-05-20T14:00:00+02:00"
---

Limpeza de dados frequentemente é tratada como overhead — a parte operacional antes da "análise de verdade". Na prática, é exatamente o contrário.

A etapa de limpeza **é** a análise. É o momento em que se entende o que os dados representam de fato: onde estão as lacunas, quais campos foram mal registrados, quais valores fogem do padrão esperado. Pular essa etapa é chegar a conclusões incorretas apresentadas com gráficos bem elaborados.

Na análise do Airbnb em Barcelona, os preços incluíam outliers extremos — listagens com €1 e €9.999 na mesma coluna. Se a média tivesse sido calculada diretamente sobre os dados brutos, o resultado não teria nenhuma aderência ao mercado real.

A regra prática: dado sujo com análise elaborada produz insight incorreto. Dado limpo com análise simples produz decisão correta.
