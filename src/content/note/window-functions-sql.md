---
title: "Window functions mudam tudo em SQL"
publishDate: "2026-06-04T09:00:00+02:00"
---

Se você ainda está resolvendo ranking com subqueries, vale descobrir as window functions.

`RANK()`, `ROW_NUMBER()`, `LAG()`, `LEAD()` — todas rodam **sem colapsar as linhas** da query, ao contrário de `GROUP BY`. Você mantém o detalhe e ainda calcula o agregado na mesma linha.

O caso que me fez entender isso de vez: calcular o crescimento MoM de receita. Com `LAG()` é uma linha. Sem ela, seria uma CTE inteira só pra isso.

```sql
LAG(receita) OVER (ORDER BY mes)
```

Simples assim.
