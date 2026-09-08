# Aplicação de Login - Labsoft

Esta documentação descreve o projeto de referência disponível em
[github.com/miklt/pcs3443-2021](https://github.com/miklt/pcs3443-2021).

O sistema demonstra uma aplicação web completa de cadastro e autenticação:

- frontend em Next.js 15, React 19, TypeScript e Tailwind CSS 4;
- backend REST em FastAPI, Python 3.14, SQLAlchemy 2 e Pydantic 2;
- senhas protegidas com bcrypt e autenticação por JSON Web Token (JWT);
- SQLite na execução local sem contêineres ou PostgreSQL 16 com Docker Compose;
- frontend implantado na Vercel e backend com PostgreSQL em servidor próprio.

A aplicação publicada está em
[pcs3443-2021.vercel.app](https://pcs3443-2021.vercel.app/).

## Login

1. O usuário informa `username` e `password` na página `/`.
2. O navegador envia os dados a `POST /api/login`, um Route Handler do Next.js.
3. O Route Handler chama `POST /login` no FastAPI pelo lado do servidor.
4. O backend procura o usuário, compara a senha com o hash bcrypt e, se as
   credenciais forem válidas, devolve um token de acesso e um token de
   renovação.
5. O frontend guarda somente o token de acesso no cookie `token`. O cookie é
   `httpOnly`, `sameSite=lax`, restrito ao caminho `/` e, em produção, `secure`.
6. O usuário é redirecionado para `/profile`. A página valida a assinatura e o
   prazo do JWT no servidor e exibe `username`, `email` e o identificador `jti`.

Por padrão, o token de acesso e o cookie expiram em 30 minutos. O backend
também emite um refresh token válido por sete dias, mas a interface atual não o
armazena nem executa renovação automática.

### Falhas de login e sessão

- campos vazios são rejeitados pela validação do formulário;
- credenciais incorretas produzem HTTP 401;
- falha de conexão com o backend é apresentada como erro de rede;
- sem o cookie, o middleware redireciona `/profile` para `/`;
- token expirado, inválido ou assinado com outro segredo impede a exibição do
  perfil.

O valor de `JWT_SECRET` no frontend deve ser exatamente igual ao
`JWT_SECRET_KEY` do backend.

## Cadastro

1. Em `/register`, o usuário informa nome de usuário, e-mail e senha.
2. O formulário valida os dados com React Hook Form e Zod.
3. `POST /api/register` encaminha a requisição para `POST /register` no backend.
4. O Pydantic valida o payload; nome e e-mail devem ser únicos.
5. A senha é transformada em hash bcrypt e o SQLAlchemy persiste o usuário.
6. O backend responde HTTP 201 e o frontend retorna à tela de login.

O nome de usuário e o e-mail aceitam até 80 caracteres; a senha aceita de 1 a
128 caracteres e o e-mail precisa ter formato válido.

## Logout

O botão **Deslogar** chama `POST /api/logout`, que apaga o cookie e redireciona
para a tela de login. Como os JWTs são stateless, o backend não mantém uma lista
de tokens revogados: um token copiado antes do logout continua válido até
expirar.

## Próximos passos

- Consulte [Arquitetura](arquitetura/arquitetura.md) para entender os
  componentes e a comunicação.
- Siga [Visão geral do ambiente](ambiente/ambiente-de-desenvolvimento.md) e
  [Obtendo o código](execucao/codigo.md) para executar o sistema.
- Use as páginas de [Implantação](implantacao/ambiente-de-producao-1.md) para
  publicar a aplicação.
