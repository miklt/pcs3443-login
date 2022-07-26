# Apresentação

A seguinte documentação descreve o Componente de Login, cujo código fonte está presente no repositório [https://github.com/miklt/pcs3443-2021](https://github.com/miklt/pcs3443-2021)

Este projeto foi criado com o intuito de apresentar o desenvolvimento de uma aplicação web composta de um frontend e um backend que se comunicam via o protocolo REST. Uma demo está rodando no seguinte link [https://pcs3443-2021.vercel.app/](https://pcs3443-2021.vercel.app/)&#x20;

## Login

* O usuário digita o login e senha no frontend e envia esses dados ao backend. Se houver um match no banco de dados, o backend retorna um token JWT que contém informações do usuário.&#x20;
* Se o token for assinado com a mesma chave configurada no frontend, o token é armazendo num cookie e o usuário é redirecionado à tela de perfil apresentadas e o token é armazendo num cookie durante a sessão do usuário.

![Tela de login](.gitbook/assets/tela\_login.png)

![Tela de Perfil](.gitbook/assets/tela\_perfil.png)

## Exceções

* Caso os dados digitados não pertençam a algum registro o backend retorna um erro HTTP 400.
* Caso o token fornecido pelo backend for assinado com uma chave diferente da do frontend, o frontend apresenta um erro e retorna para a tela principal.
* O token tem um tempo de expiração de 15 minutos

![](.gitbook/assets/tela\_erro\_perfil.png)



## Cadastro

* O usuário digita o login, email e senha no frontend e envia esses dados ao backend por meio de uma requisição POST contendo um payload em JSON.&#x20;
* O backend recebe a requisição, obtem o login, email e criptografa a senha.&#x20;
* O backend armazena os dados no banco de dados
* O backend retorna o código HTTP 201, indicando sucesso na operação
* O frontend recebe o retorno do backend e redireciona o usuário para a tela de login.

![](.gitbook/assets/tela\_cadastro.png)
