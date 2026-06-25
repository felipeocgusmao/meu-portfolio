---
title: "Window functions: cálculos analíticos sem perder o detalhe das linhas"
publishDate: "2026-06-04T09:00:00+02:00"
---

Window functions resolvem uma limitação central do `GROUP BY`: a perda do detalhe das linhas originais após a agregação.

Com `RANK()`, `ROW_NUMBER()`, `LAG()` e `LEAD()`, os cálculos analíticos são executados **sobre o conjunto de linhas original** — sem colapsá-lo. É possível manter o nível de detalhe e acessar o valor calculado na mesma linha.

Um exemplo concreto: calcular o crescimento mês a mês de receita. Com `LAG()`, é uma expressão na cláusula `SELECT`:

```sql
receita - LAG(receita) OVER (ORDER BY mes) AS variacao_mom
```

Sem window functions, o mesmo resultado exigiria uma CTE para materializar o mês anterior e um join posterior — mais código e mais pontos de falha.

Casos de uso mais comuns:
- Ranking de clientes ou produtos por métrica — `RANK`, `DENSE_RANK`
- Numeração sequencial de registros por grupo — `ROW_NUMBER`
- Comparação com período anterior ou seguinte — `LAG`, `LEAD`
- Totais acumulados — `SUM ... OVER (ORDER BY ...)`
