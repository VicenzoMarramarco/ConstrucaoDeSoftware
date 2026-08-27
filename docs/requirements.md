## **Documento de Requisitos**

**Histórico de Revisão**

|Data|Versão|Descrição|Autor|
| - | - | - | - |
|[dd/mm/aaaa]|0.1|Versão inicial|[Nome do autor]|

## **1. Introdução**

### **1.1 Propósito**
Este documento tem como objetivo especificar os requisitos funcionais e não funcionais do sistema Experienciando, servindo como referência para o desenvolvimento, manutenção e validação da solução. O projeto contempla comunicação em tempo real, autenticação de usuários e gerenciamento de conversas.

### **1.2 Escopo**
O Experienciando é um sistema de comunicação baseado em mensagens, voltado para usuários que desejam trocar texto em conversas individuais ou em grupos. A solução inclui backend, aplicação móvel em React Native e acesso via navegador, utilizando uma base de dados relacional para armazenamento das mensagens e dos usuários.

### **1.3 Definições, Acrônimos e Abreviações**

|Termo|Definição|
| - | - |
|Experienciando|Sistema de chat e comunicação do projeto|
|API|Interface de programação de aplicação|
|JWT|Token para autenticação segura entre cliente e servidor|
|RN|React Native|
|ER|Entidade e relacionamento|

### **1.4 Referências**
- Documento de arquitetura do sistema Experienciando;
- Requisitos do projeto definidos pela equipe;
- Estrutura de dados atual do sistema para usuários, mensagens e conversas;
- Boas práticas de desenvolvimento para aplicações web e mobile.

## **2. Descrição Geral**

### **2.1 Perspectiva do Produto**
O sistema é uma aplicação nova, sendo desenvolvida como solução de comunicação para suporte à troca de mensagens entre usuários. Ele integra a experiência mobile com a versão em navegador, usando uma API central para gerenciar usuários, autenticação e persistência das conversas.

### **2.2 Funções do Produto**
O produto deve permitir:
- cadastro e autenticação de usuários;
- criação de conversas;
- envio e recebimento de mensagens;
- listagem de histórico de conversa;
- acesso ao sistema em mobile e navegador.

### **2.3 Características dos Usuários**
Os usuários principais são pessoas que precisam trocar mensagens de forma simples, direta e segura. O perfil de uso é variado, desde usuários iniciantes até usuários com maior familiaridade com aplicativos e sistemas web.

### **2.4 Restrições**
- necessidade de manter comunicação segura e autenticada;
- uso de uma arquitetura centralizada para evitar duplicação de regras de negócio;
- necessidade de suporte a múltiplas plataformas (mobile e navegador);
- dependência de persistência de mensagens e usuários em banco relacional.

### **2.5 Suposições e Dependências**
- os usuários possuem acesso a um dispositivo móvel ou navegador para uso do sistema;
- a API backend estará disponível para clientes web e mobile;
- o banco relacional será responsável pela persistência de usuários, conversas e mensagens;
- os dados de autenticação serão protegidos e validados em cada requisição.

## **3. Requisitos Funcionais**

Requisitos funcionais descrevem **o que o sistema deve fazer**.

| ID | Descrição | Prioridade |
| -- | --------- | :--------: |
| RF01 | O sistema deve permitir o cadastro de usuários com nome, e-mail e senha. | Alta |
| RF02 | O sistema deve permitir login e autenticação segura dos usuários. | Alta |
| RF03 | O sistema deve permitir a criação de uma conversa entre usuários. | Alta |
| RF04 | O sistema deve permitir o envio de mensagens em uma conversa existente. | Alta |
| RF05 | O sistema deve permitir a listagem das conversas de um usuário. | Alta |
| RF06 | O sistema deve permitir a recuperação do histórico de mensagens de uma conversa. | Alta |
| RF07 | O sistema deve manter o vínculo entre usuários e conversas no banco de dados. | Média |
| RF08 | O sistema deve permitir acesso ao chat tanto em navegador quanto em aplicativo móvel. | Média |

## **4. Requisitos Não Funcionais**

Requisitos não funcionais descrevem **qualidades e restrições técnicas** do sistema.

| ID | Categoria | Descrição | Prioridade |
| -- | --------- | --------- | :--------: |
| RNF01 | Desempenho | O sistema deve responder às requisições de autenticação e leitura de mensagens em tempo aceitável para uso contínuo. | Alta |
| RNF02 | Segurança | O sistema deve proteger credenciais e autenticar os usuários via mecanismo seguro, como token JWT. | Alta |
| RNF03 | Usabilidade | A interface deve ser simples, clara e de fácil uso em mobile e navegador. | Média |
| RNF04 | Manutenibilidade | O código deve ser organizado em camadas para facilitar manutenção e evolução. | Média |
| RNF05 | Portabilidade | O sistema deve suportar acesso em diferentes plataformas sem alterar a lógica principal da aplicação. | Média |

## **5. Regras de Negócio**

| ID | Descrição |
| -- | --------- |
| RN01 | Cada usuário deve possuir um cadastro único com e-mail válido. |
| RN02 | Uma mensagem deve estar sempre vinculada a um remetente e a uma conversa. |
| RN03 | Uma conversa pode ter múltiplos participantes. |
| RN04 | O histórico de mensagens deve permanecer persistido no banco de dados. |
| RN05 | Apenas participantes da conversa podem visualizar e enviar mensagens. |

## **6. Protótipos**

Os protótipos devem ilustrar as telas de login, cadastro, lista de conversas e envio de mensagem. Como o projeto ainda está em fase de documentação e desenvolvimento, os wireframes podem ser adicionados posteriormente conforme a evolução da interface.
