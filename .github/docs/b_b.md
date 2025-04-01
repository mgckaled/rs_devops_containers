# Bloco B - Criando nossa primeira imagem

## Sumário

- [Bloco B - Criando nossa primeira imagem](#bloco-b---criando-nossa-primeira-imagem)
  - [Sumário](#sumário)
  - [Links importantes](#links-importantes)
  - [Conceitos e Explicações](#conceitos-e-explicações)
    - [Principais instruções do Dockerfile](#principais-instruções-do-dockerfile)
    - [CLI](#cli)
  - [Aulas](#aulas)
    - [Estrutura de um Dockerfile](#estrutura-de-um-dockerfile)
    - [Rodando Nosso Container](#rodando-nosso-container)
    - [Melhorias e Otimizações na Nossa Imagem](#melhorias-e-otimizações-na-nossa-imagem)

## Links importantes

## Conceitos e Explicações

### Principais instruções do Dockerfile

O Dockerfile é um arquivo de texto simples que contém uma lista de instruções que o Docker usa para criar uma imagem de contêiner. Aqui estão os principais comandos que você usará ao trabalhar com Dockerfile, junto com exemplos:

1. **FROM**:
   - Descrição: Especifica a imagem base que será usada para construir a nova imagem.
   - Exemplo: `FROM ubuntu:20.04`

2. **RUN**:
   - Descrição: Executa um comando dentro do contêiner durante o processo de construção da imagem.
   - Exemplo: `RUN apt-get update && apt-get install -y python3`

3. **COPY**:
   - Descrição: Copia arquivos ou diretórios do sistema de arquivos local para dentro do contêiner.
   - Exemplo: `COPY app.py /app/`

4. **ADD**:
   - Descrição: Similar ao COPY, mas com suporte a URLs e arquivos compactados, que são automaticamente descompactados.
   - Exemplo: `ADD https://example.com/file.txt /file.txt`

5. **WORKDIR**:
   - Descrição: Define o diretório de trabalho para todas as instruções subsequentes.
   - Exemplo: `WORKDIR /app`

6. **CMD**:
   - Descrição: Especifica o comando padrão a ser executado quando um contêiner for iniciado a partir da imagem.
   - Exemplo: `CMD ["python3", "app.py"]`

7. **EXPOSE**:
   - Descrição: Informa ao Docker que o contêiner escuta em portas específicas em tempo de execução.
   - Exemplo: `EXPOSE 80`

8. **ENV**:
   - Descrição: Define variáveis de ambiente no contêiner.
   - Exemplo: `ENV ENVIRONMENT=production`

9. **ARG**:
   - Descrição: Define argumentos que podem ser passados durante a construção da imagem.
   - Exemplo: `ARG VERSION=latest`

10. **RUN**:
    - Descrição: Executa comandos durante a construção da imagem. Pode ser usado em conjunto com os argumentos definidos com o **ARG**.
    - Exemplo: `RUN echo "Version: $VERSION"`

Aqui está um exemplo completo de um Dockerfile para construir uma imagem simples de Python:

```Dockerfile
# Define a imagem base
FROM python:3.9-slim

# Define o diretório de trabalho
WORKDIR /app

# Copia os arquivos locais para o contêiner
COPY requirements.txt .
COPY app.py .

# Instala as dependências
RUN pip install --no-cache-dir -r requirements.txt

# Especifica o comando padrão a ser executado
CMD ["python", "app.py"]
```

Para construir uma imagem a partir deste Dockerfile, você pode usar o comando `docker build`. Supondo que este Dockerfile esteja em um diretório chamado "meu_projeto", o comando seria algo assim:

```bash
docker build -t meu_projeto:1.0 .
```

Isso construirá uma imagem com a tag `meu_projeto:1.0` usando o Dockerfile no diretório atual (`.`).

### CLI

```powershell
# criar imagem baseada no script do Dockerfile (-t aloca um terminal para o container e o ponto (.) referencia o Dockerfile)
$ docker build -t <name-image> .

# criar imagem com controle de versões
$ docker build -t <name-image:v> .

# mostrar detalhes da imagem criada
$ docker image ls <name-image>
ou
$ docker image ls <CONTAINER_ID>

# mostrar log de criação e uso da imagem
$ docker image history <name-image>
ou
$ docker image history <CONTAINER_ID>

# subir container (--rm: deleta após uso, -p: port)
$ docker run --rm -p 3000:3000 <name-image>

# subir container (-p: port, -d: <detach> execução em background)
$ docker run -p 3000:3000 -d <name-image>

# listar containers em execução
$ docker ps

# parar container
$ docker stop <CONTAINER_ID>

# iniciar container
$ docker start <CONTAINER_ID>

# listar log de atividades do container
$ docker logs <CONTAINER_ID>

# remover uma imagem ou um container
$ docker rm <IMAGE_ID>
$ docker rm <CONTAINER_ID>

# baixar uma imagem do Docker Hub ou de um registro de contêiner.
$ docker pull <IMAGE_NAME:TAG>
# exemplo: docker pull ubuntu:latest
```

## Aulas

### Estrutura de um Dockerfile

Commit: [Estrutura de um Dockerfile](https://github.com/rocketseat-education/devops-docker-containers/commit/0f8c46d5dcadcc8088a2f6a5262be3bc5a7d2557)

Nesta aula, discutimos a continuação da construção do `Dockerfile` para executar nossa aplicação. Abordamos instruções como workdir para definir o diretório de trabalho, copy para copiar arquivos, `run` para executar comandos e `cmd` para iniciar a aplicação. Exploramos a importância de expor portas e a criação de imagens Docker. Também destacamos a necessidade de otimizar o tamanho das imagens geradas. Ao final, preparamos a imagem para rodar o container.

Devido as dependências do projeto `npx @nestjs/cli@latest new api` rodado em 31/03/2025, foi necessário utilizar o `node:20-slim` como *tag* para garantir compatibilidade dos pacotes iniciais do **nestjs**.

### Rodando Nosso Container

Nesta aula, abordei a criação e execução de um container Docker a partir de uma imagem. Expliquei sobre a importância de tags, Image ID, tamanho da imagem e utilização do comando `docker run`. Destaquei a instrução `-rm` para deletar o container ao final do ciclo de vida, mapeamento de portas com `-p`, e a visualização de containers em execução com `docker ps`. Também mencionei a execução em background com `-d` e a visualização de logs com `docker logs`. Finalizei ressaltando a importância das boas práticas na criação de containers.

### Melhorias e Otimizações na Nossa Imagem

Commit: [Melhorias e Otimizações na Nossa Imagem](https://github.com/rocketseat-education/devops-docker-containers/commit/7e635ed090972147fc5f0fa6c8663dbf052e89c7)

Nesta aula, vamos abordar boas práticas para melhorar a performance e economizar espaço em uma build Docker. Explico a importância de copiar o `Yarn.loc`, adicionar o `yarnrc.yml` e ignorar pastas como `node_modules` e `dist`. Demonstro como utilizar o docker ignore e a tag correta ao construir imagens Docker. Ao final, destaco a necessidade de versionamento adequado. Essas práticas contribuem para otimizar builds e manter um histórico de versões eficiente.

Estudante: Foi necessário a exe.cução do comando `yarn set version stable` seguido de `yarn install` para a criação do arquivo `yarnrc.yml`.
