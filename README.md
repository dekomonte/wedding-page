# 💍 Wedding Page

Aplicação web para gerenciamento de um casamento, com área pública para apresentação do evento e área autenticada para **RSVP, acompanhantes, mensagens e lista de presentes**.

O projeto também tem como objetivo aplicar conceitos de desenvolvimento web, incluindo **frontend, backend, banco de dados, autenticação, autorização e regras de negócio**.

---

## 🎯 Funcionalidades

### Área pública

* [ ] Página inicial
* [ ] História do casal
* [ ] Informações do evento
* [ ] Data e horário
* [ ] Localização e mapa
* [ ] Informações úteis

### Autenticação

* [ ] Cadastro de convidados
* [ ] Login e logout
* [ ] Persistência de sessão
* [ ] Access Token
* [ ] Refresh Token
* [ ] Controle de acesso baseado em funções (RBAC)
* [ ] Recuperação de senha

### RSVP

* [ ] Confirmar presença
* [ ] Recusar presença
* [ ] Informar acompanhantes
* [ ] Alterar confirmação
* [ ] Enviar mensagem aos noivos

### Lista de presentes

* [ ] Visualização do catálogo
* [ ] Reserva de presentes
* [ ] Controle de disponibilidade
* [ ] Limite de presentes por convidado
* [ ] Visualização das reservas pelos noivos

### Painel dos noivos

* [ ] Dashboard
* [ ] Lista de convidados
* [ ] Confirmações de presença
* [ ] Acompanhantes
* [ ] Mensagens recebidas
* [ ] Gerenciamento de presentes
* [ ] Visualização das reservas

### Administração

* [ ] Gerenciamento de usuários
* [ ] Gerenciamento de convidados
* [ ] Gerenciamento de presentes
* [ ] Gerenciamento das configurações

---

## 👥 Perfis de acesso

| Perfil            | Acesso                                            |
| ----------------- | ------------------------------------------------- |
| **Administrador** | Acesso total ao sistema                           |
| **Noivos**        | Gestão de convidados, RSVP, mensagens e presentes |
| **Convidado**     | Acesso aos próprios dados, RSVP e reservas        |

A autorização das operações será realizada no **backend** por meio de RBAC.

---

## 📐 Regras de negócio

### RSVP

* Um convidado pode registrar apenas um RSVP ativo.
* O convidado pode confirmar ou recusar sua presença.
* A quantidade de acompanhantes deve respeitar o limite definido pelo sistema.
* O convidado pode atualizar sua confirmação enquanto o RSVP estiver aberto.

### Lista de presentes

* Todos os convidados podem visualizar os presentes disponíveis.
* Apenas usuários autenticados podem realizar reservas.
* Cada convidado possui um limite máximo de reservas.
* Um presente não pode ser reservado por mais de um convidado.
* Uma reserva pode ser cancelada enquanto a lista estiver aberta.
* Os noivos podem visualizar o responsável por cada reserva.

---

## 🏗️ Arquitetura

A aplicação será organizada em três componentes principais:

```text
┌──────────────────────┐
│      Next.js         │
│      Frontend        │
└──────────┬───────────┘
           │
           │ HTTP / REST
           ▼
┌──────────────────────┐
│       NestJS         │
│     Backend / API    │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│     PostgreSQL       │
│       Database       │
└──────────────────────┘
```

O backend será responsável pela **lógica de negócio, autenticação, autorização e acesso aos dados**.

---

## 🗄️ Modelo de dados

Modelo inicial:

```text
User
 │
 └── 1:1 ── Guest
              │
              └── 1:1 ── RSVP
              
User
 │
 └── 1:N ── Reservation ── N:1 ── Gift
```

### Entidades principais

* `users` — autenticação e controle de acesso
* `guests` — informações dos convidados
* `rsvps` — confirmação de presença
* `gifts` — catálogo de presentes
* `reservations` — reservas realizadas pelos convidados

O modelo detalhado do banco será documentado em `docs/database`.

---

## 🔐 Segurança

* Senhas armazenadas utilizando hash seguro.
* Access Token e Refresh Token.
* RBAC implementado no backend.
* Validação dos dados recebidos pela API.
* Variáveis sensíveis armazenadas em `.env`.
* Arquivo `.env` excluído do controle de versão.
* Proteção dos endpoints conforme o perfil de acesso.

---

## 🛠️ Stack

### Frontend

* **Next.js**
* **TypeScript**

### Backend

* **NestJS**
* **TypeScript**

### Database

* **PostgreSQL**

### Ferramentas adicionais

* Docker
* ORM — a definir
* Testes — a definir
* Documentação da API — a definir

---

## 📁 Estrutura do projeto

```text
wedding-page/
│
├── frontend/
│   ├── src/
│   ├── public/
│   └── README.md
│
├── backend/
│   ├── src/
│   ├── test/
│   └── README.md
│
├── docs/
│   ├── architecture/
│   └── database/
│
├── .env.example
├── .gitignore
└── README.md
```

---

## 🗺️ Roadmap

### Planejamento

* [x] Definir stack
* [ ] Definir arquitetura detalhada
* [ ] Modelar banco de dados
* [ ] Especificar regras de negócio
* [ ] Definir API

### Backend

* [ ] Inicializar NestJS
* [ ] Configurar PostgreSQL
* [ ] Implementar entidades
* [ ] Implementar autenticação
* [ ] Implementar RBAC
* [ ] Implementar RSVP
* [ ] Implementar lista de presentes
* [ ] Implementar reservas
* [ ] Implementar testes

### Frontend

* [ ] Inicializar Next.js
* [ ] Criar layout
* [ ] Criar área pública
* [ ] Criar autenticação
* [ ] Criar área do convidado
* [ ] Criar RSVP
* [ ] Criar lista de presentes
* [ ] Criar painel dos noivos
* [ ] Criar painel administrativo

### Deploy

* [ ] Configurar ambiente de produção
* [ ] Configurar banco de dados
* [ ] Configurar variáveis de ambiente
* [ ] Publicar backend
* [ ] Publicar frontend
* [ ] Configurar domínio
* [ ] Realizar testes em produção

---

## 📌 Status

**Em planejamento.**
