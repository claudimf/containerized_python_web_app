# containerized_python_web_app

# Containerized Python Web App(conteinerização de scripts em Python)

👋 Olá, Seja Bem-vindo(a) ao Containerized Python(conteinerização de scripts em Python).

# Exigências

**:warning: Atenção:** É necessário que os desenvolvedores usem o Docker no seu ambiente de desenvolvimento.

- **🛠 Modo Desenvolvimento Docker**
    - :computer: [Linux Ubuntu LTS](https://ubuntu.com/download/desktop)
    - 🐳 [Docker](https://docs.docker.com/engine/installation/) Deve estar instalado.
    - 🐳 [Docker Compose](https://docs.docker.com/compose/) Deve estar instalado.
    - **💡 Dica:** [Documentação do Docker](https://docs.docker.com/)

# Instalando

## 🐳 Modo Desenvolvimento com Docker

Após instalar o docker e docker-compose, estando na pasta raiz do projeto, execute:

```sh
docker-compose up
```

Para se certificar que os seus containers subiram corretamente, todos os containers deve estar com o status `UP`, execute:

```sh
docker-compose ps -a
```

Para acessar o container da aplicação, execute:

```sh
docker-compose run --rm app bash
```

Para derrubar e subir a instância do docker novamente, execute:

```sh
docker-compose down && docker-compose up
```

🚀 :clap: Para visualizar o sistema basta acessar no navegador no endereço: [localhost:3000](http://localhost:3000)


# Criar a aplicação

1. Criar o arquivo [server.py](https://github.com/claudimf/containerized_python/blob/main/app/src/server.py)  com o seguinte conteúdo:


```sh
from flask import Flask


server = Flask(__name__)

@server.route("/")
def hello():
 return "Hello World!"

@server.route("/test_1")
def test_1():
 return 'test_1'

if __name__ == "__main__":
 server.run(host='0.0.0.0')
```

2. Colocar o arquivo server.py na estrutura abaixo:

```sh
Project
├─── web
├─── app
│ ├─── Dockerfile
│ ├─── requirements.txt
│ └─── src
│ └─── server.py
└─── db
```

3. No arquivo [requirements.txt](https://github.com/claudimf/containerized_python/blob/main/app/requirements.txt) adicionar o [Flask](https://flask.palletsprojects.com/en/1.1.x/):

```sh
Flask==1.1.1
```

4. Criar o arquivo [Dockerfile](https://github.com/claudimf/containerized_python/blob/main/app/Dockerfile) na pasta app com o seguinte conteúdo:

```sh
# set base image (host OS)
FROM python:3.8

# set the working directory in the container
WORKDIR /code

# copy the dependencies file to the working directory
COPY requirements.txt .

# install dependencies
RUN pip install -r requirements.txt

# copy the content of the local src directory to the working directory
COPY src/ .

# command to run on container start
CMD [ "python", "./server.py" ]
```
5. Criar o arquivo [docker-compose.yml](https://github.com/claudimf/containerized_python/blob/main/app/docker-compose.yml) na pasta app com o seguinte conteúdo: 

```sh
version: '3.3'
services:
  app:
    build: .
    volumes:
      - .:/src
    ports:
      - "3000:5000"
```

6. Na pasta app connstrua a aplicação no terminal com o comando:

```sh
docker-compose build
```

7. Suba o projeto no terminal com o comando:

```sh
docker-compose up
```

8. Para testar acesse as rotas:
- [localhost:3000](http://localhost:3000)
- [localhost:3000/test_1](http://localhost:3000/test_1)

Pronto a aplicação de teste está de pé, para derrubar use o comando:

```sh
docker-compose down
```

Espero que tenha conseguido subir uma simples aplicação Flask + Docker via docker-compose, caso haja dúvidas acesse as [Referências utilizadas](https://github.com/claudimf/containerized_python#refer%C3%AAncias-utilizadas).

# Referências utilizadas

[1° Containerized Python Development – Part 1](https://www.docker.com/blog/containerized-python-development-part-1//) 

[2° Project sample](https://github.com/aiordache/demos/tree/master/dockercon2020-demo)    