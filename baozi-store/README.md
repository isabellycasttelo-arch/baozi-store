# Baozi Store – API REST

API REST simples para controle de clientes, produtos e pedidos da Baozi Store (pãozinho chinês).
Tecnologias: Java 17, Spring Boot 3, Spring Data JPA, H2 / MySQL, Postman.

## Como executar
Requisitos: JDK 17+ e Maven (ou use a IDE: IntelliJ / Eclipse / VS Code).

```bash
mvn spring-boot:run
```
A API sobe em `http://localhost:8080`.

### Banco de dados
- **Padrão (H2, arquivo local):** não precisa instalar nada. Console: `http://localhost:8080/h2-console`
  (JDBC URL: `jdbc:h2:file:./data/baozidb`, usuário `sa`, senha em branco).
- **MySQL:** crie o banco `CREATE DATABASE baozi_store;`, ajuste a senha em
  `application-mysql.properties` e rode `mvn spring-boot:run -Dspring-boot.run.profiles=mysql`.

## Endpoints
| Método | Rota | Descrição |
|---|---|---|
| POST | /clientes, /produtos, /pedidos | Criar |
| GET | /clientes, /produtos, /pedidos | Listar todos |
| GET | /{entidade}/{id} | Consultar por ID |
| PUT | /{entidade}/{id} | Atualizar (opcional) |
| DELETE | /{entidade}/{id} | Apagar |

### Exemplos de corpo (JSON)
```json
// POST /clientes
{ "nome": "SeuNome123456", "clienteDesde": "2026-10-11" }

// POST /produtos
{ "nome": "Baozi de Carne", "preco": 8.50, "estoque": true }

// POST /pedidos
{ "cliente": { "id": 1 }, "produto": { "id": 1 }, "quantidade": 5 }
```

## Estrutura
```
src/main/java/com/baozistore
├── model        (Cliente, Produto, Pedido)
├── repository   (JpaRepository de cada entidade)
└── controller   (endpoints REST + tratamento de erros)
```
