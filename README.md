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
