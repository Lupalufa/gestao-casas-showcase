# Decisões de engenharia

## Preservação histórica dos contratos

Um contrato emitido representa um acordo em determinado momento. Por isso, ele não deve depender exclusivamente dos valores atuais do cadastro do locador.

A solução mantém um snapshot dos dados utilizados na emissão. Assim, correções ou mudanças posteriores na configuração passam a valer para contratos futuros sem alterar o conteúdo histórico dos anteriores.

## Configuração centralizada do locador

Os dados do responsável pela locação ficam em uma configuração administrativa própria. Isso evita usar dados de um cliente antigo como proprietário padrão e permite reutilizar informações consistentes na geração de novos contratos.

## Pagamentos sem coleta direta de cartão

Campos próprios para número, validade e CVV aumentariam a exposição da aplicação a dados financeiros sensíveis. A arquitetura foi preparada para componentes hospedados pelo gateway, mantendo no sistema apenas dados necessários para a operação, como parcelas e identificadores do pagamento.

## Gateway substituível

O pagamento foi organizado em torno de uma camada de integração. O Mercado Pago é o provedor de referência, enquanto um modo simulado permite demonstração e desenvolvimento sem transações reais.

As credenciais pertencem ao operador que implanta o sistema e nunca são distribuídas junto com o código.

## Idempotência e concorrência

Pagamentos podem gerar tentativas repetidas, retornos tardios e webhooks concorrentes. A aplicação considera chaves idempotentes e transições controladas de estado para reduzir cobranças ou atualizações duplicadas.

## Imagens dos imóveis

Cada imóvel aceita múltiplas imagens. A primeira imagem enviada funciona como capa nos cards e como primeiro destaque na página de detalhes. Na ausência de upload, a interface utiliza um estado visual padrão.

## Infraestrutura reproduzível

Docker Compose reúne frontend, backend, PostgreSQL e Redis para execução local. Para hospedagem, uma receita de infraestrutura documenta os serviços e as variáveis necessárias, reduzindo decisões manuais durante a implantação.

## Documentação da API

O Swagger serve como referência executável das rotas. Ele facilita avaliação, integração e manutenção sem substituir as validações de autenticação e autorização.

## Produto brasileiro

A interface e os documentos foram pensados para o contexto brasileiro, incluindo linguagem, CPF/CNPJ, endereços e meios de pagamento locais. A documentação técnica em inglês pode acompanhar a distribuição comercial, mas a localização da interface faz parte do posicionamento original do produto.
