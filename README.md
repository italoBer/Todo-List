# 📝 Todo List API

API REST de gerenciamento de tarefas desenvolvida em **Java** com **Spring Boot**, criada durante o curso introdutório de Java da [Rocketseat](https://www.rocketseat.com.br/).

O projeto implementa um CRUD de tarefas com autenticação de usuários via **Basic Auth**, senhas criptografadas com **BCrypt** e deploy feito no **Render** com **Docker**.

## 🚀 Tecnologias

- Java 17
- Spring Boot
- Spring Data JPA
- H2 Database (banco em memória)
- Lombok
- BCrypt (hash de senhas)
- Maven
- Docker

## ⚙️ Funcionalidades

- ✅ Cadastro de usuários com senha criptografada (BCrypt)
- ✅ Criação de tarefas com título, descrição, prioridade e período (início/fim)
- ✅ Listagem de tarefas do usuário autenticado
- ✅ Atualização parcial de tarefas (apenas os campos enviados são alterados)
- ✅ Autenticação via Basic Auth em um filtro customizado (`OncePerRequestFilter`)
- ✅ Validações de regra de negócio:
  - Título com no máximo 50 caracteres
  - Datas de início/término não podem ser anteriores à data atual
  - Data de início deve ser anterior à data de término
  - Usuário só pode alterar as próprias tarefas
- ✅ Tratamento global de exceções com `@ControllerAdvice`

## 🏗️ Estrutura do projeto

```
src/main/java/br/com/italoBer/todolist
├── user/       # Entidade, repositório e controller de usuários
├── task/       # Entidade, repositório e controller de tarefas
├── filter/     # Filtro de autenticação (Basic Auth)
├── errors/     # Handler global de exceções
└── utils/      # Utilitário para atualização parcial (copyNonNullProperties)
```

## 📡 Endpoints

### Usuários

| Método | Rota      | Descrição            | Autenticação |
|--------|-----------|----------------------|--------------|
| POST   | `/users/` | Cria um novo usuário | Não          |

**Corpo da requisição:**

```json
{
  "username": "italo",
  "name": "Italo Bernardo",
  "password": "123456"
}
```

### Tarefas

Todas as rotas de tarefas exigem **Basic Auth** (username e password do usuário cadastrado).

| Método | Rota          | Descrição                              |
|--------|---------------|----------------------------------------|
| POST   | `/tasks/`     | Cria uma nova tarefa                   |
| GET    | `/tasks/`     | Lista as tarefas do usuário autenticado |
| PUT    | `/tasks/{id}` | Atualiza uma tarefa (parcial)          |

**Corpo da requisição (criação):**

```json
{
  "title": "Estudar Spring Boot",
  "description": "Revisar camadas da aplicação",
  "priority": "ALTA",
  "startAt": "2026-08-01T10:00:00",
  "endAt": "2026-08-01T12:00:00"
}
```

## ▶️ Como executar localmente

Pré-requisitos: **Java 17** e **Maven** (ou use o Maven Wrapper incluso).

```bash
# Clonar o repositório
git clone https://github.com/ItaloBer/todolist.git
cd todolist

# Executar a aplicação
./mvnw spring-boot:run
```

A API ficará disponível em `http://localhost:8080`.

O console do H2 fica disponível em `http://localhost:8080/h2-console` (JDBC URL: `jdbc:h2:mem:todolist`, usuário: `admin`, senha: `admin`).

## 🐳 Executando com Docker

```bash
docker build -t todolist .
docker run -p 8080:8080 todolist
```

## ☁️ Deploy

A aplicação está no ar através do **Render**: [acesse aqui](https://SEU-LINK-DO-RENDER.onrender.com)

> ⚠️ Como o banco H2 é em memória, os dados são apagados a cada reinício da aplicação.

## 📚 O que aprendi

- Como as camadas de uma aplicação Spring Boot se conectam (Controller, Repository, Entity)
- Criação de uma API REST completa com CRUD
- Autenticação com filtros e criptografia de senhas com BCrypt
- Tratamento de exceções com `@ControllerAdvice`
- Deploy de uma aplicação Java com Docker no Render

---

Feito com por [Italo Bernardo](https://www.linkedin.com/in/italo-bernardo)
