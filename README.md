# Aula Salvar Para Muitos (Many-to-Many)

Projeto desenvolvido durante os estudos de Spring Boot e JPA com foco no relacionamento **Many-to-Many** entre entidades.

## Tecnologias Utilizadas

* Java 21
* Spring Boot
* Spring Data JPA
* Hibernate
* Maven
* Banco de Dados H2
* REST API
* Git e GitHub

---

## Objetivo

Implementar uma API REST para cadastro de produtos e categorias utilizando relacionamento **Many-to-Many**, permitindo que:

* Um produto pertença a várias categorias.
* Uma categoria possua vários produtos.

---

## Estrutura do Projeto

### Entidades

#### Product

```java
@ManyToMany
@JoinTable(
    name = "tb_product_category",
    joinColumns = @JoinColumn(name = "product_id"),
    inverseJoinColumns = @JoinColumn(name = "category_id")
)
private Set<Category> categories = new HashSet<>();
```

#### Category

```java
@ManyToMany(mappedBy = "categories")
private Set<Product> products = new HashSet<>();
```

---

## Arquitetura

```text
Controller
    ↓
DTO
    ↓
Service
    ↓
Repository
    ↓
Database
```

---

## Funcionalidades

### Inserir Produto

**POST**

```http
POST /products
```

### Exemplo de Requisição

```json
{
  "name": "Notebook Dell",
  "price": 4500.0,
  "categories": [
    {
      "id": 3
    }
  ]
}
```

### Exemplo de Resposta

```json
{
  "id": 5,
  "name": "Notebook Dell",
  "price": 4500.0,
  "categories": [
    {
      "id": 3,
      "name": "Computadores"
    }
  ]
}
```

---

## DTOs

Foram implementados:

* ProductDTO
* CategoryDTO

Responsáveis por:

* Receber dados da API
* Retornar dados ao cliente
* Evitar exposição direta das entidades

---

## Service Layer

A camada de serviço foi utilizada para:

* Converter DTO em Entity
* Associar categorias ao produto
* Persistir os dados utilizando JPA
* Converter Entity em DTO para resposta

---

## Banco de Dados H2

A aplicação utiliza banco em memória para fins de estudo.

### Console H2

```http
http://localhost:8080/h2-console
```

### Configurações

```text
JDBC URL: jdbc:h2:mem:testdb
User: sa
Password:
```

---

## Principais Conceitos Praticados

* Spring Boot
* Spring Data JPA
* Hibernate
* REST API
* DTO Pattern
* Service Layer
* Repository Pattern
* Many-to-Many
* @ManyToMany
* @JoinTable
* @JoinColumn
* Conversão Entity ↔ DTO
* Persistência de relacionamentos

---

## Aprendizados Durante o Desenvolvimento

Durante a implementação foram resolvidos diversos desafios:

* Configuração do Java 21
* Configuração do Maven Wrapper
* Ajustes de SDK no IntelliJ IDEA
* Correção de conflitos de versão Java
* Resolução de conflitos de porta 8080
* Correção de erros de serialização/deserialização do Jackson
* Implementação de DTOs com construtores vazios e setters
* Publicação do projeto no GitHub

---

## Executando o Projeto

Clone o repositório:

```bash
git clone https://github.com/MarcelFinavaro/aula-salvar-para-muitos.git
```

Entre na pasta:

```bash
cd aula-salvar-para-muitos
```

Execute:

```bash
./mvnw spring-boot:run
```

Ou execute a classe:

```java
AulaApplication
```

---

## Autor

**Marcel Fernando Finavaro**

* Desenvolvedor Java
* Estudante de Spring Boot e JPA
* Especialista em soluções digitais e automação

GitHub:
https://github.com/MarcelFinavaro
