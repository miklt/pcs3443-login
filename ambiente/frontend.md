# Frontend

O frontend usa Node.js 24+, npm, Next.js 15 com App Router, React 19,
TypeScript 5, Tailwind CSS 4, React Hook Form e Zod.

## Preparação sem Docker

```bash
cd frontend
npm install
cp .env.example .env.local
```

Edite `.env.local`:

```dotenv
BACKEND_URL=http://localhost:8000
JWT_SECRET=segredo-troque-em-producao
```

`BACKEND_URL` é usada somente no servidor Next.js pelos Route Handlers.
`JWT_SECRET` valida o token na página de perfil e deve ser idêntica a
`JWT_SECRET_KEY` do backend.

Os nomes antigos `URL_API_BACKEND` e `JWT_KEY` ainda funcionam como fallback,
mas os nomes acima são os canônicos.

## Scripts npm

| Comando | Finalidade |
| --- | --- |
| `npm run dev` | servidor de desenvolvimento em http://localhost:3000 |
| `npm run build` | build de produção |
| `npm start` | inicia um build já gerado |
| `npm run lint` | executa o lint configurado pelo Next.js |
| `npm run typecheck` | verifica os tipos sem gerar arquivos |
| `npm run cypress:open` | abre a interface do Cypress |
| `npm run cypress:run` | executa os testes end-to-end |
