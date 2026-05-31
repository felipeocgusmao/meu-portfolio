---
title: "Ponto Glass: Controle de Ponto via Smart Glasses"
description: "Sistema de registo de jornada laboral para trabalhadores de campo via óculos inteligentes — conformidade com o Real Decreto-lei 8/2019 espanhol, Next.js 14 e Supabase."
publishDate: "31 May 2026"
tags: ["nextjs", "typescript", "supabase", "fullstack", "postgresql"]
---

## O problema real

Em Espanha, o **Real Decreto-lei 8/2019** obriga todas as empresas a registar digitalmente a jornada de trabalho de cada funcionário. O não cumprimento resulta em multas significativas.

O problema: trabalhadores de campo — em obras de construção civil, limpeza, logística e segurança — frequentemente não têm acesso fácil a um smartphone durante o trabalho. Pedir a um pedreiro que tire as luvas, desbloqueie o telemóvel e registe o ponto num app é um atrito enorme.

**Ponto Glass resolve isso de forma hands-free, via óculos inteligentes (smart glasses).**

## A solução

O trabalhador faz check-in e check-out através de óculos Android — sem tocar no telemóvel, sem interromper o trabalho. A interface foi desenhada especificamente para ecrãs pequenos e uso em campo.

Do outro lado, gestores e administradores acompanham tudo em tempo real num dashboard web.

## Público-alvo

- Empresas de construção civil com equipas em campo
- Empresas de limpeza, logística e segurança privada
- Qualquer setor com trabalhadores em ambientes hostis ou hands-free
- PMEs espanholas que precisam cumprir a lei de registo de jornada

## O que foi construído

### Perfil: Trabalhador de Campo

- Check-in e check-out via smart glasses (interface otimizada para ecrã pequeno)
- Visualização do histórico de registos pessoais
- Notificação de horas em falta ou esquecimento de saída

### Perfil: Gerente / Encarregado

- Dashboard com presença da equipa em tempo real
- Alertas de trabalhadores sem check-in dentro do horário esperado
- Relatórios de horas por trabalhador e por projeto

### Perfil: Administrador da Empresa

- Gestão completa de utilizadores e permissões
- Configuração de horários e projetos
- Exportação de relatórios para conformidade legal
- Auditoria completa de todos os registos

## Stack técnica

| Categoria | Tecnologia | Função |
|---|---|---|
| Frontend | Next.js 14 (React) | Interface web principal |
| Estilização | Tailwind CSS | Design system responsivo |
| Backend/BaaS | Supabase | PostgreSQL + Auth + RLS |
| Autenticação | Supabase Auth | Login seguro por empresa/perfil |
| Hardware | Smart Glasses (Android) | Dispositivo de input dos trabalhadores |
| Deploy | Vercel | Hospedagem e CI/CD automático |

## Segurança e conformidade RGPD

O sistema trata dados pessoais de trabalhadores, por isso a segurança foi prioridade desde o início:

| Camada | Implementação |
|---|---|
| Isolamento de dados | Row Level Security (RLS) no Supabase/PostgreSQL |
| Autenticação | Tokens JWT via Supabase Auth |
| Controlo de acessos | Permissões por perfil (worker / manager / admin) |
| Comunicação cifrada | HTTPS em toda a aplicação (Vercel + Supabase) |
| Auditoria | Logs imutáveis de todos os registos de ponto |
| Conformidade RGPD | Dados em infraestrutura europeia |

## Demo ao vivo

A aplicação está deployada e acessível publicamente como prova de conceito:

**[ponto-glass-next.vercel.app](https://ponto-glass-next.vercel.app)**

Permite testar o fluxo completo de registo de ponto, dashboard e gestão de utilizadores — preparada para ser mostrada a potenciais clientes sem necessidade de instalação.

## O que aprendi

- Modelagem de banco de dados relacional com múltiplos perfis de acesso e RLS
- Arquitetura de App Router no Next.js 14 com Server e Client Components
- Desenvolvimento de interfaces para hardware não-convencional (smart glasses)
- Conformidade legal como requisito de produto, não como afterthought
- Estratégia de repositórios: código privado + demo pública como cartão de visita

## Repositório público

::github{repo="felipeocgusmao/ponto-glass-demo"}
