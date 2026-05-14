---
title: "Análise de Vendas com SQL: do básico ao avançado"
description: "Queries SQL que todo Data Analyst precisa dominar — análise de vendas com agregações, ranking, crescimento mensal e identificação de clientes em risco."
publishDate: "14 May 2026"
tags: ["sql", "data-analysis", "analytics"]
---

## Contexto

Imagine que você recebeu acesso ao banco de dados de uma loja de e-commerce com três tabelas principais:

```sql
-- Clientes
customers (id, name, city, created_at)

-- Pedidos
orders (id, customer_id, total, status, created_at)

-- Itens do pedido
order_items (id, order_id, product, category, quantity, price)
```

Abaixo estão as análises que um Data Analyst faria nas primeiras horas de acesso a esses dados.

---

## 1. Visão geral do negócio

Antes de qualquer análise, entender o tamanho dos dados:

```sql
SELECT
    COUNT(DISTINCT customer_id) AS total_clientes,
    COUNT(*)                    AS total_pedidos,
    SUM(total)                  AS receita_total,
    AVG(total)                  AS ticket_medio,
    MIN(created_at)             AS primeiro_pedido,
    MAX(created_at)             AS ultimo_pedido
FROM orders
WHERE status = 'completed';
```

---

## 2. Receita por mês (crescimento MoM)

Acompanhar a evolução da receita mês a mês usando `LAG` para calcular a variação:

```sql
WITH receita_mensal AS (
    SELECT
        DATE_TRUNC('month', created_at) AS mes,
        SUM(total)                       AS receita
    FROM orders
    WHERE status = 'completed'
    GROUP BY 1
)
SELECT
    mes,
    receita,
    LAG(receita) OVER (ORDER BY mes)                        AS receita_mes_anterior,
    ROUND(
        (receita - LAG(receita) OVER (ORDER BY mes))
        / LAG(receita) OVER (ORDER BY mes) * 100, 2
    )                                                        AS crescimento_pct
FROM receita_mensal
ORDER BY mes;
```

> **Por que isso importa:** crescimento MoM é uma das métricas mais pedidas em reuniões de negócio. Saber escrever essa query do zero é diferencial em entrevistas.

---

## 3. Top 10 clientes por receita

Ranking com `RANK()` para identificar os melhores clientes:

```sql
SELECT
    c.name,
    c.city,
    COUNT(o.id)    AS total_pedidos,
    SUM(o.total)   AS receita_total,
    AVG(o.total)   AS ticket_medio,
    RANK() OVER (ORDER BY SUM(o.total) DESC) AS ranking
FROM customers c
JOIN orders o ON c.id = o.customer_id
WHERE o.status = 'completed'
GROUP BY c.id, c.name, c.city
ORDER BY receita_total DESC
LIMIT 10;
```

---

## 4. Categoria de produto mais rentável

Quais categorias geram mais receita e têm maior volume?

```sql
SELECT
    oi.category,
    COUNT(DISTINCT o.id)    AS total_pedidos,
    SUM(oi.quantity)        AS unidades_vendidas,
    SUM(oi.price * oi.quantity) AS receita_total,
    ROUND(
        SUM(oi.price * oi.quantity)
        / SUM(SUM(oi.price * oi.quantity)) OVER () * 100, 1
    ) AS participacao_pct
FROM order_items oi
JOIN orders o ON oi.order_id = o.id
WHERE o.status = 'completed'
GROUP BY oi.category
ORDER BY receita_total DESC;
```

---

## 5. Clientes em risco de churn

Identificar clientes que compraram antes mas sumiram nos últimos 90 dias — candidatos a uma campanha de reativação:

```sql
WITH ultima_compra AS (
    SELECT
        customer_id,
        MAX(created_at) AS ultima_compra,
        COUNT(*)        AS total_pedidos,
        SUM(total)      AS receita_total
    FROM orders
    WHERE status = 'completed'
    GROUP BY customer_id
)
SELECT
    c.name,
    c.city,
    uc.ultima_compra,
    uc.total_pedidos,
    uc.receita_total,
    DATE_PART('day', NOW() - uc.ultima_compra) AS dias_sem_comprar
FROM ultima_compra uc
JOIN customers c ON uc.customer_id = c.id
WHERE uc.ultima_compra < NOW() - INTERVAL '90 days'
  AND uc.receita_total > 500   -- apenas clientes relevantes
ORDER BY uc.receita_total DESC;
```

> **Por que isso importa:** churn silencioso é um dos maiores problemas de e-commerce. Detectar esses clientes antes que sumam definitivamente é ação de alto impacto com baixo custo.

---

## O que essas queries mostram

| Conceito | Queries acima |
|---|---|
| Agregações (`SUM`, `AVG`, `COUNT`) | #1, #3, #4 |
| Window functions (`RANK`, `LAG`) | #2, #3 |
| CTEs (`WITH`) | #2, #5 |
| JOINs entre tabelas | #3, #4, #5 |
| Filtros com datas | #2, #5 |
| Cálculo de participação (%) | #4 |

Dominar esses padrões cobre a grande maioria das análises do dia a dia de um Data Analyst — e são os tópicos mais cobrados em processos seletivos.

---

## Próximos passos

Se quiser praticar com dados reais, alguns datasets públicos excelentes para SQL:

- [**Northwind**](https://github.com/pthom/northwind_psql) — banco clássico de e-commerce, perfeito para queries de negócio
- [**Kaggle: Brazilian E-Commerce (Olist)**](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) — dados reais de uma empresa brasileira, ótimo para portfolio
- [**Mode Analytics SQL Tutorial**](https://mode.com/sql-tutorial/) — exercícios práticos com datasets reais
