# wedding-page-python-flask
Projeto pessoal de página de casamento 

## Requisitos Técnicos

* Backend: API (SpringBot, FastAPI, Nest.js, Lumen)
* Frontend: React (Next.js, Vite, Vue.js)
* Banco de Dados: MySQL, Postgre, MongoDB

* Requisitos não funcionais do Lucas: CRUD básico com login, persistência de sessão, refesh token, permissionamento de usuários, três tipos de usuario adm acesso total, noivos acesso parcial, convidados parcial; convidados devem fazer cadastro para ter acesso, fazer algo escalável; convidados podem ver a lista de presente completa mas ele só pode escolher um número tal de presentes e o casal pode ver de todo mundo e quem confirmou.

# Requisitos funcionais

1. Gestão de Usuários & Permissões (RBAC)
O sistema deve suportar 3 perfis de acesso:

Administrador (Acesso Total): Gerencia todos os dados do sistema, usuários, noivos e configurações.

Noivos (Acesso de Gestão): Acessam o painel administrativo para visualizar o total de confirmados, lista de acompanhantes, mensagens recebidas e relatórios da lista de presentes.

Convidado (Acesso Limitado): Precisa criar uma conta/login para interagir com o site. Pode confirmar presença, enviar mensagens e selecionar um número limite de presentes.

## Regras de Negócio

#### Área Pública

- [ ] História do casal
- [ ] Confirmação de presença
- [ ] Lista de presentes
- [ ] Mapa do local

#### Administração

- [ ] Tela de login
- [ ] Painel de gestão de convidados

## Modelagem do Banco de Dados

* Tabela Convidados: id, nome_completo, email, confirmado (booleano), qtd_acompanhantes, mensagem
* Tabela Presentes: id, nome_item, preco, imagem_url, status (disponível/reservado), comprado_por
* Tabela Admin/User: id, username, password_hash

## Segurança
* Usar hash para salvar senhas no banco
* Configuração de .env 




# 💍 Site de Casamento & Gestão de RSVP

Aplicação web para apresentação do evento de casamento, confirmação de presença (RSVP), lista controlada de presentes e painel de gestão para os noivos com múltiplos níveis de acesso.

---

## 🎯 Requisitos Funcionais

### 1. Gestão de Usuários & Permissões (RBAC)
O sistema deve suportar 3 perfis de acesso:
* **Administrador (Acesso Total):** Gerencia todos os dados do sistema, usuários, noivos e configurações.
* **Noivos (Acesso de Gestão):** Acessam o painel administrativo para visualizar o total de confirmados, lista de acompanhantes, mensagens recebidas e relatórios da lista de presentes.
* **Convidado (Acesso Limitado):** Precisa criar uma conta/login para interagir com o site. Pode confirmar presença, enviar mensagens e selecionar um número limite de presentes.

### 2. Regras de Negócio por Módulo

#### Área Pública / Institucional
- [ ] Exibição da história do casal
- [ ] Localização com mapa e informações do evento

#### Módulo de Confirmação de Presença (RSVP)
- [ ] O convidado informa se vai ao evento, a quantidade de acompanhantes e uma mensagem para os noivos

#### Módulo de Lista de Presentes
- [ ] Exibição do catálogo completo de presentes
- [ ] **Regra de Trava:** Cada convidado autenticado só pode escolher/reservar um número máximo limite $N$ de presentes
- [ ] Atualização automática de status do presente (`disponível` / `reservado`)

#### Painel Administrativo
- [ ] Dashboard com métricas gerais (total de convidados, confirmados, presentes reservados)
- [ ] Lista detalhada de quem confirmou presença e quem escolheu cada presente

---

## 🔐 Requisitos Não-Funcionais & Segurança

* **Autenticação Robusta:** Autenticação via tokens com suporte a *Access Token* (curta duração) e *Refresh Token* (renovação de sessão).
* **Segurança de Credenciais:** As senhas devem obrigatoriamente ser armazenadas utilizando algoritmos de hash seguros (ex: bcrypt/argon2).
* **Variáveis de Ambiente:** Configurações sensíveis (chaves de criptografia, URLs de banco) devem ser isoladas em arquivo `.env`.
* **Escalabilidade:** Arquitetura desacoplada para permitir fácil expansão ou troca de banco de dados e front-end no futuro.

---

## 🗄️ Modelo de Dados Unificado (Conceitual)

* **Usuário (`users`):** `id`, `nome`, `email`, `senha_hash`, `perfil` (`admin`, `noivos`, `convidado`)
* **RSVP / Convidado (`convidados`):** `id`, `usuario_id`, `confirmado`, `qtd_acompanhantes`, `mensagem`
* **Presentes (`presentes`):** `id`, `nome_item`, `preco`, `imagem_url`, `status`, `reservado_por_usuario_id`

---

## 🛠️ Tecnologias (A definir)

- **Back-end:** TBD
- **Front-end:** TBD
- **Banco de Dados:** TBD
