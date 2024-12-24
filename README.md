# 🐳 Docker Infrastructure with .NET 8

## 📜 Descrição

Este repositório contém a infraestrutura necessária para executar uma aplicação **.NET 8** em um ambiente **Dockerizado**. A arquitetura inclui:

- **Banco Relacional (SQL Server)**: Para persistência de dados estruturados.
- **Banco Não Relacional (MongoDB)**: Para dados não estruturados e escalabilidade horizontal.
- **Mensageria (RabbitMQ)**: Para processamento assíncrono de mensagens.
- **.NET 8**: Aplicação desenvolvida em **.NET 8** que integra esses serviços e oferece uma API RESTful.
- **Redis**: Para caching e armazenamento de dados temporários.
- **Elasticsearch**: Para buscas eficientes em dados.
- **Nginx**: Como proxy reverso para balanceamento de carga.
- **Prometheus & Grafana**: Para monitoramento e alertas.
- **Fluentd**: Para coleta e encaminhamento de logs.

Este projeto é ideal para quem deseja configurar uma infraestrutura de desenvolvimento local e testar soluções distribuídas utilizando **Docker** e **.NET 8**.

## 🚀 Funcionalidades

- **Banco Relacional (SQL Server)** 🗃️: Persistência de dados estruturados.
- **Banco Não Relacional (MongoDB)** 🌱: Armazenamento de dados não estruturados.
- **Mensageria (RabbitMQ)** 📥: Comunicação assíncrona entre microserviços.
- **Cache (Redis)** 🧊: Armazenamento de dados temporários e cache de alto desempenho.
- **Busca (Elasticsearch)** 🔎: Indexação e busca eficiente em grandes volumes de dados.
- **Nginx** 🌐: Balanceamento de carga e proxy reverso para serviços.
- **Monitoramento (Prometheus & Grafana)** 📊: Monitoramento e alertas em tempo real.
- **Logs (Fluentd)** 📝: Coleta, agregação e encaminhamento de logs de aplicativos.
- **.NET 8** 💻: Implementação de microserviços com API RESTful.

## 🛠️ Tecnologias

- **.NET 8** (C#)
- **Docker** 🐳
- **SQL Server** 🗃️
- **MongoDB** 🌱
- **RabbitMQ** 📥
- **Redis** 🧊
- **Elasticsearch** 🔎
- **Nginx** 🌐
- **Prometheus** 📊
- **Grafana** 📈
- **Fluentd** 📝
- **Docker Compose** 🔧

## 🧑‍💻 Requisitos

### Pré-requisitos:

- **Docker** instalado em sua máquina.
- **Docker Compose** para orquestrar os containers.
- **.NET 8 SDK** ou superior.
- Conta no **Docker Hub** para buscar imagens, caso necessário.

### Instalação do Docker

1. **Windows/macOS**: [Download Docker Desktop](https://www.docker.com/products/docker-desktop)
2. **Linux**: Siga a [documentação oficial](https://docs.docker.com/engine/install/).

### Instalação do Docker Compose

O **Docker Compose** geralmente já vem instalado com o Docker Desktop. Para instalar manualmente no Linux, siga a [documentação oficial](https://docs.docker.com/compose/install/).

## 📝 Arquitetura

A infraestrutura é composta pelos seguintes serviços:

- **SQL Server**: Banco de dados relacional para persistência de dados estruturados.
- **MongoDB**: Banco de dados NoSQL para dados não estruturados.
- **RabbitMQ**: Sistema de mensageria para comunicação assíncrona.
- **Redis**: Sistema de cache para dados temporários.
- **Elasticsearch**: Motor de busca eficiente para grandes volumes de dados.
- **Nginx**: Proxy reverso e balanceamento de carga para a aplicação.
- **Prometheus & Grafana**: Monitoramento e geração de métricas em tempo real.
- **Fluentd**: Agregador de logs para coletar, processar e encaminhar logs.

### Estrutura do Projeto

/docker-infrastructure-dotnet8 ├── /src │ ├── Api/ # Aplicação .NET 8 com API RESTful │ ├── Models/ # Modelos de dados ├── /docker │ ├── docker-compose.yml # Arquivo de configuração do Docker Compose │ ├── Dockerfile # Dockerfile para a aplicação .NET 8 ├── /scripts │ ├── init.sql # Script SQL de inicialização do banco relacional (SQL Server) │ ├── init-mongo.js # Script de inicialização do MongoDB │ ├── fluentd.conf # Configuração do Fluentd

## 🚀 Como Usar

### 1. Clonando o Repositório

Clone o repositório para sua máquina local:

```
git clone https://github.com/usuario/docker-infrastructure-dotnet8.git
cd docker-infrastructure-dotnet8
```

### 2. Subindo a Infraestrutura com Docker Compose
Use o Docker Compose para subir todos os containers necessários. O arquivo docker-compose.yml já contém as configurações para rodar:

SQL Server na porta 1433
MongoDB na porta 27017
RabbitMQ na porta 5672
Redis na porta 6379
Elasticsearch na porta 9200
Prometheus & Grafana para monitoramento nas portas 9090 e 3000, respectivamente
Fluentd para coleta de logs na porta 24224
Aplicação .NET 8 na porta 5000

Execute o comando:

```
docker-compose up -d
```

Isso irá:

Construir e iniciar os containers.
Criar redes Docker para comunicação entre os containers.
Subir a aplicação .NET 8, bancos de dados, RabbitMQ, Redis, Elasticsearch, Nginx, Prometheus, Grafana, e Fluentd.
3. Acessando a Aplicação
Uma vez que os containers estejam rodando, você pode acessar a API da aplicação em:

API .NET 8: http://localhost:5000
RabbitMQ: http://localhost:15672 (usuário: guest, senha: guest)
MongoDB: mongodb://localhost:27017
SQL Server: Server=localhost,1433;Database=MyDatabase;User Id=sa;Password=yourPassword123!;
Redis: redis://localhost:6379
Elasticsearch: http://localhost:9200
Prometheus: http://localhost:9090
Grafana: http://localhost:3000 (usuário: admin, senha: admin)
Fluentd: Coleta logs de todos os containers.
4. Inicialização do Banco Relacional (SQL Server)
Ao iniciar o SQL Server, você pode executar um script SQL para inicializar o banco de dados. O arquivo scripts/init.sql contém exemplos de como criar tabelas e relacionamentos.

Para inicializar o banco, entre no container SQL Server e execute o script:

```
docker exec -it <sql-server-container-id> /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P yourPassword123! -i /scripts/init.sql
```

### 5. Usando a API

A API expõe endpoints RESTful para interagir com os serviços. Aqui estão alguns exemplos:

GET /api/products: Retorna todos os produtos armazenados no SQL Server.
POST /api/messages: Envia uma mensagem para o RabbitMQ.
GET /api/mongodb/products: Recupera produtos armazenados no MongoDB.

### 6. Cache com Redis
A aplicação pode usar o Redis para caching de dados. Exemplo de uso:

```
public class RedisService
{
    private readonly ConnectionMultiplexer _redis;
    private readonly IDatabase _db;

    public RedisService(IConfiguration configuration)
    {
        _redis = ConnectionMultiplexer.Connect(configuration["Redis:ConnectionString"]);
        _db = _redis.GetDatabase();
    }

    public void SetCache(string key, string value)
    {
        _db.StringSet(key, value);
    }

    public string GetCache(string key)
    {
        return _db.StringGet(key);
    }
}
```

### 📊 Monitoramento com Prometheus & Grafana

**Prometheus**

O Prometheus coleta métricas de todos os containers Docker, incluindo a aplicação .NET 8 e outros serviços.
As métricas podem ser acessadas em http://localhost:9090.

**Grafana**

Grafana é usado para visualizar as métricas coletadas pelo Prometheus.
A interface do Grafana pode ser acessada em http://localhost:3000 (usuário: admin, senha: admin).

### 📝 Logs com Fluentd

O Fluentd coleta logs de todos os containers e pode ser configurado para enviar esses logs para diversos destinos, como Elasticsearch ou arquivos locais. A configuração básica do Fluentd pode ser encontrada no arquivo scripts/fluentd.conf.

### 🤝 Contribuição

Se você deseja contribuir com melhorias, siga estas etapas:

Faça um fork do repositório.
Crie uma nova branch para sua feature (git checkout -b minha-feature).
Realize as alterações desejadas e faça commit (git commit -am 'Adiciona nova feature').
Envie suas alterações para o repositório remoto (git push origin minha-feature).
Abra um pull request explicando suas mudanças.

### 📝 Licença
Este projeto está licenciado sob a MIT License - veja o arquivo LICENSE.
