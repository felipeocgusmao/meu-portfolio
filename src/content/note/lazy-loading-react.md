---
title: "Lazy loading: ~500 KB a menos no bundle inicial"
publishDate: "2026-06-17T14:00:00+02:00"
---

No dashboard do Ponto Glass, duas abas carregavam bibliotecas pesadas: exportação de PDF (~300 KB com `jspdf`) e exportação de Excel (~200 KB com `xlsx`). Ambas eram importadas no topo do arquivo — mesmo que o usuário nunca abrisse essas abas.

A solução foi substituir por `next/dynamic` com `{ ssr: false }`:

```typescript
const RelatoriosTab = dynamic(() => import("./RelatoriosTab"), { ssr: false });
const RegistrosTab = dynamic(() => import("./RegistrosTab"), { ssr: false });
```

Resultado: aproximadamente 500 KB a menos no bundle inicial. O único custo é um estado de loading na primeira abertura de cada aba — aceitável para funcionalidades de uso eventual.

O critério para aplicar lazy loading: o componente precisa satisfazer duas condições simultaneamente — (1) conter bibliotecas ou lógica pesada e (2) não estar visível no carregamento inicial. Lazy loading em componentes leves ou acima da dobra piora a experiência sem nenhum ganho de performance mensurável.
