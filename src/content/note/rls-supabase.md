---
title: "Row Level Security: isolamento de dados no nível do banco"
publishDate: "2026-06-10T10:00:00+02:00"
---

A abordagem mais comum para isolar dados de múltiplos tenants é validar o perfil do usuário na camada de aplicação antes de cada query. O problema: qualquer falha nessa lógica pode expor dados de outras empresas.

Row Level Security (RLS) move esse controle para dentro do PostgreSQL. Com RLS ativado, toda query é automaticamente filtrada pelas políticas definidas no banco — independentemente de como foi construída na aplicação.

```sql
-- retorna apenas registros da empresa do usuário autenticado
CREATE POLICY "users see own company"
ON registros_ponto
FOR SELECT
USING (empresa_id = (auth.jwt() ->> 'empresa_id')::uuid);
```

O Supabase expõe o JWT do usuário autenticado diretamente nas políticas via `auth.jwt()`, tornando o padrão direto de implementar. O benefício central: o isolamento funciona por padrão — via aplicação, Supabase Studio ou qualquer cliente SQL.

No Ponto Glass, RLS foi o mecanismo de separação entre empresas: cada empresa enxerga apenas seus próprios trabalhadores, registros e relatórios, sem nenhuma lógica adicional na camada de aplicação para garantir isso.

Regra prática: se uma tabela contém dados de múltiplos tenants, RLS é mais seguro e mais confiável do que isolamento implementado no servidor.
