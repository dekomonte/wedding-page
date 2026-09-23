# 💍 Wedding Page

Aplicação web fullstack para gerenciamento completo de um casamento, com área pública informativa e portal autenticado para **RSVP, acompanhantes, mensagens e lista de presentes**.

Este projeto também é utilizado como estudo prático e consolidação de arquitetura web moderna, cobrindo **frontend, backend, banco de dados relacional, autenticação JWT com Refresh Token, autorização via RBAC e DevOps básico**.

---

## 📌 Gerenciamento do Projeto (GitHub Project)

O acompanhamento e o fluxo de desenvolvimento do projeto são gerenciados utilizando o **GitHub Projects** (estilo Kanban com suporte a Milestones, Issues e Tasklists).

* 🗺️ **Quadro do Projeto:** [Wedding Page Development Board](https://github.com/seu-usuario/seu-repositorio/projects) *(atualize com o link real do seu project)*
* 🏷️ **Padrão de Labels:** Categorização por camadas (`frontend`, `backend`, `database`, `devops`, `auth`, `rsvp`, `gifts`, `public`, `admin`, `study`, `setup`, `testing`, `deploy`).

---

## 🎯 Funcionalidades

### 🌐 Área Pública
* [ ] Página inicial (Landing Page com Hero Banner e contagem regressiva)
* [ ] Nossa história (Linha do tempo interativa e galeria de fotos do casal)
* [ ] Informações do evento (Data, horário e dress code)
* [ ] Localização (Mapa interativo para cerimônia e festa)
* [ ] Dicas úteis (Hospedagem, transporte, salões de beleza e estacionamento)

### 🔐 Autenticação & Segurança
* [ ] Cadastro e login de convidados
* [ ] Persistência de sessão segura com Access Token (JWT) e Refresh Token
* [ ] Controle de Acesso Baseado em Funções (**RBAC**) no Backend
* [ ] Simulação/Recuperação de senha
* [ ] Encriptação de senhas com algoritmo de Hashing (bcrypt/argon2)

### 📩 RSVP (Confirmação de Presença)
* [ ] Confirmar ou recusar presença
* [ ] Registro dinâmico de acompanhantes (respeitando o limite do convidado)
* [ ] Alteração de status da confirmação enquanto o RSVP estiver aberto
* [ ] Envio de mensagem personalizada dos convidados aos noivos

### 🎁 Lista de Presentes
* [ ] Visualização interativa do catálogo com filtros e busca
* [ ] Reserva online de presentes
* [ ] Controle de estoque/disponibilidade em tempo real
* [ ] Regra de limite máximo de presentes reservados por convidado
* [ ] Cancelamento de reserva por parte do convidado

### 👑 Painel dos Noivos & Administração
* [ ] **Dashboard Resumo:** Total de convidados, presenças, ausências e presentes reservados
* [ ] Gestão da lista de convidados e visualização de acompanhantes
* [ ] Leitura das mensagens enviadas pelos convidados
* [ ] **CRUD de Presentes:** Cadastrar, editar e remover itens do catálogo
* [ ] Mapeamento e gestão de reservas efetuadas

---

## 👥 Perfis de Acesso (RBAC)

| Perfil | Nível de Acesso |
| :--- | :--- |
| **Admin** | Acesso total às configurações do sistema, usuários e gerenciamento geral. |
| **Noivos** | Acesso ao Dashboard exclusivo, gestão de convidados, RSVP, mensagens e catálogo de presentes. |
| **Convidado** | Acesso aos próprios dados cadastrais, envio de RSVP e reserva/cancelamento de presentes. |

---

## 📐 Regras de Negócio Chave

### RSVP
1. Cada convidado pode registrar apenas **um RSVP ativo**.
2. O número de acompanhantes informados **não pode exceder** o campo `max_companions` atribuído ao convidado.
3. As confirmações só podem ser alteradas enquanto a janela de RSVP estiver configurada como **aberta**.

### Lista de Presentes
1. Todos os visitantes podem visualizar o catálogo; a reserva exige **autenticação**.
2. Um presente **não pode ter mais reservas** do que a quantidade cadastrada (`total_quantity`).
3. Cada convidado respeita um **limite máximo de reservas ativas**.
4. Os noivos têm visibilidade completa sobre quem reservou cada item.

---

## 🏗️ Arquitetura do Sistema

```text
┌──────────────────────────────────────┐
│           Next.js 14+                │
│    Frontend (App Router & React)     │
└──────────────────┬───────────────────┘
                   │
                   │ HTTP / REST (JSON + JWT)
                   ▼
┌──────────────────────────────────────┐
│             NestJS                   │
│   Backend (API REST, Guards, RBAC)   │
└──────────────────┬───────────────────┘
                   │
                   │ Prisma ORM
                   ▼
┌──────────────────────────────────────┐
│           PostgreSQL                 │
│      Database (Docker Container)     │
└──────────────────────────────────────┘

# 🗄️ Modelo de Dados (Relacional)

```text
[ User ] ─── (1:1) ─── [ Guest ] ─── (1:1) ─── [ RSVP ]
     │
     └─── (1:N) ─── [ Reservation ] ─── (N:1) ─── [ Gift ]

### Entidades

users: Credenciais, papel/role (ADMIN, HOST, GUEST) e controle de acesso.

guests: Informações do convidado e limite de acompanhantes (max_companions).

rsvps: Status da confirmação (CONFIRMED, DECLINED), acompanhantes e mensagem.

gifts: Catálogo de presentes, preço, imagem e quantidade disponível.

reservations: Vínculo entre convidado e presente reservado.

🛠️ Tech Stack & Ferramentas
Frontend
Framework: Next.js (TypeScript)

Estilização: Tailwind CSS

Gerenciamento de Estado/HTTP: React Context API / Fetch API / Axios

Backend
Framework: NestJS (TypeScript)

ORM: Prisma ORM

Segurança: Passport-JWT, Bcrypt, Class-Validator, Class-Transformer

Banco de Dados & Infraestrutura
Banco de Dados: PostgreSQL

Containerização: Docker & Docker Compose

Hospedagem (Planejada): Vercel (Frontend), Render/Fly.io (Backend e PostgreSQL)

📁 Estrutura de Pastas
wedding-page/
├── .github/
│   └── ISSUE_TEMPLATE/     # Templates de Issues em Markdown
├── docs/                   # Documentação do banco e arquitetura
├── backend/                # Aplicação NestJS
│   ├── src/
│   ├── prisma/             # Schema do Prisma e Migrations
│   └── .env.example
├── frontend/               # Aplicação Next.js
│   ├── src/
│   └── .env.example
├── docker-compose.yml      # Configuração do PostgreSQL local
└── README.md

🗺️ Roadmap por Milestones
📍 Milestone 1: Fundamentos & Estudos
[ ] Issue 1.1 Estudo de Frontend (React, Next.js App Router, Tailwind CSS)

[ ] Issue 1.2 Estudo de Backend & DB (NestJS, ORM, PostgreSQL, JWT)

📍 Milestone 2: Setup & Banco de Dados
[ ] Issue 2.1 Preparação do ambiente local (Node, Docker, Git, DBeaver)

[ ] Issue 2.2 Estruturação do repositório, Docker Compose e monorepo/pastas

[ ] Issue 2.3 Modelagem Prisma Schema, Migrations e Seeds

📍 Milestone 3: Backend & Regras
[ ] Issue 3.1 Módulo de Autenticação, Tokens (JWT Refresh) e RBAC Guards

[ ] Issue 3.2 Módulo de RSVP (Endpoints, Validações e Regras de Limite)

[ ] Issue 3.3 Módulo de Presentes e Reservas (CRUD e Controle de Estoque)

📍 Milestone 4: Frontend & Interfaces
[ ] Issue 4.1 Layout base, Design System e Páginas Públicas

[ ] Issue 4.2 Contexto de Autenticação, Interceptors e Proteção de Rotas

[ ] Issue 4.3 Formulário do RSVP e Catálogo de Presentes

[ ] Issue 4.4 Dashboard dos Noivos, Tabela de Confirmações e Gestão de Presentes

📍 Milestone 5: Testes & Deploy
[ ] Issue 5.1 Testes unitários/integração, validação responsiva e estados de loading

[ ] Issue 5.2 Provisionamento de Banco Cloud, Deploy da API e publicação na Vercel
