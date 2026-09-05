# Backend

O backend atual é uma API FastAPI escrita para Python 3.14. O projeto não usa
mais Flask nem Pipenv.

## Dependências principais

| Pacote | Responsabilidade |
| --- | --- |
| FastAPI e Uvicorn | API HTTP e servidor ASGI |
| SQLAlchemy 2 | mapeamento objeto-relacional e sessões de banco |
| Pydantic 2 e pydantic-settings | validação dos payloads e configuração |
| psycopg2-binary | conexão com PostgreSQL |
| PyJWT | criação e validação dos tokens HS256 |
| bcrypt | hash e verificação de senhas |

As dependências de execução estão em `backend/requirements.txt` e também são
declaradas em `backend/pyproject.toml`. `backend/requirements-dev.txt` adiciona
pytest, HTTPX e Ruff.

## Preparação sem Docker

No macOS ou Linux:

```bash
cd backend
python3.14 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
cp .env.example .env
```

No PowerShell:

```powershell
cd backend
py -3.14 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
Copy-Item .env.example .env
```

O arquivo `.env.example` já configura SQLite. Para desenvolvimento com
PostgreSQL, altere `DATABASE_URL` para uma URL compatível com o SQLAlchemy.

## Variáveis do backend

| Variável | Padrão/finalidade |
| --- | --- |
| `DATABASE_URL` | `sqlite:///./data.db`; URL canônica do banco |
| `SQLALCHEMY_DATABASE_URI` | nome legado aceito se `DATABASE_URL` não existir |
| `JWT_SECRET_KEY` | segredo de assinatura, igual ao `JWT_SECRET` do frontend |
| `JWT_ALGORITHM` | `HS256` |
| `ACCESS_TOKEN_EXPIRE_MINUTES` | 30 |
| `REFRESH_TOKEN_EXPIRE_DAYS` | 7 |
| `BACKEND_CORS_ORIGINS` | lista JSON, CSV ou uma origem permitida |

Em produção, gere um segredo forte e configure explicitamente as origens CORS.
