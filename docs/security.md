# Segurança e privacidade

## Princípios adotados

O projeto separa dados públicos, administrativos e sensíveis. A aplicação evita colocar segredos no código e exige configurações externas para ambientes reais.

## Autenticação

- Senhas não devem ser persistidas em texto puro;
- Tokens de acesso e renovação usam segredos distintos;
- Recuperação de senha possui segredo próprio;
- Rotas administrativas exigem autenticação e autorização no backend;
- Credenciais de demonstração não devem ser reutilizadas em produção.

## Dados contratuais

CPFs relacionados à configuração do locador e aos snapshots contratuais são protegidos com AES-256-GCM, que fornece confidencialidade e verificação de integridade.

A variável responsável pela chave de criptografia contratual precisa:

- Ser forte e gerada de forma segura;
- Permanecer fora do repositório;
- Ser armazenada no gerenciador de segredos da infraestrutura;
- Ter backup seguro;
- Permanecer estável enquanto existirem dados criptografados com ela.

Perder ou substituir essa chave sem migração pode impedir a recuperação dos dados existentes.

## Pagamentos

A interface não deve coletar diretamente número completo do cartão, validade ou CVV. Em produção, informações de cartão devem ser preenchidas em componentes seguros hospedados pelo gateway.

O backend trabalha com identificadores, tokens e estados fornecidos pelo provedor, além de validar webhooks e aplicar idempotência para evitar processamento duplicado.

## Ambientes e segredos

Arquivos reais de ambiente não fazem parte do repositório. Cada implantação fornece suas próprias configurações, como:

- URLs e credenciais do banco;
- URL do Redis;
- Segredos de autenticação;
- Chave de criptografia contratual;
- Credenciais do serviço de e-mail;
- Credenciais e assinatura de webhook do gateway;
- Origens permitidas pelo CORS.

## Demonstração pública

O ambiente público deve usar somente dados fictícios. Recomenda-se limitar permissões, manter pagamentos em sandbox ou simulação e restaurar periodicamente o estado demonstrativo.

Não devem ser publicados:

- Arquivos `.env`;
- Tokens, senhas ou chaves;
- Dados pessoais reais;
- Logs com informações sensíveis;
- Dumps do banco de produção;
- Credenciais administrativas permanentes.

## Responsabilidade da implantação

Antes do uso em produção, o responsável pela operação deve revisar requisitos legais e regulatórios aplicáveis, política de privacidade, retenção de dados, backups, monitoramento, domínio, HTTPS e configurações dos provedores externos.
