# Banco de dados PostgreSQL

Em produção, o PostgreSQL 16 roda no mesmo servidor do backend, no serviço `db`
definido em `infra/docker-compose.prod.yml`. A porta 5432 não é publicada no
host: somente o contêiner `backend` acessa o banco pela rede interna.

## Configuração

O arquivo `infra/.env.prod` não é versionado. No deploy automatizado ele é
gerado no servidor a partir dos GitHub Secrets. Para uma instalação manual,
crie-o a partir do modelo:

```bash
cp infra/.env.example infra/.env.prod
```

Defina pelo menos:

```dotenv
POSTGRES_USER=login
POSTGRES_PASSWORD=uma-senha-forte
POSTGRES_DB=pcs3443
JWT_SECRET_KEY=um-segredo-jwt-forte
BACKEND_CORS_ORIGINS=["https://seu-app.vercel.app"]
BACKEND_PORT=8000
```

O Compose monta internamente a URL:

```text
postgresql+psycopg2://POSTGRES_USER:POSTGRES_PASSWORD@db/POSTGRES_DB
```

Não é necessário definir `DATABASE_URL` no arquivo: o serviço `backend` a
constrói com os valores acima.

## Inicialização e persistência

Ao iniciar, o FastAPI executa `Base.metadata.create_all` e cria a tabela
`users` caso ela ainda não exista. O projeto não usa Alembic ou outro sistema de
migrações; mudanças futuras no modelo exigirão uma estratégia de migração.

Os dados ficam no volume nomeado `pgdata-prod`. Recriar o contêiner não apaga o
volume.

{% hint style="danger" %}
Não execute `docker compose down -v` em produção: a opção `-v` remove o volume
do PostgreSQL e seus dados.
{% endhint %}

## Estado e acesso administrativo

No servidor, a partir da raiz do repositório:

```bash
docker compose --env-file infra/.env.prod -f infra/docker-compose.prod.yml ps
docker compose --env-file infra/.env.prod -f infra/docker-compose.prod.yml logs -f db
docker compose --env-file infra/.env.prod -f infra/docker-compose.prod.yml exec db \
  psql -U login -d pcs3443
```

Se você alterar `POSTGRES_USER` ou `POSTGRES_DB`, ajuste os dois últimos
argumentos do `psql`.

Para listar usuários sem expor hashes:

```sql
SELECT id, username, email FROM users ORDER BY id;
```

## Backup

Exemplo de backup lógico no servidor:

```bash
docker compose --env-file infra/.env.prod -f infra/docker-compose.prod.yml exec db \
  pg_dump -U login pcs3443 > backup-$(date +%F).sql
```

Proteja o arquivo gerado e teste periodicamente a restauração em outro banco.
O repositório fornece o comando de backup como operação básica, mas não agenda
backups nem envia cópias para armazenamento externo.
