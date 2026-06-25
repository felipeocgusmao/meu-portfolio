---
title: "pandas .query() para filtros mais expressivos em DataFrames"
publishDate: "2026-05-28T11:00:00+02:00"
---

A sintaxe de filtragem booleana padrão do pandas funciona, mas se torna verbosa rapidamente com múltiplas condições. O método `.query()` oferece uma alternativa mais expressiva:

```python
# filtragem booleana padrão
df[(df["status"] == "completed") & (df["total"] > 100)]

# com .query()
df.query("status == 'completed' and total > 100")
```

Para referenciar variáveis do escopo externo, use o prefixo `@`:

```python
threshold = 100
df.query("total > @threshold")
```

`.query()` é especialmente vantajoso em notebooks, onde a legibilidade do código tem peso tão grande quanto o resultado em si. Para filtragens que envolvem índices, operações vetorizadas ou chamadas de método, a sintaxe booleana padrão ainda é a escolha mais adequada.
