# Executando o Backend

## Instalação&#x20;

Com o repositório clonado no seu computador, volte ao terminal e execute os seguintes comandos.&#x20;

```
cd backend
pipenv shell
pipenv install
```

Depois de instalar as dependências do projeto é preciso criar o arquivo `.env`arquivo `.env.example` dentro da pasta backend.&#x20;

```bash
cp .env.example .env
```

E depois, deixar o arquivo .env com os seguintes dados:

```
JWT_SECRET_KEY=segredo
SQLALCHEMY_DATABASE_URI=sqlite:///data.db
```

A seguir, executar o seguinte comando para rodar o backend:

```
python app.py
```

No windows pode aparecer uma mensagem do firewall solicitando acesso a sua rede. Permita o acesso. Depois o programa deve estar em execução.

![](../.gitbook/assets/flask\_run.PNG)

