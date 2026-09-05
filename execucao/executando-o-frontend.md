# Executando o frontend

## Com Docker Compose

O comando da stack completa inicia o frontend com hot reload:

```bash
docker compose --env-file infra/.env.dev -f infra/docker-compose.dev.yml up --build
```

Acesse http://localhost:3000. Dentro da rede do Compose, o Next.js chama o
backend em `http://backend:8000`; o navegador continua falando apenas com
`localhost:3000`.

## Sem Docker

Primeiro inicie o backend na porta 8000. Em outro terminal:

```bash
cd frontend
npm install
cp .env.example .env.local
npm run dev
```

Confira `.env.local`:

```dotenv
BACKEND_URL=http://localhost:8000
JWT_SECRET=segredo-troque-em-producao
```

`JWT_SECRET` deve ser idêntico ao `JWT_SECRET_KEY` do backend. Depois, use:

- http://localhost:3000 para login;
- http://localhost:3000/register para cadastro;
- http://localhost:3000/profile para o perfil autenticado.

## Verificações

Na pasta `frontend`:

```bash
npm run typecheck
npm run build
```

Os testes Cypress existentes esperam que backend e frontend já estejam no ar:

```bash
npm run cypress:run
```

Eles cadastram o usuário `michelet`, exercitam duplicidade, realizam o login e
confirmam a criação do cookie `token`. A API de remoção do frontend é usada para
limpar o usuário antes do cenário de cadastro.

{% hint style="info" %}
O cookie é `secure` em produção. Em desenvolvimento ele pode ser usado por HTTP
em `localhost`.
{% endhint %}
