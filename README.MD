ATTUS TESTE DEVOPS YURI.ROZENDO

## Tecnologias Utilizadas

- Frontend: React.js
- Backend: Spring Boot (Java 17)
- Containerização: Docker

## Estrutura do Projeto

O projeto está dividido em duas partes principais:

- `/teste-front`: Contém o código fonte da aplicação React.js
- `/teste-back`: Contém o código fonte da API Spring Boot

## Pré-requisitos

### Para execução via Docker:
- Docker
- Docker Compose

### Para desenvolvimento:
- Java 17 (JDK)
- Node.js (versão 14 ou superior)
- npm (geralmente vem com Node.js)
- Maven
- IDE de sua preferência (recomendamos IntelliJ IDEA para backend e VSCode para frontend)
- Git

### Opcional:
- PostgreSQL (para desenvolvimento local sem Docker)

## Configuração e Instalação

1. Clone o repositório:

   git clone https://github.com/audsonyuri/attus-teste.git
   cd attus-teste


3. Construa e inicie os containers:

   docker-compose up --build


## Uso

Após a inicialização dos containers, você pode acessar:

- Frontend: http://localhost:3000
- Backend API: http://localhost:8080

## Desenvolvimento

### Frontend

Para desenvolver o frontend:

1. Navegue até o diretório `/teste-front`
2. Instale as dependências: `npm install`
3. Inicie o servidor de desenvolvimento: `npm run serve`

### Backend

Para desenvolver o backend:

1. Navegue até o diretório `/teste-back`
2. Abra o projeto em sua IDE preferida
3. Execute a classe principal `java -jar app.jar`

## Implantação

1. Construa as imagens Docker:
   
   docker-compose build
   
2. Inicie os serviços:
   
   docker-compose up -d
   

## CI/CD Pipeline

Este projeto utiliza um pipeline de Integração Contínua e Implantação Contínua (CI/CD) baseado no GitHub Actions para automatizar o processo de build, teste e implantação na AWS.

### Visão Geral do Pipeline

O pipeline é acionado em pull requests direcionadas à `main`. Ele consiste em dois jobs principais:

1. **Build e Teste**
2. **Implantação no ECS (Elastic Container Service)**

### Pré-requisitos para CI/CD

- Conta AWS com acesso às seguintes serviços:
  - ECR (Elastic Container Registry)
  - ECS (Elastic Container Service)
- Secrets do GitHub configuradas no repositório:

  COMUM:
  - `AWS_PROD_REGION`
  - `AWS_PROD_ACCESS_KEY_ID`
  - `AWS_PROD_SECRET_ACCESS_KEY`
  - `AWS_PROD_ECS_CLUSTER`

  BACKEND:
  - `AWS_PROD_BACK_ECR_REPOSITORY`
  - `AWS_PROD_BACK_ECS_SERVICE`

  FRONTEND:
  - `AWS_PROD_FRONT_ECR_REPOSITORY`
  - `AWS_PROD_FRONT_ECS_SERVICE`
  
### Estrutura do Pipeline Backend

1. **Build e Teste**
   - Checkout do código
   - Configuração do JDK 17
   - Build com Maven
   - Execução de testes
   - Build e push da imagem Docker para o ECR

2. **Implantação no ECS**
   - Atualização do serviço ECS
   - Verificação da implantação

### Estrutura do Pipeline Frontend

1. **Build e Teste**
   - Checkout do código
   - Configuração do Node.js
   - Instalação de dependências
   - Execução de testes
   - Build e push da imagem Docker para o ECR

2. **Implantação no ECS**
   - Atualização do serviço ECS
   - Verificação da implantação

### Melhorias Futuras

- Adição de análise de código estático (ex: SonarQube)
- Estratégia de rollback automático
- Notificações de status de implantação (Slack, email)
- Ambiente de staging

### Customização do Pipeline

O arquivo de configuração do pipeline está localizado em `.github/workflows/aws-deploy.yml`. Desenvolvedores que precisam modificar o processo de CI/CD devem editar este arquivo.

### Resolução de Problemas

Se a implantação falhar, verifique os logs no console do GitHub Actions. Problemas comuns incluem:

- Secrets do GitHub não configuradas corretamente
- Permissões insuficientes na conta AWS
- Falhas nos testes unitários

Para assistência adicional, entre em contato com a equipe de DevOps.

## Contato

Audson Yuri F. Rozendo - audsonyuri@gmail.com

Link do projeto: [https://github.com/audsonyuri/attus-devops](https://github.com/audsonyuri/attus-devops)
