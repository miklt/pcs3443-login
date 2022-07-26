# Projeto do Backend

## Backend

O backend foi desenvolido em Python e foram usados os pacotes Flask-Restful, flask-sqlAlchemy e Marshmallow. Flask-Restful é uma biblioteca que facilita o desenvolvimento de aplicações RESTful, ela se encarrega de expor os endpoints da aplicação e interagir com o protocolo HTTP. A biblioteca flask-sqlalchemy é usada para fazer um mapeamento objeto-relacional para de classes python para bancos relacionais. Esta aplicação usa Postgresql em produção e também pode usar Sqlite em desenvolvimento. A biblioteca Marshmallow é responsável por facilitar a serialização e deserialização de objetos python no formato JSON. Ainda, este projeto usa a bibliotecas bcrypt para criptografar os passwords persistidos no banco de dados e a biblioteca flask-jwt-extended para criar tokens de autenticação. O seguinte diagrama de classes ilustra estas relações.

![](../.gitbook/assets/backend\_backend.svg)

### Funcionamento

O seguinte diagrama de sequência ilustra o funcionamento do login no lado do servidor.

![](<../.gitbook/assets/backend\_login\_sequence (1).svg>)

{% file src="../.gitbook/assets/backend_login_sequence (1).svg" %}
Backend\_login\_sequência
{% endfile %}

