---
title: "pandas .query() deixa filtros muito mais legíveis"
publishDate: "2026-05-28T11:00:00+02:00"
---

Troquei o filtro boilerplate por `.query()` e o notebook ficou bem mais fácil de ler:

```python
# antes
df[(df["status"] == "completed") & (df["total"] > 100)]

# depois
df.query("status == 'completed' and total > 100")
```

Funciona com variáveis do escopo usando `@`:

```python
limite = 100
df.query("total > @limite")
```

Ainda prefiro o modo explícito quando o filtro envolve índices ou métodos, mas para condições simples `.query()` ganha fácil em legibilidade.
