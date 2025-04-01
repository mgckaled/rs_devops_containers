# Quizzes

## Sumário

- [Quizzes](#quizzes)
  - [Sumário](#sumário)
  - [Questionário Avaliativo](#questionário-avaliativo)
  - [Quiz - Iniciando com containers](#quiz---iniciando-com-containers)
  - [Quiz - Criando nossa primeira Imagem](#quiz---criando-nossa-primeira-imagem)
  - [Quiz - Redes e Volumes](#quiz---redes-e-volumes)
  - [Quiz - Melhorando a Performance Alpine e Stretch](#quiz---melhorando-a-performance-alpine-e-stretch)
  - [Quiz - Trabalhando com múltiplos containers](#quiz---trabalhando-com-múltiplos-containers)

## Questionário Avaliativo

## Quiz - Iniciando com containers

1 - *Qual é a principal diferença entre uma imagem e um contêiner no Docker?* **Resposta:** As imagens são modelos para aplicações, enquanto os contêineres são instâncias em tempo de execução das imagens.

2 - *O que é o CGroup (Control Group) no contexto de containers?* **Resposta:** Uma funcionalidade do kernel do Linux que permite o controle e a limitação de recursos de um processo.

3 - *Qual é o principal objetivo da Open Container Initiative (OCI)?* **Resposta:**

4 - *Por que é importante que os contêineres sejam agnósticos em relação aos clientes e às pilhas de orquestração?* **Resposta:** Para facilitar a interoperabilidade e a portabilidade dos contêineres

5 - *Qual é o principal objetivo da Docker CLI (Command Line Interface)?* **Resposta:** Permitir que os usuários executem comandos para criar, gerenciar e excluir contêineres

6 - *Qual é o significado de um contêiner ser efêmero no contexto do Docker?* **Resposta:**

7 - *O que é o Docker Hub?* **Resposta:** Uma plataforma para compartilhar imagens de contêineres com a comunidade

8 - *Qual é a finalidade do comando "docker run" na Docker CLI?* **Resposta:** Iniciar a execução de um novo contêiner com base em uma imagem existente

## Quiz - Criando nossa primeira Imagem

1 - *O que é um Dockerfile e qual é a sua função principal na criação de imagens Docker?* **Resposta:** Um Dockerfile é um manifesto declarativo que define como um contêiner será executado

2 - *Qual é a função da instrução `FROM` em um Dockerfile?* **Resposta:** Especifica a imagem base que será usada como ponto de partida

3 - *Por que é importante escolher a imagem base correta ao criar um Dockerfile?* **Resposta:** Para garantir a consistência das dependências

4 - *Como podemos verificar o tamanho da imagem Docker construída a partir de um Dockerfile?* **Resposta:** Usando o comando `docker image ls`

5 - *Qual é a finalidade da opção `rm` no comando docker `run`?* **Resposta:** Excluir o contêiner após a finalização de sua execução

6 - *O que faz a instrução `EXPOSE` em um Dockerfile?* **Resposta:** Expõe portas do contêiner para o host

7 - *Qual é o significado da tag de imagem latest ?* **Resposta:** Indica que a imagem é a versão mais recente disponível

8 - *Qual é a importância de implementar um arquivo `.dockerignore` em um projeto Docker?* **Resposta:** Para não incluir arquivos e diretórios desnecessários no contêiner

## Quiz - Redes e Volumes

1 - *Qual é o comando usado para listar as redes disponíveis no Docker?* **Resposta:** `docker network ls`

2 - *Qual é o driver padrão de rede no Docker?* **Resposta:** `bridge`

3 - *Como podemos associar uma rede a um contêiner já em execução?* **Resposta:** `docker network connect`

4 - *Qual opção podemos usar no comando docker run para criar um contêiner já associado a uma rede específica?* **Resposta:** $ `-network`

5 - *Qual comando é utilizado para criar um volume no Docker?* **Resposta:** `docker volume create`

6 - *O que são volumes no Docker?* **Resposta:** Diretórios externos associados diretamente a contêineres

7 - *Como podemos acessar o shell de um contêiner em execução?* **Resposta:** $ `docker exec -it [ID_CONTAINER] bash`

8 - *Por que é essencial associar um volume a um contêiner no Docker?* **Resposta:** Para persistir dados mesmo quando o contêiner é destruído e recriado

## Quiz - Melhorando a Performance Alpine e Stretch

1 - ** **Resposta:**

2 - ** **Resposta:**

3 - ** **Resposta:**

4 - ** **Resposta:**

5 - ** **Resposta:**

6 - ** **Resposta:**

7 - ** **Resposta:**

8 - ** **Resposta:**

## Quiz - Trabalhando com múltiplos containers

1 - ** **Resposta:**

2 - ** **Resposta:**

3 - ** **Resposta:**

4 - ** **Resposta:**

5 - ** **Resposta:**

6 - ** **Resposta:**

7 - ** **Resposta:**

8 - ** **Resposta:**
