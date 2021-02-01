# Containerized Python Web App(conteinerização de aplicação Web em Python)

👋 Olá, Seja Bem-vindo(a) ao Containerized Python Web App(conteinerização de aplicação Web em Python).

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

1. Criar a estrutura abaixo de diretórios e arquivos:

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

2. Confira aqui o que a configuração do arquivo [server.py](https://github.com/claudimf/containerized_python_web_app/blob/main/app/src/server.py) com o seguinte conteúdo:

3. No arquivo [requirements.txt](https://github.com/claudimf/containerized_python_web_app/blob/main/app/requirements.txt) adicionar o [Flask](https://flask.palletsprojects.com/en/1.1.x/) e o [MySql Connector](https://flask.palletsprojects.com/en/1.1.x/):

```sh
Flask==1.1.1
mysql-connector==2.2.9
```

4. Criar o arquivo [Dockerfile](https://github.com/claudimf/containerized_python_web_app/blob/main/app/Dockerfile) na pasta app com o seguinte conteúdo:

```sh
FROM python:3.8-alpine
WORKDIR /src
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY ./src /src
EXPOSE 5000
CMD python server.py
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

Pronto a aplicação de teste está de pé, para derrubar use o comando:

```sh
docker-compose down
```

Espero que tenha conseguido subir uma simples aplicação Flask + Docker via docker-compose, caso haja dúvidas acesse as [Referências utilizadas](https://github.com/claudimf/containerized_python#refer%C3%AAncias-utilizadas).

# Referências utilizadas


[1° Conteinerização de scripts em Python](https://github.com/claudimf/containerized_python) 

[2° Containerized Python Development – Part 2](https://www.docker.com/blog/containerized-python-development-part-2/)  

[3° Containerized Python Development – Part 3](https://www.docker.com/blog/containerized-python-development-part-3/)  

[4° Project sample](https://github.com/aiordache/demos/tree/master/dockercon2020-demo)