# PedeLogo Catálogo

## Visão Geral
Aplicação RESTful em C# (.NET Core 3.1) que expõe um catálogo de produtos e foi projetada como exemplo prático de uso de containers, Docker, Kubernetes e CI/CD com Jenkins.

## Funcionalidades
- API de catálogo de produtos em ASP.NET Core
- Persistência de dados em MongoDB
- Configuração por variáveis de ambiente
- Empacotamento em Docker
- Deploy em Kubernetes via manifestos em `k8s/`
- Pipeline Jenkins para build, push de imagem e deploy

## Tecnologias
- .NET Core 3.1
- ASP.NET Core Web API
- MongoDB.Driver
- Docker
- Kubernetes
- Jenkins
- NLog
- Swagger / OpenAPI
- Prometheus para métricas

## Estrutura do Projeto
- `src/PedeLogo.Catalogo.Api/` - código fonte da API
- `src/PedeLogo.Catalogo.Api/Dockerfile` - definição de imagem Docker
- `k8s/api.yaml` - manifesto de deploy da aplicação
- `k8s/mongodb.yaml` - manifesto de provisionamento de MongoDB
- `Jenkinsfile` - pipeline de CI/CD para build, push e deploy

## Pré-requisitos
- .NET Core SDK 3.1
- Docker
- Kubernetes (kubectl configurado)
- MongoDB ou cluster MongoDB acessível
- Jenkins com credenciais DockerHub e AWS EKS configuradas (opcional para pipeline)

## Configuração de Ambiente
Defina as variáveis de ambiente para conexão com MongoDB:

- `Mongo__DataBase` - nome do banco de dados
- `Mongo__Host` - host do MongoDB
- `Mongo__Port` - porta do MongoDB
- `Mongo__User` - usuário do MongoDB
- `Mongo__Password` - senha do MongoDB
- `MONGODB_PORT` - porta usada pela aplicação (opcional)

## Como Executar Localmente
1. Restaurar dependências:
   ```bash
   dotnet restore src/PedeLogo.Catalogo.Api/PedeLogo.Catalogo.Api.csproj
   ```
2. Executar a API:
   ```bash
   dotnet run --project src/PedeLogo.Catalogo.Api/PedeLogo.Catalogo.Api.csproj
   ```
3. A API estará disponível em `http://localhost:5000` (ou na porta configurada).

## Docker
Gerar a imagem Docker:
```bash
docker build -t pedelogo-catalogo:latest -f src/PedeLogo.Catalogo.Api/Dockerfile .
```

Executar a imagem localmente:
```bash
docker run -e Mongo__Host=<host> -e Mongo__Port=<port> -e Mongo__DataBase=<db> -e Mongo__User=<user> -e Mongo__Password=<password> -p 5000:80 pedelogo-catalogo:latest
```

## Kubernetes
Aplicar os manifestos do Kubernetes:
```bash
kubectl apply -f k8s/
```

## Pipeline Jenkins
O `Jenkinsfile` executa as etapas principais:
- build da imagem Docker usando o `Dockerfile`
- push da imagem para Docker Hub
- deploy no EKS usando `kubectl apply`

## Observações
- A API utiliza MongoDB como banco de dados principal.
- O projeto inclui integração com `NLog` para logging e `prometheus-net` para métricas.
- Ajuste as variáveis de ambiente e os arquivos de manifesto Kubernetes conforme o ambiente de destino.

## Contato
Para dúvidas ou melhorias, utilize este repositório como base para implementação de pipelines de entrega contínua e integração com containers.

## Assista a apresentação do projeto:

https://youtu.be/0o9bNBtsMI8

