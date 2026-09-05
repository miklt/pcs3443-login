# Executando o backend

## Com Docker Compose

A partir da raiz do repositório, a stack completa é a opção mais simples:

```bash
docker compose --env-file infra/.env.dev -f infra/docker-compose.dev.yml up --build
```

Para iniciar apenas banco e backend:

```bash
docker compose --env-file infra/.env.dev -f infra/docker-compose.dev.yml up --build db backend
```

O backend fica em:

- API: http://localhost:8000;
- Swagger UI: http://localhost:8000/docs;
- OpenAPI: http://localhost:8000/openapi.json;
- healthcheck: http://localhost:8000/health;
- status legado: http://localhost:8000/status.

O diretório `backend/app` é montado no contêiner e o Uvicorn usa `--reload`.

## Sem Docker

Na pasta `backend`:

```bash
python3.14 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
cp .env.example .env
uvicorn app.main:app --reload --port 8000
```

No Windows, ative o ambiente com
`.\.venv\Scripts\Activate.ps1`. O `.env.example` usa SQLite em
`backend/data.db` e traz as demais configurações necessárias.

Se frontend e backend forem iniciados diretamente na máquina, confirme:

```dotenv
DATABASE_URL=sqlite:///./data.db
JWT_SECRET_KEY=segredo-troque-em-producao
BACKEND_CORS_ORIGINS=["http://localhost:3000"]
```

Use o mesmo valor no `JWT_SECRET` do frontend.

## Testes unitários e de API

Com o ambiente virtual ativo:

```bash
python -m pip install -r requirements-dev.txt
PYTHONPATH=. pytest tests -q
```

No PowerShell:

```powershell
$env:PYTHONPATH = "."
pytest tests -q
```

Os testes usam bancos SQLite temporários e verificam cadastro, duplicidade,
login, tokens, consulta, logout, refresh e remoção.

## Teste integrado da stack Docker

Com os três serviços em execução, rode da raiz do repositório:

```bash
python3 infra/tests/e2e_dev.py
```

O script usa somente a biblioteca padrão do Python e realiza 19 verificações no
backend, no BFF do frontend, nas páginas e no PostgreSQL. Os usuários criados
pelo teste são removidos ao final.
