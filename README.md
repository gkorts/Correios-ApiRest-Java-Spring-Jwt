# Spring-Security-Correios

Sistema de registro e listagem de usuários, autenticação JWT, controle de acesso por roles (administrador e usuário comum) e gerenciamento básico de correios (criar, excluir e listar correspondências), tudo protegido por Spring Security e utilizando MongoDB como armazenamento.

---

## Funcionalidades

* **Inicialização de roles e admin**: Insere papéis `ADMIN` e `BASIC` e cria um usuário administrador padrão.
* **Cadastro de usuário**: Criação de novos usuários com criptografia de senha.
* **Autenticação JWT**: Emissão e validação de tokens JWT (acesso e escopos).
* **Gerenciamento de correspondências**: Criação, listagem paginada e exclusão de correspondências.
* **Controle de acesso**:
  * Rota **`/users`** para listagem de usuários restrita a administradores.
  * Exclusão de correspondências permitida apenas ao remetente ou a administradores.

---

## Endpoints

| Método | Rota | Descrição | Acesso |
|---|---|---|---|
| POST | `/users` | Cadastra novo usuário | Público |
| GET | `/users` | Lista todos os usuários | ADMIN |
| POST | `/login` | Autentica usuário e retorna token JWT | Público |
| POST | `/correios` | Cria uma nova correspondência | Autenticado |
| DELETE | `/correios/{id}` | Exclui uma correspondência (remetente ou ADMIN) | Autenticado |
| GET | `/correios/feed` | Retorna a listagem paginada de correspondências | Autenticado |

---

## Tecnologias

* Java 24
* Spring Boot 3.5.3
* Spring Security (JWT, OAuth2 Resource Server)
* Spring Data MongoDB
* Nimbus JOSE + JWT
* BCryptPasswordEncoder
* JUnit
* Mockito

---

## Pré-requisitos

* Java 24
* Maven
* MongoDB rodando em `mongodb://localhost:27017/teste`

---

## Configuração

No arquivo `src/main/resources/application.properties`, defina:

```properties
spring.application.name=Security

spring.data.mongodb.uri=mongodb://localhost:27017/teste
spring.data.mongodb.auto-index-creation=true

jwt.public.key=classpath:app.pub
jwt.private.key=classpath:app.key
```

No `pom.xml`, confira:

```xml
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-parent</artifactId>
  <version>3.5.3</version>
</parent>
<properties>
  <java.version>24</java.version>
</properties>
```

Coloque suas chaves RSA nos arquivos `app.pub` e `app.key` em `src/main/resources`.

---

## Execução

Para compilar e iniciar a aplicação:

```bash
mvn clean spring-boot:run
```

A API será iniciada em `http://localhost:8080`.

---

## Testes

Os testes unitários utilizam **JUnit** e **Mockito**. Para executá-los:

```bash
mvn test
```

---

*Desenvolvido como projeto de demonstração de gerenciamento de correspondências, utilizando Spring Security, JWT e MongoDB.*
