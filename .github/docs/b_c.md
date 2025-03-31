# Bloco C - Redes e Volumes

## Sumário

- [Bloco C - Redes e Volumes](#bloco-c---redes-e-volumes)
  - [Sumário](#sumário)
  - [Links Importantes](#links-importantes)
  - [Conceitos e Explicações](#conceitos-e-explicações)
    - [CLI](#cli)
  - [Conceitos](#conceitos)
    - [Como trabalhar com arquivos dentro de um Container?](#como-trabalhar-com-arquivos-dentro-de-um-container)
    - [O que são Volumes?](#o-que-são-volumes)
      - [Lidando com Volumes em Docker](#lidando-com-volumes-em-docker)

## Links Importantes

## Conceitos e Explicações

### CLI

```bash
# exibir lista de conexões com o Docker
$ docker network ls

# criar conexão com o Docker
$ docker network create [nome-conexao]

# remover uma conexão
$ docker network rm [nome-conexao]

# associar uma rede a um container
$ docker network connect [ID_REDE] [ID_CONTAINER]

# inspecionar rede conectada
$ docker network inspect [ID_REDE]

# inspecionar container
$ docker container inspect [ID_CONTAINER]

# acessar arquivos do container
$ docker exec -it [ID_CONTAINER] bash

# criar volume 
$ docker volume create [nome-volume]

# remover volume 
$ docker volume create [nome-volume]

# inspecionar volume
$ docker volume inspect [nome-volume]
```

## Conceitos

### Como trabalhar com arquivos dentro de um Container?

Para trabalhar com arquivos dentro de um contêiner Docker, você tem algumas opções:

1. **Copiar arquivos para dentro ou fora do contêiner**: Você pode usar os comandos `docker cp` para copiar arquivos entre o host e o contêiner.

   Exemplo:

   ```bash
   # Copiando um arquivo do host para o contêiner
   docker cp arquivo.txt meu-container:/caminho/destino/arquivo.txt

   # Copiando um arquivo do contêiner para o host
   docker cp meu-container:/caminho/arquivo.txt arquivo.txt
   ```

2. **Montar volumes**: Esta é uma maneira mais flexível de trabalhar com arquivos, onde você monta um diretório do host dentro do contêiner. Qualquer alteração feita no diretório dentro do contêiner será refletida no diretório do host e vice-versa.

   Exemplo:

   ```bash
   docker run -d --name meu-container -v /caminho/no/host:/caminho/no/contêiner imagem
   ```

3. **Usar comandos dentro do contêiner**: Você também pode acessar um shell dentro do contêiner usando `docker exec` e, em seguida, executar comandos de manipulação de arquivo dentro do ambiente do contêiner.

   Exemplo:

   ```bash
   docker exec -it meu-container bash
   # Dentro do contêiner, você pode usar comandos como cp, mv, rm, mkdir, etc.
   cp /caminho/arquivo.txt /caminho/destino/arquivo.txt
   ```

4. **Construir uma imagem com os arquivos incorporados**: Se você tem arquivos que deseja que estejam disponíveis em um contêiner, pode incluí-los em uma imagem Docker usando um Dockerfile.

   Exemplo de Dockerfile:

   ```bash
   FROM ubuntu:latest
   COPY arquivo.txt /caminho/no/contêiner/arquivo.txt
   ```

   Em seguida, você pode construir a imagem com `docker build` e executar um contêiner a partir dela.

Essas são algumas maneiras comuns de lidar com arquivos dentro de contêineres Docker. A escolha entre elas dependerá das suas necessidades específicas e da maneira como você deseja interagir com os arquivos.

### O que são Volumes?

Os volumes no Docker são diretórios ou arquivos especiais que residem fora do sistema de arquivos do contêiner. Eles são gerenciados pelo Docker e podem ser compartilhados e reutilizados por vários contêineres. Os volumes podem persistir dados, mesmo quando o contêiner que os utiliza não está em execução.

#### Lidando com Volumes em Docker

1. **Criando um volume**:

   Você pode criar um volume usando o comando `docker volume create`.

   ```bash
   docker volume create meu-volume
   ```

2. **Montando um volume em um contêiner**:

   Você pode montar um volume em um contêiner usando a opção `-v` ou `--mount` ao iniciar o contêiner.

   ```bash
   docker run -d --name meu-container -v meu-volume:/caminho/no/contêiner imagem
   ```

   ou

   ```bash
   docker run -d --name meu-container --mount source=meu-volume,target=/caminho/no/contêiner imagem
   ```

3. **Montando um diretório do host como volume**:

   Além de criar volumes dedicados, você também pode montar diretórios do host como volumes.

   ```bash
   docker run -d --name meu-container -v /caminho/no/host:/caminho/no/contêiner imagem
   ```

4. **Listando volumes**:

   Você pode listar todos os volumes disponíveis no sistema usando o comando `docker volume ls`.

   ```bash
   docker volume ls
   ```

5. **Removendo volumes**:

   Você pode remover volumes não utilizados com o comando `docker volume rm`.

   ```bash
   docker volume rm meu-volume
   ```

6. **Usando volumes em Dockerfile**:

   Você também pode definir volumes em um Dockerfile, indicando quais diretórios dentro do contêiner devem ser tratados como volumes.

   ```bash
   VOLUME /caminho/no/contêiner
   ```

Volumes são essenciais para muitos casos de uso do Docker, como persistência de dados, compartilhamento de arquivos entre contêineres e integração com sistemas de armazenamento externos. Eles oferecem uma maneira flexível e poderosa de lidar com o armazenamento de dados em contêineres Docker.
