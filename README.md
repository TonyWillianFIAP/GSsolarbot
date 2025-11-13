# ☀️ SolarBot Energy Monitor

O **SolarBot** é um sistema inteligente integrado a um robô com câmera, projetado para **monitorar e mapear usinas solares**.  
O sistema coleta informações sobre o **estado de conservação**, **quantidade de placas**, **layout da instalação**, **leituras de energia** e outros dados importantes.

Ele foi desenvolvido em **Java com Spring Boot**, usando **arquitetura modular e autenticação JWT**, e se conecta a um **banco de dados Oracle** para armazenar e gerenciar informações sobre as usinas e usuários.

Desenvolvido por:

Henrique Parra - RM551973
Roberto Oliveira - RM551460
Tony Willian - RM550667

---

## 🧠 Funcionalidades

- 📡 Monitoramento automatizado de usinas solares  
- 🔐 Autenticação e autorização via **Spring Security + JWT**  
- ⚙️ API REST modular com serviços independentes  
- 🧾 Tratamento global de exceções (`@ControllerAdvice`)  
- 🧰 Estrutura completa com Entities, DTOs, Controllers e Services  

---

## 🧰 Tecnologias utilizadas

| Categoria | Tecnologia |
|------------|-------------|
| Linguagem | Java 17+ |
| Framework principal | Spring Boot 3.x |
| Banco de Dados | Oracle Database |
| ORM | Spring Data JPA |
| Autenticação | Spring Security + JWT (JJWT 0.11.5) |
| IDE recomendada | IntelliJ IDEA Community Edition |
| Build tool | Maven |

---

## 🚀 Como executar o projeto (para iniciantes)

> Este guia assume **zero configurações prévias** — você só precisa ter Java e Git instalados.

---

### 🪜 1. Pré-requisitos

Antes de começar, instale:

- **Java 17 ou superior** → [Download JDK 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)
- **Git** → [Download Git](https://git-scm.com/downloads)
- **IntelliJ IDEA Community Edition** → [Download IntelliJ](https://www.jetbrains.com/idea/download/)
- **Oracle Database Express Edition (XE)** → [Download Oracle XE](https://www.oracle.com/database/technologies/appdev/xe.html)

---

### ⚙️ 2. Clonar o repositório

Abra o terminal e digite:

```bash
git clone https://github.com/SEU-USUARIO/solarbot-energy-monitor.git
cd solarbot-energy-monitor
```

> Substitua `SEU-USUARIO` pelo seu nome de usuário do GitHub.

---

### 🧩 3. Abrir no IntelliJ

1. Abra o **IntelliJ IDEA Community**  
2. Clique em **File → Open...**  
3. Selecione a pasta do projeto (`solarbot-energy-monitor`)  
4. O IntelliJ detectará o `pom.xml` e importará o projeto Maven automaticamente.  
   Se aparecer uma mensagem, clique em **“Load Maven Project”**.

---

### 🧱 4. Configurar o banco de dados Oracle

1. Instale e inicie o **Oracle XE**  
2. Abra o **SQL Developer** ou o terminal do Oracle e crie o banco:

```sql
CREATE USER solarbot IDENTIFIED BY solar123;
GRANT CONNECT, RESOURCE TO solarbot;
```

3. No projeto, edite o arquivo `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:oracle:thin:@localhost:1521:XE
spring.datasource.username=solarbot
spring.datasource.password=solar123
spring.datasource.driver-class-name=oracle.jdbc.OracleDriver

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

---

### 🔐 5. Dependências principais do Maven

O arquivo `pom.xml` contém todas as dependências necessárias:

```xml
<dependencies>
    <!-- Spring Boot básico -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- Banco de dados Oracle -->
    <dependency>
        <groupId>com.oracle.database.jdbc</groupId>
        <artifactId>ojdbc11</artifactId>
        <version>23.3.0.23.09</version>
    </dependency>

    <!-- Spring Data JPA -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>

    <!-- Spring Security -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>

    <!-- JWT (JSON Web Token) -->
    <dependency>
        <groupId>io.jsonwebtoken</groupId>
        <artifactId>jjwt-api</artifactId>
        <version>0.11.5</version>
    </dependency>
    <dependency>
        <groupId>io.jsonwebtoken</groupId>
        <artifactId>jjwt-impl</artifactId>
        <version>0.11.5</version>
        <scope>runtime</scope>
    </dependency>
    <dependency>
        <groupId>io.jsonwebtoken</groupId>
        <artifactId>jjwt-jackson</artifactId>
        <version>0.11.5</version>
        <scope>runtime</scope>
    </dependency>

    <!-- Validações -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-validation</artifactId>
    </dependency>

    <!-- Testes -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

Após editar, clique em **“Load Maven Changes”** 🐘 no IntelliJ.

---

### ▶️ 6. Executar o projeto

No IntelliJ:
- Vá até a classe principal (geralmente `SolarbotApplication.java`)
- Clique no botão **▶️ Run**

Ou, via terminal:

```bash
mvn spring-boot:run
```

Se tudo estiver certo, aparecerá:

```
Tomcat started on port(s): 8080
Started SolarbotApplication in X seconds
```

---

### 🧪 7. Testar a API

Abra o navegador ou o Postman e acesse:

```
http://localhost:8080/api/auth/login
```

Você pode testar as rotas públicas e protegidas.  
As rotas protegidas exigem **Bearer Token JWT**, que você obtém após fazer login.

---

## 🧠 Estrutura do projeto

```
src/
 └── main/
      ├── java/com/solarbot/
      │    ├── auth/
      │    │    ├── controller/
      │    │    ├── dto/
      │    │    ├── model/
      │    │    ├── repository/
      │    │    ├── service/
      │    │    │    └── UserDetailsServiceImpl.java
      │    │    └── config/
      │    │         └── SecurityConfig.java
      │    ├── solar/
      │    │    ├── controller/
      │    │    ├── service/
      │    │    └── model/
      │    └── SolarbotApplication.java
      └── resources/
           ├── application.properties
           └── data.sql
```

---

**Desenvolvido por estudantes de Engenharia de Software — Projeto SolarBot 🌞**
