# Bloco C - Redes e Volumes

## Sumário

- [Bloco C - Redes e Volumes](#bloco-c---redes-e-volumes)
  - [Sumário](#sumário)
  - [Links Importantes](#links-importantes)
  - [Conceitos e Explicações](#conceitos-e-explicações)
    - [CLI](#cli)
    - [importância da comunicação e redes (network) em containers Docker](#importância-da-comunicação-e-redes-network-em-containers-docker)
      - [Tipos de Redes no Docker](#tipos-de-redes-no-docker)
      - [Comunicação Entre Containers](#comunicação-entre-containers)
      - [Exposição de Portas e Comunicação Externa](#exposição-de-portas-e-comunicação-externa)
      - [Segurança e Isolamento](#segurança-e-isolamento)
      - [Conclusão](#conclusão)
    - [Como trabalhar com arquivos dentro de um Container?](#como-trabalhar-com-arquivos-dentro-de-um-container)
    - [O que são Volumes?](#o-que-são-volumes)
      - [Lidando com Volumes em Docker](#lidando-com-volumes-em-docker)
  - [Aulas](#aulas)
    - [Camada de abstração](#camada-de-abstração)
    - [Gerenciando redes](#gerenciando-redes)
    - [Arquivos e Containers](#arquivos-e-containers)
    - [Entendendo sobre volumes](#entendendo-sobre-volumes)
    - [Persistindo informações nos volumes](#persistindo-informações-nos-volumes)

## Links Importantes

## Conceitos e Explicações

### CLI

```powershell

# exibir lista de conexões com o Docker
$ docker network ls

# criar conexão com o Docker
$ docker network create <nome-conexao>

# remover uma conexão
$ docker network rm <nome-conexao>

# associar uma rede a um container
$ docker network connect <ID_REDE> <ID_CONTAINER>

# inspecionar rede conectada
$ docker network inspect <ID_REDE>

# inspecionar container
$ docker container inspect <ID_CONTAINER>

# acessar arquivos do container (-it: interatividade)
$ docker exec -it <ID_CONTAINER> bash

# criar volume 
$ docker volume create <nome-volume>

# remover volume 
$ docker volume create <nome-volume>

# inspecionar volume
$ docker volume inspect <nome-volume>

# Exemplo de associação de network e volume a um container com definição de nome
$ docker run --volume primeiro-volume:/usr/src/app --network primeira-network --name nice-container -p 3001:3000 -d api-rocket:v1 
```

### importância da comunicação e redes (network) em containers Docker

A comunicação e redes no Docker são essenciais para garantir que os containers possam interagir entre si, com serviços externos e com o host. O Docker fornece um sistema de redes flexível que permite configurar diferentes tipos de conectividade conforme a necessidade da aplicação.  

#### Tipos de Redes no Docker

O Docker possui vários drivers de rede que controlam como os containers se comunicam:  

- **Bridge (Padrão)**  
  - Usado quando um container é iniciado sem especificar uma rede.  
  - Containers na mesma rede bridge podem se comunicar entre si usando nomes de serviço (DNS interno do Docker).  
  - Exemplo:  

    ```powershell
    docker network create my_bridge
    docker run -d --name app --network my_bridge my_image
    docker run -d --name db --network my_bridge mysql
    ```
  
- **Host**  
  - O container compartilha a pilha de rede do host, eliminando a necessidade de mapeamento de portas.  
  - Útil para reduzir latência e quando o container precisa acessar diretamente as interfaces do host.  
  - Exemplo:  
  
    ```powershell
    docker run --network host nginx
    ```

- **None**  
  - O container é isolado da rede, sem acesso externo.  
  - Pode ser usado para segurança em processos que não precisam de comunicação.  
  - Exemplo:  
  
    ```powershell
    docker run --network none busybox
    ```

- **Overlay** (usado em Swarm)  
  - Conecta containers em diferentes hosts do Docker.  
  - Necessário para aplicações distribuídas.  

- **Macvlan**  
  - Permite que containers tenham um endereço MAC próprio e sejam tratados como dispositivos de rede pelo host.  

#### Comunicação Entre Containers

- Containers na **mesma rede bridge** podem se comunicar usando seus nomes como hostname.  
- Se estiverem em redes diferentes, é necessário configurar **port forwarding** ou utilizar **Docker Compose** para criar uma rede compartilhada.  

#### Exposição de Portas e Comunicação Externa

- Containers podem expor portas para o host usando `-p`.  
- Exemplo:  
  
  ```powershell
  docker run -d -p 8080:80 nginx
  ```

  Aqui, o Nginx dentro do container responde na porta `8080` do host.  

- O Docker também permite publicar portas automaticamente com `-P`, mapeando portas aleatórias.  

#### Segurança e Isolamento

- **Firewalls e regras de iptables** controlam o tráfego entre containers e o host.  
- **Network Policies** em Kubernetes podem definir restrições de comunicação.  

#### Conclusão

A comunicação em containers Docker é fundamental para arquiteturas distribuídas, permitindo que serviços independentes se comuniquem de forma eficiente e segura. O uso correto dos drivers de rede garante desempenho, escalabilidade e segurança.

### Como trabalhar com arquivos dentro de um Container?

Para trabalhar com arquivos dentro de um contêiner Docker, você tem algumas opções:

1. **Copiar arquivos para dentro ou fora do contêiner**: Você pode usar os comandos `docker cp` para copiar arquivos entre o host e o contêiner.

   Exemplo:

   ```powershell
   # Copiando um arquivo do host para o contêiner
   docker cp arquivo.txt meu-container:/caminho/destino/arquivo.txt

   # Copiando um arquivo do contêiner para o host
   docker cp meu-container:/caminho/arquivo.txt arquivo.txt
   ```

2. **Montar volumes**: Esta é uma maneira mais flexível de trabalhar com arquivos, onde você monta um diretório do host dentro do contêiner. Qualquer alteração feita no diretório dentro do contêiner será refletida no diretório do host e vice-versa.

   Exemplo:

   ```powershell
   docker run -d --name meu-container -v /caminho/no/host:/caminho/no/contêiner imagem
   ```

3. **Usar comandos dentro do contêiner**: Você também pode acessar um shell dentro do contêiner usando `docker exec` e, em seguida, executar comandos de manipulação de arquivo dentro do ambiente do contêiner.

   Exemplo:

   ```powershell
   docker exec -it meu-container bash
   # Dentro do contêiner, você pode usar comandos como cp, mv, rm, mkdir, etc.
   cp /caminho/arquivo.txt /caminho/destino/arquivo.txt
   ```

4. **Construir uma imagem com os arquivos incorporados**: Se você tem arquivos que deseja que estejam disponíveis em um contêiner, pode incluí-los em uma imagem Docker usando um Dockerfile.

   Exemplo de Dockerfile:

   ```Dockerfile
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

   ```powershell
   docker volume create meu-volume
   ```

2. **Montando um volume em um contêiner**:

   Você pode montar um volume em um contêiner usando a opção `-v` ou `--mount` ao iniciar o contêiner.

   ```powershell
   docker run -d --name meu-container -v meu-volume:/caminho/no/contêiner imagem
   ```

   ou

   ```powershell
   docker run -d --name meu-container --mount source=meu-volume,target=/caminho/no/contêiner imagem
   ```

3. **Montando um diretório do host como volume**:

   Além de criar volumes dedicados, você também pode montar diretórios do host como volumes.

   ```powershell
   docker run -d --name meu-container -v /caminho/no/host:/caminho/no/contêiner imagem
   ```

4. **Listando volumes**:

   Você pode listar todos os volumes disponíveis no sistema usando o comando `docker volume ls`.

   ```powershell
   docker volume ls
   ```

5. **Removendo volumes**:

   Você pode remover volumes não utilizados com o comando `docker volume rm`.

   ```powershell
   docker volume rm meu-volume
   ```

6. **Usando volumes em Dockerfile**:

   Você também pode definir volumes em um Dockerfile, indicando quais diretórios dentro do contêiner devem ser tratados como volumes.

   ```powershell
   VOLUME /caminho/no/contêiner
   ```

Volumes são essenciais para muitos casos de uso do Docker, como persistência de dados, compartilhamento de arquivos entre contêineres e integração com sistemas de armazenamento externos. Eles oferecem uma maneira flexível e poderosa de lidar com o armazenamento de dados em contêineres Docker.

## Aulas

### Camada de abstração

Nesta aula, abordamos a importância da comunicação e redes em containers Docker. Exploramos os conceitos de redes, como o driver bridge, null e roast, e a criação de redes personalizadas. Destacamos a organização de redes por projetos e a utilização de redes específicas para diferentes aplicações. Além disso, discutimos a criação de redes com o comando `docker network create` e a importância das boas práticas, como a utilização de tags para otimização. Na próxima aula, vamos aprofundar o conhecimento em redes e realizar algumas práticas.

### Gerenciando redes

Nesta aula, foi abordado como associar uma rede a um container Docker. Foram apresentadas duas formas de fazer essa associação: utilizando o comando `docker network connect` para containers já em execução e definindo a rede no momento da criação do container com o parâmetro `--network`. Foi explicado como verificar a associação da rede ao container utilizando os comandos `docker network inspect` e `docker container inspect`. Também foi mencionado que um container pode estar associado a várias redes.

### Arquivos e Containers

Esta aula, aborda a importância dos volumes em containers Docker para manter dados persistentes. Mostra como os arquivos são armazenados no container e como são perdidos ao reconstruir o container. Destaca a necessidade de separar responsabilidades e exemplifica a criação de arquivos dentro do container. Demonstra como os arquivos são perdidos sem volumes persistentes. O instrutor encerra indicando que o próximo vídeo abordará como manter arquivos persistentes em volumes específicos.

### Entendendo sobre volumes

Nesta aula, abordamos o conceito de volumes no Docker. Volumes são diretórios externos que permitem persistência de dados, essenciais para salvar arquivos e manter dados em containers. A criação e associação de volumes são fundamentais para garantir a persistência de dados entre reinicializações de containers. O comando `docker volume` é utilizado para gerenciar volumes, permitindo a criação, inspeção e remoção de volumes. A associação de volumes com containers é feita através do comando `docker run -v`, garantindo a persistência dos dados.

### Persistindo informações nos volumes

Nesta aula, abordo a criação de arquivos em containers Docker e a persistência desses arquivos em volumes. Demonstrando como criar, verificar e manter arquivos em containers com volumes associados. Destaco a importância de apontar para o volume ao executar um container para evitar a perda de arquivos. Exploro a continuidade da existência dos volumes mesmo após a exclusão dos arquivos e a possibilidade de restaurar arquivos ao associar um volume novamente. Esses conceitos serão aprofundados nos módulos futuros.
