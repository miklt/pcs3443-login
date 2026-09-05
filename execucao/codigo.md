# Obtendo o código

Clone o repositório da aplicação:

```bash
git clone https://github.com/miklt/pcs3443-2021.git
cd pcs3443-2021
```

O repositório é um monorepo simples:

```text
pcs3443-2021/
├── backend/                    # API FastAPI, testes e Dockerfile
├── frontend/                   # aplicação Next.js, Cypress e Dockerfile
├── infra/
│   ├── docker-compose.dev.yml  # stack local completa
│   ├── docker-compose.prod.yml # banco + backend de produção
│   ├── scripts/                # preparação e deploy do servidor
│   └── tests/e2e_dev.py        # teste integrado da stack
├── .github/workflows/deploy.yml
└── docker-compose.yml          # atalho para o Compose de desenvolvimento
```

## Início rápido com Docker

Na raiz do repositório:

```bash
docker compose --env-file infra/.env.dev -f infra/docker-compose.dev.yml up --build
```

Quando os serviços estiverem prontos:

- aplicação: http://localhost:3000;
- API: http://localhost:8000;
- documentação interativa da API: http://localhost:8000/docs;
- PostgreSQL: `localhost:5432`.

Para executar em segundo plano, acrescente `-d`. Para acompanhar ou encerrar:

```bash
docker compose --env-file infra/.env.dev -f infra/docker-compose.dev.yml logs -f
docker compose --env-file infra/.env.dev -f infra/docker-compose.dev.yml down
```

O volume `pgdata-dev` preserva os dados entre reinicializações. `docker compose
down` não apaga o volume; `down -v` o remove e apaga o banco de desenvolvimento.

{% hint style="warning" %}
Use `down -v` somente quando quiser descartar deliberadamente todos os dados
locais do PostgreSQL.
{% endhint %}

Para executar sem Docker, prepare e inicie o
[backend](executando-o-backend.md) e o [frontend](executando-o-frontend.md) em
terminais separados.
