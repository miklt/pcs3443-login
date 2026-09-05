# JavaScript e TypeScript

O frontend é escrito em TypeScript, que acrescenta verificação estática de tipos
ao JavaScript. O `tsconfig.json` ativa o modo `strict` e o alias `@/*`.

## Fundamentos

- [Guia de JavaScript — MDN](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide);
- [JavaScript assíncrono — MDN](https://developer.mozilla.org/pt-BR/docs/Learn_web_development/Extensions/Async_JS);
- [Manual do TypeScript](https://www.typescriptlang.org/docs/handbook/);
- [Referência do TSConfig](https://www.typescriptlang.org/tsconfig/).

## Bibliotecas usadas

- [Axios](https://axios-http.com/docs/intro), cliente HTTP dos Route Handlers;
- [Zod](https://zod.dev/), schemas dos formulários;
- [React Hook Form](https://react-hook-form.com/get-started), estado e validação
  dos formulários;
- [jose](https://github.com/panva/jose), verificação do JWT no servidor Next.js;
- [Cypress](https://docs.cypress.io/), testes end-to-end.

Para verificar o código TypeScript:

```bash
cd frontend
npm run typecheck
```
