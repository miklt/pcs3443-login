# Banco de dados (Postgresql)

## Pre-requisitos <a href="#user-content-pre-requisitos" id="user-content-pre-requisitos"></a>

1. Ter uma conta na plataforma Okteto
2. (opcional) Ter um ambiente gráfico para conexão ao banco de dados ([dbbeaver](https://dbeaver.io/), [datagrip ](https://www.jetbrains.com/pt-br/community/education/#students)ou o [pgAdmin](https://www.pgadmin.org/))

## Objetivo <a href="#user-content-objetivo" id="user-content-objetivo"></a>

Implantar no cluster um banco de dados sql e conectar-se a ele no ambiente de produção.

## Passos <a href="#user-content-passos" id="user-content-passos"></a>

1\. Logar na plataforma Okteto.

2\. Clicar em Deploy

3\. Escolher a opção "from Chart" e selecionar postgresql, depois clicar em "Deploy"

4\. A seguir aparecerá uma tela para configurar o nome de usuário, nome do banco de dados e senha. Mantenha os valores padrão se preferir. O tamanho de armazenamento oferecido é de 2GB, o que deve ser suficiente para o projeto. Clicar em "Deploy" novamente.

5\. Esperar até que o serviço esteja pronto.

Com os dados de conexão padrão:&#x20;

> * host: postgresql.\<nome-da-conta>.svc.cluster.local
> * port: 5432
> * user: okteto
> * password: okteto
> * database: okteto

Para que o backend consiga se conectar ao banco de dados, é preciso alterar a chave `SQLALCHEMY_DATABASE_URI`  do arquivo `.env` na pasta `backend` . Com os dados acima, ficaria:`SQLALCHEMY_DATABASE_URI=postgresql+psycopg2://okteto:okteto@postgresql.<nome-da-conta>.svc.cluster.local/okteto?client_encoding=utf8`

Para poder se conectar a partir do ambiente local de desenvolvimento, é preciso criar um tunel de conexão, de forma que o cliente (dBeaver, pgAdmin, datagrip ou outros) se conecte remotamente no servidor.\
Para isso, é preciso abrir o terminal e executar o seguinte comando:

`kubectl port-forward --namespace $(namespaceId) svc/postgresql 5432:5432` (Lembre-se de substituir $(namespaceId) pelo seu seu namespace)

Se tudo der certo, as conexões na porta 5432 do computador local serão encaminhadas para o servidor no cluster.

Para testar, podemos abrir o nosso cliente (dBeaver) e passar a url de conexão, trocando a parte: `postgresql.<nome-da-conta>.svc.cluster.local` por `localhost`
