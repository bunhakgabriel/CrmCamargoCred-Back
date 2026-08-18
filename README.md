# CRM Camargo Cred

## 📖 Sobre o projeto

O **CRM Camargo Cred** é um sistema desenvolvido para auxiliar na gestão de clientes e vendedores de um escritório de crédito consignado. O projeto surgiu a partir da necessidade de centralizar e organizar informações que anteriormente eram mantidas principalmente por meio de arquivos físicos.

Este repositório contém o **backend da aplicação**, responsável por disponibilizar a API utilizada pelo frontend, processar as requisições, aplicar as regras de negócio e realizar o gerenciamento dos dados do sistema.

A aplicação foi desenvolvida especificamente para atender às necessidades do escritório e já está em funcionamento em ambiente de produção, sendo utilizada em sua rotina de trabalho.

O projeto está em evolução contínua e possui planos para incorporar novas funcionalidades ao longo do tempo, incluindo recursos para **gestão de contratos, gestão financeira** e outras necessidades relacionadas à operação do escritório.

## ✨ Funcionalidades

### 🔐 Autenticação e autorização

* Validação dos tokens de autenticação emitidos pelo Firebase.
* Verificação do token em todas as requisições realizadas aos endpoints protegidos.
* Validação do e-mail do usuário após a autenticação para garantir que apenas usuários autorizados tenham acesso ao sistema.
* Bloqueio de requisições sem token ou com credenciais inválidas.
* Proteção das rotas da API por middleware de autenticação e autorização.

### 👥 API de clientes

* Endpoint para criação de clientes.
* Endpoint para consulta de cliente.
* Listagem de clientes com suporte a filtros.
* Paginação dos resultados.
* Atualização de clientes.
* Exclusão de clientes.
* Validação dos dados recebidos pela API.
* Associação opcional do cliente a um vendedor responsável.

### 👨‍💼 API de vendedores

* Endpoint para criação de vendedores.
* Endpoint para consulta de vendedor.
* Listagem de vendedores.
* Atualização de vendedores.
* Exclusão de vendedores.
* Validação dos dados recebidos pela API.
* Disponibilização dos vendedores para associação aos clientes.

### 🔗 Relacionamento entre clientes e vendedores

* Relacionamento entre clientes e vendedores armazenado no banco de dados.
* Um vendedor pode estar associado a vários clientes.
* Cada cliente pode possuir apenas um vendedor responsável.
* Validação e gerenciamento do relacionamento durante as operações de clientes.

### 📄 Gerenciamento de documentos

* Upload de documentos vinculados aos clientes.
* Criação de diretórios específicos para cada cliente no servidor.
* Associação dos documentos ao cliente através do seu identificador.
* Armazenamento dos arquivos no servidor.
* Persistência dos caminhos dos arquivos no banco de dados.
* Exclusão de documentos armazenados.
* Endpoint responsável pelas operações de upload e exclusão de documentos.

### 🗄️ Persistência e consultas

* Persistência dos dados utilizando PostgreSQL.
* Armazenamento das informações de clientes e vendedores.
* Armazenamento dos relacionamentos entre clientes e vendedores.
* Armazenamento das referências dos documentos.
* Processamento de filtros e paginação no backend.
* Consultas ao banco realizadas de acordo com os filtros enviados pelo frontend, retornando apenas os registros necessários.

### 📦 Padronização da API

* Padronização das respostas retornadas pelos endpoints.
* Estrutura de resposta contendo status da operação, dados, mensagens e metadados adicionais quando necessário.
* Tratamento centralizado de erros da aplicação.
* Retorno de códigos HTTP adequados para diferentes situações de erro.

## 🛠️ Tecnologias

### Backend

* **Node.js** — ambiente de execução utilizado no desenvolvimento do backend.
* **Express** — framework utilizado para construção da API e gerenciamento das rotas e middlewares.
* **Firebase Admin SDK** — integração com o Firebase no backend, incluindo validação dos tokens de autenticação.
* **Multer** — processamento dos arquivos enviados pelo frontend para upload de documentos.
* **CORS** — configuração do acesso da API para comunicação com o frontend.
* **dotenv** — gerenciamento das variáveis de ambiente utilizadas pela aplicação.

### Banco de dados

* **PostgreSQL** — banco de dados relacional utilizado para persistência das informações da aplicação.
* **node-postgres (pg)** — biblioteca utilizada para estabelecer e gerenciar a comunicação entre o backend e o PostgreSQL.

### Infraestrutura e produção

* **Ubuntu Linux** — sistema operacional utilizado na VPS de produção.
* **Nginx** — servidor utilizado como proxy reverso para disponibilização da API.
* **PM2** — gerenciamento do processo Node.js em produção, garantindo que a aplicação permaneça em execução.
* **Git** — utilizado para versionamento e atualização do código no ambiente de produção.
* **VPS** — infraestrutura utilizada para hospedagem da API e do banco de dados PostgreSQL.

## 🏗️ Arquitetura

O backend utiliza uma arquitetura organizada em camadas, buscando separar as responsabilidades relacionadas ao recebimento das requisições, regras de negócio e acesso aos dados.

O fluxo principal da aplicação segue a seguinte estrutura:

```text
Frontend
   │
   ▼
Routes
   │
   ▼
Middlewares
   │
   ▼
Controllers
   │
   ▼
Services
   │
   ├──────► Mappers
   │
   ▼
Repositories
   │
   ▼
PostgreSQL
```

### Routes

Responsáveis por definir os endpoints da API e direcionar as requisições para os controllers correspondentes.

### Middlewares

Responsáveis por operações que devem ocorrer antes da execução dos controllers, como autenticação e autorização das requisições, além do tratamento centralizado de erros.

### Controllers

Responsáveis por lidar com o contexto HTTP da aplicação, recebendo as requisições, acionando os services e retornando as respostas para o frontend.

### Services

Concentram a lógica da aplicação e coordenam as operações necessárias para atender às requisições recebidas pelos controllers.

### Repositories

Responsáveis pelo acesso ao banco de dados, executando as operações de persistência e consulta no PostgreSQL.

### Mappers

Responsáveis por transformar e adaptar os dados entre diferentes estruturas utilizadas pela aplicação.


## 🧩 Principais desafios técnicos

### 🖥️ Configuração do ambiente de produção

Um dos principais desafios do projeto foi disponibilizar a API em produção utilizando uma infraestrutura própria, sem depender de plataformas gerenciadas para realizar a hospedagem do backend.

Para isso, foi necessário configurar e administrar uma **VPS Linux**, preparar o ambiente para execução da aplicação, instalar e configurar o **PostgreSQL**, utilizar o **PM2** para gerenciamento do processo Node.js e configurar o **Nginx** como proxy reverso para disponibilização da API.

Além do desenvolvimento da aplicação, esse processo proporcionou experiência prática com deploy, configuração de servidores e manutenção de uma aplicação em ambiente de produção.

### 🔐 Autenticação, autorização e proteção das rotas

Por se tratar de um sistema que trabalha com informações internas do escritório, outro desafio importante foi garantir que somente usuários autorizados pudessem acessar os recursos da API.

A autenticação é realizada através do **Firebase**, enquanto o backend recebe e valida o token enviado pelo frontend em cada requisição protegida. Após a validação do token, o sistema também verifica se o e-mail autenticado pertence à lista de usuários autorizados.

Dessa forma, requisições sem um token válido ou realizadas por usuários não autorizados são bloqueadas antes de acessar os recursos protegidos da aplicação.

### 📄 Armazenamento e gerenciamento de documentos

Outro desafio foi definir uma estratégia adequada para o armazenamento dos documentos vinculados aos clientes.

Em projetos anteriores, arquivos eram armazenados diretamente no banco de dados utilizando Base64. Para este projeto, considerando a necessidade de trabalhar com múltiplos documentos por cliente, foi adotada uma abordagem diferente para evitar o armazenamento dos arquivos diretamente no PostgreSQL.

Os documentos são armazenados no sistema de arquivos do servidor, em diretórios associados ao identificador de cada cliente, enquanto o banco de dados mantém as referências necessárias para localizar esses arquivos.

Essa implementação permitiu separar o armazenamento dos arquivos da persistência dos demais dados da aplicação e disponibilizar os documentos ao frontend quando necessário.
