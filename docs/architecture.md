# Arquitetura

## Contexto

O Gestão de Casas segue uma arquitetura cliente-servidor. O frontend concentra a experiência do visitante, do cliente e do administrador; o backend aplica autenticação, autorização e regras de negócio e integra os serviços externos.

## Componentes

### Frontend

A interface foi construída com React 19, TypeScript e Vite. Ela consome a API por HTTPS e oferece fluxos diferentes de acordo com o perfil autenticado.

Responsabilidades principais:

- Apresentar o catálogo e as galerias de imóveis;
- Coletar os dados necessários para cadastro e reserva;
- Exibir disponibilidade, contratos e pagamentos;
- Oferecer as operações administrativas;
- Hospedar os componentes seguros fornecidos pelo gateway de pagamento.

### Backend

A API utiliza Node.js, Express e Sequelize. As rotas são documentadas com OpenAPI/Swagger.

Responsabilidades principais:

- Autenticação e autorização;
- Validação e processamento das regras de negócio;
- Gestão de imóveis, clientes, reservas e contratos;
- Orquestração dos pagamentos;
- Persistência e consulta de dados;
- Envio de e-mails e processamento de webhooks.

### PostgreSQL

Armazena os dados relacionais da aplicação, incluindo usuários, imóveis, reservas, contratos, configurações e registros financeiros. Migrations e seeders permitem criar e popular ambientes controlados.

### Redis

Atende necessidades transitórias da aplicação e complementa fluxos que exigem armazenamento rápido. A indisponibilidade do Redis deve ser tratada de acordo com a criticidade de cada operação.

### Serviços externos

- **Mercado Pago:** pagamentos e notificações por webhook;
- **Provedor de e-mail:** mensagens transacionais;
- **Render:** hospedagem dos serviços da aplicação;
- **Neon:** PostgreSQL gerenciado com conexão SSL.

## Fluxo simplificado de uma reserva

1. O cliente seleciona um imóvel e um período disponível.
2. O frontend envia a solicitação para a API.
3. O backend valida autenticação, regras e disponibilidade.
4. A reserva é persistida no PostgreSQL.
5. Quando aplicável, a API inicia o fluxo de pagamento.
6. O gateway confirma mudanças de estado por resposta e webhook.
7. A aplicação atualiza a reserva de maneira idempotente.

## Perfis de acesso

- **Visitante:** consulta informações públicas;
- **Cliente:** mantém seus dados e realiza reservas;
- **Administrador:** gerencia a operação, configurações e relatórios.

As permissões são verificadas no backend; esconder uma ação na interface não substitui autorização na API.

## Implantação

O produto pode ser executado localmente com Docker Compose ou implantado em serviços independentes. Em produção, frontend, API, PostgreSQL e Redis têm ciclos próprios, conectados por URLs e credenciais definidas em variáveis de ambiente.

Consulte [Estratégia de implantação](deployment.md) para mais detalhes.
