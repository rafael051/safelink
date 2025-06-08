# 🛡️ SafeLink - Sistema Inteligente de Monitoramento de Riscos Naturais
## 📄 Descrição do Projeto
O SafeLink é um sistema inteligente para monitoramento, prevenção e resposta a eventos extremos da natureza, voltado para alertas, ocorrências, regiões de risco e relatos dos usuários. Projeto desenvolvido no Challenge 2025/1 (FIAP).
## 👨‍💻 Integrantes
- Rafael Rodrigues de Almeida - RM: 557837
- Lucas Kenji Miyahira - RM: 555368
## 🚀 Tecnologias Utilizadas
- Java 17
- Spring Boot 3.x
- Spring Data JPA
- Spring Security (JWT)
- ModelMapper
- PostgreSQL (Railway ou local)/Oracle (opcional)
- Redis (opcional)
- Docker
- Swagger OpenAPI
## ✅ Passo a Passo: Publicação Docker Hub
### 1) Login no Docker Hub
```bash
docker login
```
### 2) Gerar JAR
```bash
./mvnw clean package -DskipTests
```
### 3) Build da imagem Docker
```bash
docker build -t <seu-usuario>/safelink:latest .
```
### 4) Push Docker Hub
```bash
docker push <seu-usuario>/safelink:latest
```
## 🐘 Banco PostgreSQL Railway
- Crie projeto PostgreSQL no Railway (https://railway.app)
- Copie URL gerada e configure o `application.properties`
```properties
spring.datasource.url=jdbc:postgresql://<host>:<port>/<database>
spring.datasource.username=<usuario>
spring.datasource.password=<senha>
spring.datasource.driver-class-name=org.postgresql.Driver
```
## 🧩 Funcionalidades Principais
- Autenticação usuários (JWT)
- Cadastro e consulta alertas risco
- Monitoramento eventos naturais
- Relatos ocorrências usuários
- Gestão regiões monitoradas
- Consulta paginada e filtros dinâmicos
- Documentação automática Swagger
## 🛠️ Executar Localmente
1. Clone repositório:
```bash
git clone https://github.com/rafael051/safelink.git
cd safelink
```
2. Configure banco PostgreSQL (Railway ou local)
3. Ajuste `application.properties`
4. Execute aplicação:
```bash
./mvnw spring-boot:run
```
Ou Docker:
```bash
docker build -t safelink .
docker run -p 8080:8080 safelink
```
5. Documentação Swagger: http://localhost:8080/swagger-ui.html
## 📚 Estrutura das Pastas
```
safelink/
├─src/
│ ├─main/
│ │ ├─java/br/com/fiap/safelink/
│ │ │ ├─controller/
│ │ │ ├─dto/request/
│ │ │ ├─dto/response/
│ │ │ ├─exception/
│ │ │ ├─filter/
│ │ │ ├─model/
│ │ │ ├─repository/
│ │ │ ├─service/
│ │ │ └─config/
│ │ └─resources/
│ │   ├─application.properties
│ │   └─...
├─Dockerfile
└─README.md
```
## 🔒 Autenticação JWT
Todos endpoints (exceto login) exigem autenticação JWT. Use endpoint `/auth/login` para obter token.
## 👀 Exemplos Endpoints
## 🔁 Endpoints POST
```
### Cadastrar Usuario
```http
POST /users
Content-Type: application/json
{
  "email": "usuario@safelink.com",
  "password": "s3nh@F0rte",
  "role": "ADMIN"
}
```
### Autenticar
```http
POST /login
Content-Type: application/json
{
  "email": "admin@safelink.com",
  "password": "admin123"
}
```
### Cadastrar Região
```http
POST /regioes
Authorization: Bearer <token>
Content-Type: application/json
{
  "nome": "Zona Norte",
  "cidade": "São Paulo",
  "estado": "SP",
  "latitude": -23.5365,
  "longitude": -46.6333
}
```
### Cadastrar Alerta
```http
POST /alertas
Authorization: Bearer <token>
Content-Type: application/json
{
  "tipo": "Enchente",
  "nivelRisco": "ALTO",
  "mensagem": "Evacuar imediatamente a área afetada pela enchente",
  "emitidoEm": "08/06/2025 14:00:00",
  "idRegiao": 1
}
```
### Cadastrar Evento Natural
```http
POST /eventos-naturais
Authorization: Bearer <token>
Content-Type: application/json
{
  "tipo": "Deslizamento",
  "descricao": "Deslizamento de terra após fortes chuvas",
  "dataOcorrencia": "08/06/2025 14:00:00",
  "regiaoId": 1
}
```
### Registrar Previsão de Risco
```http
POST /previsoes-risco
Authorization: Bearer <token>
Content-Type: application/json
{
  "nivelPrevisto": "MÉDIO",
  "fonte": "INMET",
  "geradoEm": "08/06/2025 14:00:00",
  "regiaoId": 1
}
```
### Criar Relato de Usuário
```http
POST /relatos-usuarios
Authorization: Bearer <token>
Content-Type: application/json
{
  "mensagem": "Há deslizamento parcial na encosta próxima à escola municipal.",
  "dataRelato": "08/06/2025 14:00:00",
  "regiaoId": 1
}
```
## 📝 Licença
Projeto acadêmico — sem fins lucrativos.
## ✉️ Contato
- rm557837@fiap.com.br
- rm555368@fiap.com.br
