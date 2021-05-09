# Docker Class
Aprenda o que é Docker e Docker Compose, e como utilizá-los.

![Docker Logo](./assets/docker.png)

## Sumário Docker
* [O que é Docker](#o-que-é-docker)
* [Como o Docker funciona](#como-o-docker-funciona)
* [Por que usar o Docker](#por-que-usar-o-docker)
* [Instalando o Docker](#instalando-o-docker)
* [Comandos mais usados no Docker](#comandos-mais-usados-no-docker)
* [Docker na prática](#docker-na-prática)

## Sumário Docker Compose
* [O que é Docker Compose](#o-que-é-docker-compose)
* [Como o Docker Compose funciona](#como-o-docker-compose-funciona)
* [Por que usar o Docker Compose](#por-que-usar-o-docker-compose)
* [Instalando o Docker Compose](#instalando-o-docker-compose)
* [Comandos mais usados no Docker Compose](#comandos-mais-usados-no-docker-compose)
* [Docker Compose na prática](#docker-compose-na-prática)

## O que é Docker
O Docker é uma plataforma de software que permite a criação, o teste e a implantação de aplicações rapidamente. O Docker cria pacotes de software em unidades padronizadas chamadas de contêineres que têm tudo o que o software precisa para ser executado, inclusive bibliotecas, ferramentas de sistema, código e runtime. Ao usar o Docker, é possível implantar e escalar rapidamente aplicações em qualquer ambiente e ter a certeza de que o seu código será executado.

## Como o Docker funciona
O Docker permite executar o código de maneira padronizada. O Docker é um sistema operacional para contêineres. Da mesma maneira que uma máquina virtual virtualiza (desfaz a necessidade de gerenciar diretamente) o hardware do servidor, os contêineres virtualizam o sistema operacional de um servidor. O Docker é instalado em cada servidor e apresenta comandos simples que você pode usar para criar, iniciar ou interromper contêineres.  
O contêiner sempre será criado à partir de uma imagem. Uma imagem pode ser baixada à partir do Docker Hub, ou pode ser criada à partir de um Dockerfile.

## Por que usar o Docker
Ao usar o Docker, é possível enviar o código com mais rapidez, padronizar as operações de aplicativo, mover o código com facilidade e economizar, melhorando a utilização de recursos. Com o Docker, você tem um único objeto que pode ser executado com segurança em qualquer lugar. A sintaxe simples e direta do Docker possibilita o controle total. A ampla adoção significa que o Docker disponibiliza um ecossistema reforçado de ferramentas e aplicações prontas para uso. Docker resolve o famoso problema (na minha máquina funciona).

## Instalando o Docker
Para instalar o Docker no Windows:
> https://desktop.docker.com/win/stable/amd64/Docker%20Desktop%20Installer.exe

Para instalar o Docker no Linux (copia tudo e cola no terminal):
```bash
sudo apt install -y apt-transport-https ca-certificates curl gnupg software-properties-common && \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && \
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" && \
sudo apt install -y docker-ce && \
sudo systemctl start docker && sudo systemctl enable docker
```

Verificando se o docker foi instalado, execute o seguinte comando no terminal:
```bash
docker --version
```

## Comandos mais usados no Docker
```bash
docker ps # Lista apenas os containers que estão em execução
docker ps -a # Lista todos os containers
docker images # Lista todas as imagens
docker rm <container_id> # Remove o container pelo ID
docker rmi <image_id> # Remove a imagem pelo ID
docker build -f Dockerfile -t image-name . # Cria uma imagem a partir de um Dockerfile, a flag -f indica o caminho do arquivo Dockerfile e a flag -t a tag(nome) da imagem, o ponto ao final representa o contexto em que ela deve ser buildada, ou seja, a partir da pasta em que está localizada
docker run -d --name <container_name> -p 8080:80 <image_name> # Cria e executa um contẽiner a partir de uma imagem. A flag -d indica que será executado em background e a flag -p faz o roteamento da porta
docker start <container_id> # Inicia um container a partir do ID
docker stop <container_id> # Encerra a execução de um container pelo ID
```

## O que é Docker Compose
O Docker Compose é um orquestrador de contêineres Docker. Ou seja, ele rege como os contêineres específicados no arquivo de configuração do Docker Compose devem se comportar.  
O Docker Compose é composto por serviços (contêineres), e o uso dele tem o propósito de utilizar vários contêineres em uma mesma network, permitindo a comunicação entre os contêineres.

## Como o Docker Compose funciona
À partir de um arquivo yml seguindo a sintáxe de configuração do Docker Compose é possível orquestrar seus contêires através de um único comando. Resumindo, ao invés de subir um contêiner por vez, você pode subir 4 de umas vez resolve toda sua infraestrutura de desenvolvimento sempre perder tempo.  
O contêiner sempre será criado à partir de uma imagem. Uma imagem pode ser baixada à partir do Docker Hub, ou pode ser criada à partir de um Dockerfile.

## Por que usar o Docker Compose
Ao usar o Docker Compose você ganha tempo, é muito mais produtivo. É excelente por criar uma comunicação entre os contêineres por default, tem uma ampla possibilidade de configuração automizando ainda mais seu ambiente de desenvolvimento e além disso, da mesma maneira que você sobe vários contêineres de uma vez, vocẽ também os para.

## Instalando Docker Compose
Geralmente o Docker Compose é instalado em conjunto com o Docker, não precisa se preocupar.  
Verificando se o docker-compose foi instalado, execute o seguinte comando no terminal:
```bash
docker-compose --version
```

## Comandos mais usados
```bash
docker-compose up # Executa todos os contêineres disponíveis na configuração do arquivo
docker-compose up -d # Executa todos os contêineres disponíveis na configuração do arquivo, porém, executa em background, não lockando o terminal
docker-compose up nome-do-servico # Executa o contêiner que possui o nome passado como parâmetro
docker-compose stop # Para a execução de todos os contêineres disponíveis na configuração do arquivo
docker-compose stop nome-do-servico # Para a execução do contêiner que possui o nome passado como parâmetro
docker-compose rm # Remove todos os contêineres explicítados no arquivo
```

## Docker na prática
Nesse hands on, criaremos uma imagem Docker à partir do nosso [Dockerfile](./Dockerfile) (presente neste repositório), e criaremos um contêiner a partir da nossa nova imagem, expondo nossa página html na porta 8080.  

Em uma terminal de sua preferência, se posicione na raiz do diretório docker-class e execute:
```bash
# Esse comando indica que queremos criar uma imagem à partir do arquivo Dockerfile com a tag nginx-html, indicando o contexto atual através do (.)
docker build -f Dockerfile -t nginx-html .
```

Agora verifique se a nova imagem foi criada:
```bash
docker images # Deve aparecer entre as imagens listadas o nome nginx-html
```

Agora vamos criar e executar um contêiner à partir da imagem que acabamos de criar:
```bash
# Esse comando indica que queremos criar e executar em background um contêiner com o nome docker-class à partir da imagem que criamos à pouco
docker run -d --name docker-class -p 8080:80 nginx-html
```

Para saber o contêiner está em execução, execute o seguinte comando:
```bash
docker ps # Você verá algo parecido com o log abaixo
# CONTAINER ID   IMAGE        COMMAND                  CREATED         STATUS         PORTS                                   NAMES
# c2a8068d1bbf   nginx-html   "/docker-entrypoint.…"   5 seconds ago   Up 2 seconds   0.0.0.0:8080->80/tcp, :::8080->80/tcp   docker-class
```

Acesse a seguinte URL e deverá ver `Hello Docker` na sua tela:
> http://localhost:8080/

## Docker Compose na prática
Nesse hands on, criaremos dois contêineres à partir do nosso [docker-compose.yml](./docker-compose.yml) (presente neste repositório), o `nginx-from-local` será criado à partir do nosso [Dockerfile](./Dockerfile), expondo nossa página html na porta 8080, e o `nginx-from-docker-hub` será criado à partir da imagem do nginx no DockerHub, e através do volumes, copiaremos a pasta compose para dentro do contêiner, expondo nossa página html na porta 8081, ou seja, o html será diferente e a porta também.  

Em uma terminal de sua preferência, se posicione na raiz do diretório docker-class e execute:
```bash
# Esse comando irá subir todos os contêires listados dentro de services no arquivo docker-compose.yml
docker-compose up
```

Agora verifique se a nova imagem foi criada a partir do docker-compose, abra um novo terminal e execute:
```bash
docker images # Deve aparecer entre as imagens listadas o nome docker-class_nginx-from-local
```

Verifique também se os contêineres estão em execução, execute o seguinte comando:
```bash
docker ps # Você verá algo parecido com o log abaixo
# CONTAINER ID   IMAGE                           COMMAND                  CREATED         STATUS          PORTS                                   NAMES
# 3177349d6e23   nginx:alpine                    "/docker-entrypoint.…"   5 minutes ago   Up 37 seconds   0.0.0.0:8081->80/tcp, :::8081->80/tcp   nginx-from-docker-hub
# 5a1750e92a67   docker-class_nginx-from-local   "/docker-entrypoint.…"   5 minutes ago   Up 37 seconds   0.0.0.0:8080->80/tcp, :::8080->80/tcp   nginx-from-local

```

Acesse as seguinte URLs e deverá ver `Hello Docker` na porta 8080 e `Hello Docker Compose` na porta 8081:
> http://localhost:8080/  
> http://localhost:8081/

Para encerrar a execução, no termina em que executou `docker-compose up`, pressione `CTRL+C`
