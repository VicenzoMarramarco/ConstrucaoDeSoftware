## **Documento de Requisitos**

**Histórico de Revisão**

|Data|Versão|Descrição|Autor|
| - | - | - | - |
|31/08/2026|0.1|Versão inicial com especificação de domínio|Equipe do projeto|

## **1. Introdução**

### **1.1 Propósito**
Este documento tem como objetivo especificar os requisitos funcionais e não funcionais da Plataforma de Assinaturas de Experiências, servindo como referência para o desenvolvimento, manutenção e validação da solução. O projeto contempla gestão de assinantes, catálogo de experiências, parceiros e emissão/validação de vouchers.

### **1.2 Escopo**
A Plataforma de Assinaturas de Experiências é um sistema de clube de benefícios voltado para assinantes que desejam acessar experiências presenciais (turismo, gastronomia, eventos culturais) de forma recorrente com resgates sob demanda. A solução inclui backend, aplicação móvel em React Native e acesso via navegador, utilizando uma base de dados relacional para armazenamento de assinantes, parceiros, experiências e vouchers.

### **1.3 Definições, Acrônimos e Abreviações**

|Termo|Definição|
| - | - |
|Assinante|Cliente ativo com assinatura válida na plataforma|
|Parceiro|Estabelecimento (hotel, restaurante, teatro) que oferece experiências|
|Experiência|Oferta ou serviço específico prestado por um parceiro|
|Voucher|Cupom/código de resgate emitido para utilização de uma experiência|
|API|Interface de programação de aplicação|
|JWT|Token para autenticação segura entre cliente e servidor|
|RN|React Native|
|UNIQUE|Restrição de unicidade que garante máximo um registro por chave composta|

### **1.4 Referências**
- Documento de Arquitetura da Plataforma de Assinaturas de Experiências;
- Especificação de Domínio do projeto;
- Estrutura de dados (Customer, Subscription, Partner, Experience, Voucher);
- Boas práticas de desenvolvimento para aplicações web e mobile com backend centralizado.

## **2. Descrição Geral**

### **2.1 Perspectiva do Produto**
A Plataforma de Assinaturas de Experiências é uma aplicação nova que resolve três problemas principais: (1) fadiga de decisão do consumidor na busca de atividades de lazer, (2) ociosidade e alto custo de aquisição para parceiros, e (3) falta de previsibilidade de receita no setor de lazer. O sistema integra a experiência mobile com a versão em navegador, usando uma API central para gerenciar assinantes, parceiros, catálogo de experiências e emissão/validação de vouchers.

### **2.2 Funções do Produto**
O produto deve permitir:
- cadastro e autenticação de assinantes;
- gestão de perfis de interesse dos assinantes;
- cadastro e visualização de parceiros e suas experiências;
- consulta de catálogo de experiências (filtrado por categoria e parceiro);
- emissão ilimitada de vouchers respeitando a regra de máximo 1 resgate por parceiro;
- resgate e validação de vouchers com controle de status;
- acesso ao sistema em mobile e navegador.

### **2.3 Características dos Usuários**
Os usuários principais são:
- **Assinantes**: pessoas que desejam acessar experiências presenciais de forma recorrente sem se preocupar com decisão e planejamento;
- **Parceiros**: hotéis, restaurantes, teatros e produtoras culturais que buscam reduzir sazonalidade e garantir receita previsível;
- **Administradores**: responsáveis pela gestão do catálogo, parceiros e assinantes.

### **2.4 Restrições**
- necessidade de manter comunicação segura e autenticada entre cliente e servidor;
- uso de uma arquitetura centralizada para evitar duplicação de regras de negócio;
- necessidade de suporte a múltiplas plataformas (mobile e navegador);
- dependência de persistência de dados em banco relacional;
- aplicação rigorosa da regra de negócio: máximo 1 voucher por combinação (customer_id, partner_id);
- validação de status de assinatura antes de emissão de vouchers.

### **2.5 Suposições e Dependências**
- os assinantes possuem acesso a um dispositivo móvel ou navegador para uso do sistema;
- os parceiros possuem interface web ou mobile para validação de resgates;
- a API backend estará disponível para clientes web e mobile;
- o banco relacional será responsável pela persistência de todos os dados;
- os dados de autenticação serão protegidos e validados em cada requisição;
- as assinaturas possuem datas de validade que determinam elegibilidade para resgate.

## **3. Requisitos Funcionais**

Requisitos funcionais descrevem **o que o sistema deve fazer**.

| ID | Descrição | Prioridade |
| -- | --------- | :--------: |
| RF01 | O sistema deve permitir o cadastro de clientes/assinantes com nome, e-mail e documento. | Alta |
| RF02 | O sistema deve permitir login e autenticação segura dos assinantes. | Alta |
| RF03 | O sistema deve permitir o cadastro de parceiros com informações de negócio (categoria, contato, endereço). | Alta |
| RF04 | O sistema deve permitir que parceiros cadastrem experiências com título, descrição, categoria e termos. | Alta |
| RF05 | O sistema deve permitir a consulta do catálogo de experiências filtrado por categoria e/ou parceiro. | Alta |
| RF06 | O sistema deve gerenciar o ciclo de vida de assinativas (status: ativo, cancelado, inadimplente). | Alta |
| RF07 | O sistema deve emitir vouchers ilimitados respeitando a restrição de máximo 1 resgate por (customer, partner). | Alta |
| RF08 | O sistema deve validar que apenas assinantes com assinatura ativa podem emitir vouchers. | Alta |
| RF09 | O sistema deve manter o controle de status do voucher (Disponível, Utilizado, Expirado, Cancelado). | Alta |
| RF10 | O sistema deve permitir a validação/resgate de vouchers pelo parceiro. | Alta |
| RF11 | O sistema deve gerar código identificador único para cada voucher emitido. | Média |
| RF12 | O sistema deve registrar data/hora de emissão e resgate de vouchers. | Média |
| RF13 | O sistema deve permitir acesso ao catálogo e emissão de vouchers em navegador e aplicativo móvel. | Média |
| RF14 | O sistema deve manter o histórico de vouchers (emitidos, resgatados, expirados) para análise. | Média |

## **4. Requisitos Não Funcionais**

Requisitos não funcionais descrevem **qualidades e restrições técnicas** do sistema.

| ID | Categoria | Descrição | Prioridade |
| -- | --------- | --------- | :--------: |
| RNF01 | Desempenho | O sistema deve responder às requisições de autenticação, consulta de catálogo e emissão de vouchers em tempo aceitável (máx. 2s). | Alta |
| RNF02 | Segurança | O sistema deve proteger credenciais e autenticar os usuários via mecanismo seguro, como token JWT. | Alta |
| RNF03 | Segurança | O sistema deve validar e aplicar a regra de unicidade (máx. 1 voucher por customer-partner) em nível de banco de dados. | Alta |
| RNF04 | Usabilidade | A interface deve ser simples, clara e de fácil uso em mobile e navegador. | Média |
| RNF05 | Manutenibilidade | O código deve ser organizado em camadas para facilitar manutenção, testes e evolução. | Média |
| RNF06 | Portabilidade | O sistema deve suportar acesso em diferentes plataformas (mobile, web) sem alterar a lógica principal da aplicação. | Média |
| RNF07 | Escalabilidade | O sistema deve ser capaz de suportar crescimento de assinantes, parceiros e vouchers sem degradação significativa de performance. | Média |
| RNF08 | Disponibilidade | O sistema deve apresentar disponibilidade mínima de 99% durante horários comerciais. | Baixa |

## **5. Regras de Negócio**

| ID | Descrição |
| -- | --------- |
| RN01 | Cada assinante deve possuir um cadastro único com e-mail e documento válidos. |
| RN02 | Uma assinativa deve conter status válido (ativo, cancelado, inadimplente) e datas de vigência. |
| RN03 | Apenas assinantes com assinatura ativa podem emitir vouchers. |
| RN04 | Um assinante pode emitir no máximo um voucher por parceiro (restrição UNIQUE(customer_id, partner_id)). |
| RN05 | Cada voucher possui um código identificador único e status no ciclo de vida (Disponível, Utilizado, Expirado, Cancelado). |
| RN06 | Um parceiro pode oferecer uma ou mais experiências. |
| RN07 | Uma experiência deve estar vinculada a exatamente um parceiro. |
| RN08 | O histórico de todas as operações (emissão, resgate, expiração) deve ser persistido para auditoria. |
| RN09 | A validação de resgate é feita pelo parceiro e marca o voucher como Utilizado com data/hora do resgate. |
| RN10 | Vouchers expiram automaticamente conforme data de validade da assinatura associada. |

## **6. Protótipos**

Os protótipos devem ilustrar as seguintes telas e fluxos:

**Para Assinantes:**
- Login e cadastro
- Dashboard com catálogo de experiências
- Filtros por categoria e parceiro
- Detalhes da experiência
- Emissão de voucher (com validação de regra de negócio)
- Meus vouchers (com status)
- Resgate de voucher

**Para Parceiros:**
- Login e gestão de perfil
- Cadastro e edição de experiências
- Validação/resgate de vouchers (check-in)
- Relatório de resgates

Como o projeto ainda está em fase de documentação e desenvolvimento, os wireframes podem ser adicionados posteriormente conforme a evolução da interface.
