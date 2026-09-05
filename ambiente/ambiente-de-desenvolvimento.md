# Visão geral

A forma recomendada de executar o projeto é com Docker Compose. Ela inicia
PostgreSQL 16, FastAPI e Next.js com um único comando e não exige instalar
Python, Node.js ou PostgreSQL diretamente na máquina.

## Opção recomendada: Docker

Instale:

- [Git](https://git-scm.com/downloads);
- [Docker Desktop](https://docs.docker.com/desktop/) no Windows ou macOS, ou
  Docker Engine com o plugin Compose no Linux;
- um editor de código, como o
  [Visual Studio Code](https://code.visualstudio.com/), se desejar alterar o
  projeto.

Confirme a instalação:

```bash
git --version
docker --version
docker compose version
```

O ambiente de desenvolvimento definido em `infra/docker-compose.dev.yml` usa:

| Serviço | Tecnologia | Endereço local |
| --- | --- | --- |
| `frontend` | Next.js 15 / React 19 | http://localhost:3000 |
| `backend` | FastAPI / Uvicorn | http://localhost:8000 |
| `db` | PostgreSQL 16 | localhost:5432 |

## Opção sem Docker

Para executar os componentes diretamente, instale também:

- Python 3.14 e `venv`;
- Node.js 24 ou superior, com npm;
- PostgreSQL, apenas se não quiser usar o SQLite local.

O backend sem Docker usa SQLite por padrão. As instruções detalhadas estão em
[Backend](backend.md), [Frontend](frontend.md) e na seção
[Execução](../execucao/codigo.md).

{% hint style="warning" %}
Os valores de `infra/.env.dev` são públicos e deliberadamente inseguros. Use-os
somente no computador de desenvolvimento; nunca os copie para produção.
{% endhint %}
