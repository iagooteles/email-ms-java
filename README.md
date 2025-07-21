# 📧 Microserviço de Email

Este projeto é um microserviço desenvolvido em Java com Spring Boot responsável por consumir mensagens da fila RabbitMQ e realizar o envio de e-mails. Ele faz parte de um sistema de microsserviços que se comunica de forma assíncrona através do RabbitMQ. Os dados dos emails enviados (ou com erro) são armazenados em um banco de dados PostgreSQL containerizado via Docker.

## 🔗 Este serviço recebe mensagens do microserviço de usuários e processa o envio dos e-mails.

Repositório do microserviço de usuários: 

```bash
https://github.com/iagooteles/user-ms-java
```

## 🚀 Tecnologias Utilizadas

Java 17+
Spring Boot
Spring Data JPA
Spring AMQP (RabbitMQ)
Spring Mail
PostgreSQL
Docker
Jakarta Validation

## ✉️ Funcionamento

Este microserviço consome mensagens enviadas por outros serviços (como o de usuários) através do RabbitMQ.

- As mensagens são recebidas na fila definida pela propriedade broker.queue.email.name.
- A classe EmailConsumer escuta a fila e consome as mensagens do tipo EmailDto.
- O conteúdo é transformado em um EmailModel e processado pela EmailService.
- O e-mail é enviado com a biblioteca JavaMailSender.
- O status do envio (SENT ou ERROR) é armazenado no banco de dados PostgreSQL.

## 📁 Estrutura do Projeto
`configs`: Configurações do RabbitMQ.  
`consumers`: ouvinte da fila do RabbitMQ (EmailConsumer).  
`controllers`: (opcional neste serviço, não expõe endpoints)  
`dtos`: objeto de dados transferido entre microsserviços.  
`models`: entidade EmailModel que representa os dados persistidos.  
`repository`: interface de persistência com o banco (EmailRepository).  
`services`: lógica de envio de e-mails (EmailService).  
`enums`: ENUMS de status de envio (SENT, ERROR).  

## 🐳 Como Rodar Localmente
Pré-requisitos: Docker, Java 17+, RabbitMQ ativo

Suba o container do PostgreSQL com Docker
Configure seu .properties com as credenciais corretas
Garanta que o RabbitMQ esteja acessível (ex: CloudAMQP)
Execute o projeto Spring Boot (main da classe EmailApplication)
Acompanhe os logs e a persistência dos dados no banco
