# Bloco B - Criando nossa primeira imagem

## Sumário

- [Bloco B - Criando nossa primeira imagem](#bloco-b---criando-nossa-primeira-imagem)
  - [Sumário](#sumário)
  - [Links importantes](#links-importantes)
  - [Conceitos e Explicações](#conceitos-e-explicações)
    - [CLI](#cli)

## Links importantes

## Conceitos e Explicações

### CLI

```bash
# criar imagem baseada no script do Dockerfile
$ docker build -t [name-image] .

# mostrar detalhes da imagem criada
$ docker image ls [name-image]

# mostrar log de criação e uso da imagem
$ docker image history [name-image]

# subir container (--rm: deleta após uso, -p: port)
$ docker run --rm -p 3000:3000 [name-image]

# subir container (-p: port, -d: execução em background)
$ docker run -p 3000:3000 -d [name-image]

# listar containers em execução
$ docker ps

# parar container
$ docker stop [CONTAINER_ID]

# iniciar container
$ docker start [CONTAINER_ID]

# listar log de atividades do container
$ docker logs [CONTAINER_ID]

# remover uma imagem ou um container
$ docker rm [IMAGE_ID]
$ docker rm [CONTAINER_ID]

# baixar uma imagem do Docker Hub ou de um registro de contêiner.
$ docker pull [IMAGE_NAME:TAG]
# exemplo: docker pull ubuntu:latest
```
