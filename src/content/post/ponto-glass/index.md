---
title: "PontoGlass: Sistema de Controle de Ponto Digital"
description: "Sistema full-stack de gestão de ponto digital com Next.js 14, Supabase e JWT — painel ao vivo, exportação PDF/CSV, PWA e suporte a 4 idiomas."
publishDate: "23 May 2026"
tags: ["nextjs", "typescript", "supabase", "fullstack", "postgresql"]
---

## Sobre o projeto

O **PontoGlass** nasceu de uma necessidade real: permitir que funcionários registrem entradas e saídas pelo celular, enquanto gestores acompanham tudo em tempo real — sem infraestrutura local, sem complicação.

É um sistema full-stack completo, com três níveis de acesso (funcionário, gestor e administrador), construído com Next.js 14 e Supabase.

## O que foi construído

### Para funcionários

- Relógio ao vivo com status em tempo real (dentro / pausa / fora)
- Registro de entrada, saída e pausas (almoço, café)
- Visualização de ganhos diários calculados automaticamente
- Histórico mensal com visualização em calendário
- Solicitações de correção de registros

### Para gestores

- Painel de status ao vivo de toda a equipe
- Histórico detalhado por funcionário
- Relatórios com exportação em **CSV e PDF** (jsPDF + AutoTable)
- Gestão de banco de horas

### Para administradores

- CRUD completo de funcionários
- Configuração de jornadas, horários e valores por hora
- **Audit log** de todas as ações do sistema
- Modo quiosque para tablet compartilhado
- Gestão de feriados e ausências

## Stack técnica

| Camada | Tecnologia |
|---|---|
| Frontend | Next.js 14 (App Router) + TypeScript strict |
| Banco de dados | Supabase (PostgreSQL gerenciado) |
| Autenticação | JWT em httpOnly cookies + bcryptjs |
| Notificações | Web Push API com VAPID |
| Documentos | jsPDF + AutoTable |
| Email | Nodemailer |
| Deploy | Vercel com Cron Jobs |

## Funcionalidades de destaque

**PWA nativa** — instalável no celular como app, com notificações push nativas.

**Multilíngue** — suporte completo a PT-PT, PT-BR, EN e ES com internacionalização.

**Turno noturno** — ajuste automático de data para turnos que cruzam a meia-noite.

**Geolocalização** — configurável por funcionário para validar o local do registro.

**Design system próprio** — construído com CSS Variables sem depender de frameworks de UI.

## O que aprendi

Esse projeto foi um salto para o desenvolvimento full-stack com foco em produto real:

- Modelagem de banco de dados relacional para múltiplos perfis de acesso
- Autenticação segura com JWT em cookies httpOnly (sem localStorage)
- Arquitetura de App Router no Next.js 14 com Server e Client Components
- Geração de documentos PDF diretamente no servidor
- Deploy de aplicações com Cron Jobs no Vercel

## Código

::github{repo="felipeocgusmao/ponto-glass-next"}
