# Frontend

O frontend é implantado na Vercel a partir da pasta `frontend` do repositório.
O backend e o PostgreSQL não são implantados na Vercel.

## Criar o projeto

1. Importe `miklt/pcs3443-2021` no painel da Vercel.
2. Em **Root Directory**, escolha `frontend`.
3. Confirme que o framework detectado é Next.js.
4. Configure as variáveis de ambiente antes do primeiro deploy.

Como o código está em um monorepo, selecionar a raiz correta é essencial: o
`package.json` e o `package-lock.json` do frontend ficam nessa pasta.

## Variáveis de ambiente

Configure para **Production** e, se usar previews, também para **Preview**:

| Variável | Valor |
| --- | --- |
| `BACKEND_URL` | URL pública do FastAPI, preferencialmente HTTPS |
| `JWT_SECRET` | exatamente o mesmo `JWT_SECRET_KEY` usado pelo backend |

Exemplo:

```dotenv
BACKEND_URL=https://api.seu-dominio.example
JWT_SECRET=mesmo-segredo-forte-do-backend
```

Essas variáveis são consumidas apenas no servidor Next.js. Não use o prefixo
`NEXT_PUBLIC_`, pois isso exporia os valores ao bundle do navegador.

Os nomes antigos `URL_API_BACKEND` e `JWT_KEY` são aceitos como fallback, mas
novas configurações devem usar `BACKEND_URL` e `JWT_SECRET`.

## Integração com o backend

Inclua o domínio do frontend no `BACKEND_CORS_ORIGINS` usado pelo servidor:

```dotenv
BACKEND_CORS_ORIGINS=["https://seu-app.vercel.app"]
```

O fluxo normal é server-side: os Route Handlers da Vercel chamam o backend. Por
isso, `BACKEND_URL` precisa ser alcançável a partir da Internet e não pode ser
`localhost` nem o nome de serviço `backend` usado no Docker Compose.

Se as variáveis forem alteradas, faça um novo deploy; a mudança não modifica
deploys já existentes.

## Validação

Depois da publicação:

1. abra a URL da Vercel;
2. cadastre um usuário;
3. entre com as mesmas credenciais;
4. confirme o redirecionamento a `/profile` e os dados do JWT;
5. clique em **Deslogar** e confirme o retorno à tela de login;
6. no servidor, confira `/health` e os logs do backend se houver erro.

Falhas comuns:

- **ECONNREFUSED**: `BACKEND_URL` está incorreta ou inacessível;
- **Token inválido**: `JWT_SECRET` e `JWT_SECRET_KEY` são diferentes;
- perfil volta ao login: o cookie não foi criado ou não chegou à requisição;
- backend responde, mas cadastro falha: confira os logs e a conexão PostgreSQL.

Também existe uma imagem Docker de produção do frontend. Para auto-hospedá-la
junto do backend, use o profile opcional:

```bash
docker compose --env-file infra/.env.prod -f infra/docker-compose.prod.yml \
  --profile selfhost up -d
```

Nesse modo, `FRONTEND_PORT` define a porta publicada, 3000 por padrão.
