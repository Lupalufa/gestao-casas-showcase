# Diagramas

Este diretório receberá o diagrama visual definitivo da arquitetura.

Nome sugerido:

```text
architecture-overview.png
```

O diagrama pode representar:

```text
Usuário
  ↓
Frontend React
  ↓ HTTPS
API Node.js/Express
  ├── PostgreSQL/Neon
  ├── Redis
  ├── Mercado Pago
  └── Serviço de e-mail
```

Use somente nomes genéricos e não inclua hosts, credenciais, chaves ou detalhes internos do ambiente real.
