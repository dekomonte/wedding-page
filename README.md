# 💍 Wedding Page

Aplicação web para o site de um casamento, com área pública para apresentação do evento e área autenticada para gerenciamento de convidados, confirmação de presença e lista de presentes.

O projeto tem como objetivo servir como aplicação prática para estudo e desenvolvimento de uma arquitetura web completa, envolvendo **frontend, backend, banco de dados, autenticação, autorização e regras de negócio**.

---

## 🎯 Objetivos

* Criar uma página personalizada para um casamento.
* Permitir que convidados confirmem presença.
* Permitir o gerenciamento de acompanhantes.
* Disponibilizar uma lista de presentes com controle de reservas.
* Permitir que os noivos acompanhem confirmações, acompanhantes, mensagens e presentes escolhidos.
* Implementar autenticação e autorização com diferentes níveis de acesso.
* Desenvolver uma arquitetura organizada e preparada para futuras expansões.

---

## 👥 Perfis de Usuário

O sistema terá três níveis de acesso:

### Administrador
Acesso total ao sistema.

* Gerenciar usuários;
* Gerenciar convidados;
* Gerenciar noivos;
* Gerenciar presentes;
* Alterar configurações do sistema;
* Visualizar todas as informações.

### Noivos
Acesso à área de gestão do casamento.

* Visualizar o total de convidados;
* Visualizar confirmações de presença;
* Visualizar acompanhantes;
* Visualizar mensagens recebidas;
* Gerenciar a lista de presentes;
* Visualizar quais convidados reservaram cada presente.

### Convidado
Acesso limitado à área autenticada.

* Criar uma conta;
* Fazer login;
* Confirmar ou recusar presença;
* Informar acompanhantes;
* Enviar mensagem aos noivos;
* Visualizar a lista de presentes;
* Reservar presentes respeitando o limite definido pelo sistema.

---

# 📋 Funcionalidades

## 1. Área Pública

* [ ] Página inicial
* [ ] História do casal
* [ ] Informações sobre o casamento
* [ ] Data e horário do evento
* [ ] Localização e mapa
* [ ] Informações úteis para os convidados
* [ ] Acesso à área de login/cadastro

## 2. Autenticação

* [ ] Cadastro de convidados
* [ ] Login
* [ ] Logout
* [ ] Hash seguro de senhas
* [ ] Access Token
* [ ] Refresh Token
* [ ] Persistência da sessão
* [ ] Controle de acesso baseado em perfil (RBAC)
* [ ] Recuperação de senha *(futuro)*

## 3. RSVP — Confirmação de Presença

Cada convidado autenticado poderá registrar sua presença.

* [ ] Confirmar presença
* [ ] Recusar presença
* [ ] Informar quantidade de acompanhantes
* [ ] Alterar confirmação
* [ ] Enviar mensagem aos noivos
* [ ] Visualizar o próprio status de confirmação

### Informações registradas

* Convidado
* Status da confirmação
* Quantidade de acompanhantes
* Mensagem
* Data da confirmação

---

## 4. Lista de Presentes

A aplicação disponibilizará um catálogo de presentes.

Cada presente poderá possuir:

* Nome;
* Descrição;
* Preço;
* Imagem;
* Status de disponibilidade.

### Regras de negócio

* [ ] Todos os convidados podem visualizar a lista completa.
* [ ] Apenas convidados autenticados podem reservar presentes.
* [ ] Cada convidado possui um limite máximo de presentes que pode reservar.
* [ ] Um presente reservado não pode ser reservado novamente.
* [ ] O sistema deve atualizar automaticamente a disponibilidade.
* [ ] Os noivos podem visualizar quem reservou cada presente.
* [ ] Administradores podem gerenciar todos os presentes.

> **Exemplo:** se o limite for `N = 3`, um convidado poderá reservar no máximo três presentes.

---

## 5. Painel dos Noivos

Dashboard para acompanhamento do evento.

### Indicadores

* [ ] Total de convidados
* [ ] Total de confirmações
* [ ] Total de recusas
* [ ] Total de acompanhantes
* [ ] Total de presentes reservados
* [ ] Presentes disponíveis

### Gestão

* [ ] Listar convidados
* [ ] Consultar confirmação de presença
* [ ] Consultar acompanhantes
* [ ] Visualizar mensagens
* [ ] Gerenciar presentes
* [ ] Visualizar responsável por cada reserva

---

# 🗄️ Modelo de Dados

O modelo inicial será organizado em torno de **usuários, convidados, RSVP e presentes**.

### `users`

Responsável pela autenticação e autorização.

| Campo        | Descrição                        |
| ------------ | -------------------------------- |
| `id`         | Identificador                    |
| `nome`       | Nome do usuário                  |
| `email`      | E-mail                           |
| `senha_hash` | Senha armazenada com hash        |
| `perfil`     | `admin`, `noivos` ou `convidado` |
| `created_at` | Data de criação                  |
| `updated_at` | Data de atualização              |

### `convidados`

Informações específicas relacionadas à participação no casamento.

| Campo               | Descrição                   |
| ------------------- | --------------------------- |
| `id`                | Identificador               |
| `usuario_id`        | Usuário relacionado         |
| `confirmado`        | Status do RSVP              |
| `qtd_acompanhantes` | Quantidade de acompanhantes |
| `mensagem`          | Mensagem enviada aos noivos |
| `created_at`        | Data de criação             |
| `updated_at`        | Data de atualização         |

### `presentes`

Catálogo de presentes.

| Campo           | Descrição                      |
| --------------- | ------------------------------ |
| `id`            | Identificador                  |
| `nome`          | Nome do presente               |
| `descricao`     | Descrição                      |
| `preco`         | Valor                          |
| `imagem_url`    | URL da imagem                  |
| `status`        | `disponivel` ou `reservado`    |
| `reservado_por` | Usuário que realizou a reserva |
| `created_at`    | Data de criação                |
| `updated_at`    | Data de atualização            |

### Relacionamentos

```text
User
 ├── 1:1 ── Convidado
 │            └── RSVP
 │
 └── 1:N ── Reservas ── N:1 ── Presente
```

> A modelagem poderá ser refinada durante o desenvolvimento, principalmente a relação entre convidados, acompanhantes e reservas.

---

# 🔐 Segurança

O projeto deverá seguir boas práticas básicas de segurança.

* Senhas armazenadas exclusivamente como hash;
* Uso de **bcrypt ou Argon2**;
* Access Token com tempo de vida reduzido;
* Refresh Token para renovação da sessão;
* Controle de autorização no backend;
* Variáveis sensíveis armazenadas em `.env`;
* `.env` incluído no `.gitignore`;
* Validação dos dados recebidos pela API;
* Proteção dos endpoints de acordo com o perfil do usuário.

> A autorização deve ser validada no **backend**. Ocultar funcionalidades no frontend não é suficiente para proteger um recurso.

---

# 🏗️ Arquitetura

A aplicação será estruturada inicialmente seguindo uma arquitetura desacoplada:

```text
                    ┌─────────────────┐
                    │    Frontend     │
                    │ React / Next.js │
                    └────────┬────────┘
                             │
                             │ HTTP / REST
                             ▼
                    ┌─────────────────┐
                    │     Backend     │
                    │   API REST      │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │    Database     │
                    │ PostgreSQL/etc. │
                    └─────────────────┘
```

Essa separação permite desenvolver e substituir as camadas de forma independente.

---

# 🛠️ Tecnologias

## Backend

**Definida: NestJS**

Opções consideradas:

* Spring Boot
* FastAPI
* NestJS
* Lumen

## Frontend

**Definida: Next.js**

Opções consideradas:

* React
* Next.js
* Vite
* Vue.js

## Banco de Dados

**Definida: PostgreSQL**

Opções consideradas:

* PostgreSQL
* MySQL
* MongoDB

---

# 📁 Estrutura prevista

```text
wedding-page/
│
├── backend/
│   ├── src/
│   ├── tests/
│   └── README.md
│
├── frontend/
│   ├── src/
│   ├── public/
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

A estrutura definitiva será definida após a escolha das tecnologias.

---

# 🗺️ Roadmap

## Fase 1 — Planejamento

* [ ] Definir stack
* [ ] Definir arquitetura
* [ ] Refinar modelo de dados
* [ ] Definir regras de negócio
* [ ] Definir endpoints da API

## Fase 2 — Backend

* [ ] Configurar projeto
* [ ] Configurar banco de dados
* [ ] Criar entidades
* [ ] Implementar autenticação
* [ ] Implementar RBAC
* [ ] Implementar CRUDs
* [ ] Implementar RSVP
* [ ] Implementar lista de presentes
* [ ] Criar testes

## Fase 3 — Frontend

* [ ] Criar layout
* [ ] Criar página inicial
* [ ] Criar login/cadastro
* [ ] Criar área do convidado
* [ ] Criar RSVP
* [ ] Criar lista de presentes
* [ ] Criar painel dos noivos
* [ ] Criar painel administrativo

## Fase 4 — Integração

* [ ] Integrar frontend e API
* [ ] Implementar tratamento de erros
* [ ] Validar regras de autorização
* [ ] Testar fluxo completo
* [ ] Revisar segurança

## Fase 5 — Deploy

* [ ] Configurar ambiente de produção
* [ ] Configurar banco de produção
* [ ] Configurar variáveis de ambiente
* [ ] Publicar backend
* [ ] Publicar frontend
* [ ] Configurar domínio
* [ ] Testar aplicação em produção

---

# 📌 Status

**Em planejamento.**

A próxima etapa é definir a stack tecnológica e transformar os requisitos em uma especificação técnica inicial.
