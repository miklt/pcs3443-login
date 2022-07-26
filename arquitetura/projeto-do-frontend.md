# Projeto do Frontend

## Frontend

O frontend foi desenvolvido usando [Next.js](https://nextjs.org/) que é um framework para construir aplicações em [React](https://pt-br.reactjs.org/).

{% hint style="info" %}
O uso de um framework pode facilitar algumas escolhas em relação ao desenvolvimento do projeto.
{% endhint %}

Uma das principais características do `next.js`consiste em que os arquivos dentro da pasta `pages` já se tornam urls dentro da nossa aplicação. E, se incluirmos uma pasta `api`dentro da pasta `pages`, os arquivos que estiverem nela também poderão ser [`endpoints`](https://nextjs.org/docs/api-routes/introduction) da aplicação e rodarão do lado do servidor. Isto é muito útil se quisermos acessar bancos de dados ou aplicações externas.

O seguinte diagrama de classes ilustra a tela de login.

![](<../.gitbook/assets/frontend\_Login (1).svg>)



### Funcionamento

O seguinte diagrama de sequência mostra a funcionalidade de Login.&#x20;

![](../.gitbook/assets/frontend\_Login.svg)

{% file src="../.gitbook/assets/frontend_Login.svg" %}
Para melhor visualização, baixe ele aqui
{% endfile %}

##
