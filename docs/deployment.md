# Estratégia de implantação

## Ambientes suportados

O projeto foi preparado para dois cenários principais:

- Execução local com Docker Compose;
- Hospedagem em serviços gerenciados, com frontend e backend separados.

## Ambiente local

O Compose organiza os seguintes serviços:

- Frontend;
- API;
- PostgreSQL;
- Redis.

Variáveis de exemplo documentam a configuração, mas segredos reais são fornecidos apenas no ambiente de execução.

## Ambiente hospedado

A implantação de referência utiliza:

- **Render** para frontend e backend;
- **Neon** para PostgreSQL;
- **Redis gerenciado** para dados transitórios;
- **Mercado Pago** para pagamentos;
- **Provedor SMTP** para mensagens transacionais.

As conexões públicas usam HTTPS e o banco externo exige SSL. A URL pública do frontend deve ser liberada no CORS da API, e a URL pública do backend deve ser incorporada ao build do frontend.

## Preparação do banco

Após configurar a conexão, a implantação executa as migrations. Seeders demonstrativos podem ser aplicados somente em ambientes apropriados e nunca devem inserir dados pessoais ou credenciais de produção.

## Operação da demonstração

Para um showcase público:

- Utilize uma conta específica e permissões limitadas;
- Mantenha dados fictícios;
- Use pagamentos simulados ou sandbox;
- Monitore o consumo dos planos gratuitos;
- Considere uma rotina de restauração do banco;
- Informe que o primeiro acesso pode demorar em serviços que entram em repouso.

## Produção

A receita de implantação acelera a configuração, mas não elimina as responsabilidades operacionais. O responsável pelo ambiente deve cuidar de domínio, segredos, backup, observabilidade, custos, política de privacidade, credenciais dos serviços e integrações reais.
