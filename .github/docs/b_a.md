# Bloco A - Iniciando com containers

## Sumário

- [Bloco A - Iniciando com containers](#bloco-a---iniciando-com-containers)
  - [Sumário](#sumário)
  - [Links Importantes](#links-importantes)
  - [Conceitos e Explicações](#conceitos-e-explicações)
    - [O que é um container?](#o-que-é-um-container)
    - [E o que são "máquinas virtuais"?](#e-o-que-são-máquinas-virtuais)
    - [O que é Docker?](#o-que-é-docker)
    - [O que é LXC?](#o-que-é-lxc)
    - [O que é OCI?](#o-que-é-oci)
    - [Qual a diferença entre uma Imagem e um Container?](#qual-a-diferença-entre-uma-imagem-e-um-container)
    - [O que é o CGroup (Control Group) no contexto de containers?](#o-que-é-o-cgroup-control-group-no-contexto-de-containers)
  - [Principais instruções do Dockerfile](#principais-instruções-do-dockerfile)

## Links Importantes

- [Docker](https://www.docker.com/)
- [Docker Docs](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com)
- [Docker Hub Explore](https://hub.docker.com/explore)

## Conceitos e Explicações

### O que é um container?

Em DevOps, um "container" refere-se a uma unidade de software que empacota código e todas as suas dependências necessárias para que o aplicativo seja executado de maneira eficiente e consistente em diferentes ambientes de computação, como desenvolvimento, teste e produção.

Os containers encapsulam o software em um ambiente isolado, garantindo que ele funcione de maneira consistente, independentemente do ambiente em que seja executado. Eles incluem tudo o que é necessário para executar um aplicativo: o código, as bibliotecas, as dependências e as configurações do ambiente. Isso permite que os desenvolvedores criem aplicativos uma vez e os executem em qualquer lugar, eliminando problemas de compatibilidade entre ambientes de desenvolvimento e produção.

Um dos sistemas de container mais populares é o Docker, que facilita a criação, implantação e gerenciamento de containers. Os containers são amplamente usados em DevOps por sua capacidade de acelerar o desenvolvimento, simplificar a implantação e melhorar a portabilidade e a consistência dos aplicativos.

### E o que são "máquinas virtuais"?

Máquinas virtuais (VMs) são ambientes de computação virtualizados que operam como se fossem computadores físicos separados, mas são executados em um único hardware físico. Cada máquina virtual possui seu próprio sistema operacional, aplicativos e recursos de hardware simulados, como CPU, memória RAM, armazenamento e rede.

As VMs são criadas através de software de virtualização, que permite que um único servidor físico hospede várias VMs simultaneamente. Isso é útil para consolidar servidores físicos, maximizar a utilização de recursos e isolar aplicativos uns dos outros para melhorar a segurança e a confiabilidade.

Em resumo, máquinas virtuais fornecem uma maneira eficiente de executar múltiplos sistemas operacionais e aplicativos em um único hardware físico, oferecendo flexibilidade, escalabilidade e isolamento. Elas são comumente usadas em ambientes de data center, nuvem computacional e desenvolvimento de software.

### O que é Docker?

Docker é uma plataforma de código aberto projetada para simplificar a criação, implantação e execução de aplicativos em containers. Lançado em 2013, o Docker revolucionou a forma como os desenvolvedores criam, distribuem e executam software, oferecendo uma abordagem mais eficiente e consistente em comparação com as máquinas virtuais tradicionais.

Aqui estão os principais componentes e conceitos do Docker:

1. **Containers**: O Docker utiliza containers para empacotar e isolar aplicativos com suas dependências, como bibliotecas e configurações, em um ambiente leve e portátil. Os containers são executados em um sistema operacional host e compartilham o kernel do host, tornando-os mais eficientes do que as máquinas virtuais.

2. **Docker Engine**: É o componente central do Docker, responsável por criar e executar containers. O Docker Engine inclui o daemon do Docker, que gerencia os containers, e a interface de linha de comando (CLI) do Docker, que permite aos usuários interagir com o Docker.

3. **Imagens Docker**: As imagens Docker são modelos somente leitura usados para criar containers. Elas contêm o sistema de arquivos do aplicativo, bem como metadados sobre como executar o aplicativo. As imagens Docker são criadas usando um arquivo de configuração chamado Dockerfile e são armazenadas em registros Docker, como Docker Hub.

4. **Dockerfile**: É um arquivo de texto usado para definir a configuração de uma imagem Docker. Ele especifica os passos necessários para criar a imagem, como a instalação de dependências, a configuração do ambiente e a execução de comandos. O Dockerfile é usado junto com o comando `docker build` para criar uma imagem Docker.

5. **Docker Hub**: É um serviço de registro de imagens Docker hospedado pelo Docker, Inc. O Docker Hub permite que os usuários compartilhem, armazenem e gerenciem imagens Docker publicamente ou em repositórios privados. Ele contém milhares de imagens prontas para uso, incluindo sistemas operacionais, bancos de dados, servidores web e aplicativos populares.

6. **Docker Compose**: É uma ferramenta usada para definir e executar aplicativos Docker multi-container. Com o Docker Compose, os desenvolvedores podem definir a estrutura de um aplicativo em um arquivo YAML, especificando os serviços, redes e volumes necessários, e, em seguida, iniciar e parar o aplicativo com um único comando.

7. **Docker Swarm**: É uma ferramenta de orquestração de containers integrada ao Docker Engine. Com o Docker Swarm, os usuários podem criar e gerenciar clusters de hosts Docker para dimensionar e distribuir aplicativos em vários servidores. Ele fornece recursos de balanceamento de carga, escalabilidade automática e recuperação de falhas para aplicativos Docker em produção.

8. **Docker Desktop**: É uma aplicação para Windows e macOS que fornece uma experiência de desenvolvimento Docker completa em ambientes de desktop. O Docker Desktop inclui o Docker Engine, a CLI do Docker, o Docker Compose e outras ferramentas para facilitar o desenvolvimento de aplicativos Docker localmente.

Em resumo, o Docker é uma plataforma poderosa e flexível que simplifica o processo de desenvolvimento, implantação e execução de aplicativos em containers, oferecendo portabilidade, eficiência e consistência em diferentes ambientes de computação. Ele se tornou uma ferramenta essencial para DevOps, desenvolvedores e equipes de operações de TI que buscam modernizar e otimizar seus fluxos de trabalho de desenvolvimento e implantação de software.

### O que é LXC?

LXC (Linux Containers) é uma tecnologia de virtualização baseada no kernel do Linux que permite criar e gerenciar ambientes de computação isolados, conhecidos como containers. Desenvolvido inicialmente em 2008, o LXC fornece uma maneira leve e eficiente de virtualização que utiliza os recursos de isolamento do kernel do Linux, como namespaces e grupos de controle (cgroups), para criar e executar containers.

Aqui estão alguns pontos-chave sobre o LXC:

1. **Isolamento de Recursos**: O LXC usa namespaces do kernel do Linux para isolar processos, redes, sistemas de arquivos e outros recursos do sistema operacional dentro de cada container. Isso permite que múltiplos containers compartilhem o mesmo kernel do host, mas executem de forma isolada uns dos outros.

2. **Eficiência e Desempenho**: Como os containers do LXC compartilham o mesmo kernel do host, eles têm menos sobrecarga em comparação com as máquinas virtuais tradicionais. Isso resulta em uma maior eficiência de recursos e melhor desempenho, tornando o LXC uma escolha popular para ambientes onde a densidade e o desempenho são importantes.

3. **Ferramentas de Gerenciamento**: O LXC fornece ferramentas de linha de comando, bibliotecas e APIs para criar, iniciar, parar e gerenciar containers. Ele também oferece suporte a ferramentas de gerenciamento de containers de nível superior, como LXD (pronunciado "lex-dee"), que simplifica o uso do LXC e fornece recursos adicionais, como armazenamento em cluster e migração de containers.

4. **Flexibilidade**: O LXC é altamente flexível e pode ser usado para uma ampla variedade de casos de uso, desde a execução de aplicativos isolados até o fornecimento de ambientes de desenvolvimento e teste consistentes. Ele é amplamente utilizado em DevOps, computação em nuvem, hospedagem de serviços e virtualização de servidores.

Embora o Docker seja mais popular e amplamente adotado para a virtualização de containers, o LXC continua sendo uma opção sólida para usuários que preferem uma abordagem mais direta e integrada à virtualização de containers, especialmente em ambientes que exigem um alto desempenho e controle granular sobre os recursos do sistema.

### O que é OCI?

OCI (Open Container Initiative) é uma organização sem fins lucrativos criada em 2015 por líderes da indústria de tecnologia, incluindo empresas como Docker, Google, Red Hat e muitas outras. O objetivo da OCI é padronizar os formatos e as especificações técnicas para containers de software, promovendo a interoperabilidade entre diferentes implementações de tecnologia de containers e fornecendo uma base aberta e neutra para a inovação contínua no espaço de containers.

Os principais componentes e iniciativas da OCI incluem:

1. **Especificação de Formato de Imagem OCI**: Define um formato de arquivo padrão para imagens de containers, garantindo que as imagens sejam portáveis e interoperáveis entre diferentes runtimes de containers. O formato de imagem OCI é baseado em especificações anteriores, como Docker Image Format (DIF), e fornece uma especificação neutra para a indústria.

2. **Especificação de Runtime de Container OCI**: Define uma especificação para a execução de containers, incluindo como os containers são iniciados, gerenciados e interagem com o sistema operacional host. Esta especificação permite que diferentes runtimes de containers implementem o mesmo conjunto de APIs e comportamentos, garantindo a compatibilidade entre plataformas.

3. **Testes e Certificação OCI**: A OCI oferece um programa de testes e certificação para garantir que as implementações de tecnologia de containers estejam em conformidade com as especificações OCI. Isso ajuda a promover a interoperabilidade e a consistência entre diferentes soluções de containers.

Ao estabelecer padrões abertos e neutros, a OCI promove a inovação e a competição saudável no espaço de containers, permitindo que os usuários escolham entre várias implementações de tecnologia de containers sem ficarem presos a uma única plataforma ou fornecedor. Isso também facilita a integração e a interoperabilidade entre diferentes ferramentas e sistemas de software que utilizam containers, promovendo um ecossistema mais aberto e colaborativo.

### Qual a diferença entre uma Imagem e um Container?

A diferença fundamental entre uma imagem e um container está no seu estado e função:

1. **Imagem Docker**: Uma imagem Docker é um modelo somente leitura que contém um conjunto de instruções sobre como criar um container. Ela inclui o sistema de arquivos do aplicativo, suas dependências e metadados sobre como executar o aplicativo. As imagens Docker são criadas a partir de um arquivo de configuração chamado Dockerfile e podem ser armazenadas e compartilhadas em repositórios, como o Docker Hub. Em essência, uma imagem é como um molde que define o que será executado quando você iniciar um container.

2. **Container Docker**: Um container Docker é uma instância em execução de uma imagem Docker. Ele representa um ambiente isolado onde o aplicativo pode ser executado de forma consistente e independente de outros containers ou do sistema host. Um container Docker é criado a partir de uma imagem Docker usando o comando `docker run` e pode ser iniciado, parado, reiniciado e removido conforme necessário. Cada container possui seu próprio sistema de arquivos, processos, rede e ambiente de tempo de execução.

Em resumo, uma imagem Docker é um modelo somente leitura usado para criar containers, enquanto um container Docker é uma instância em execução de uma imagem Docker, que representa um ambiente isolado onde o aplicativo pode ser executado. As imagens são usadas para criar containers e podem ser compartilhadas e reutilizadas entre diferentes ambientes de desenvolvimento, teste e produção.

### O que é o CGroup (Control Group) no contexto de containers?

No contexto de containers, o CGroup (Control Group) é uma funcionalidade do kernel do Linux que é fundamental para a virtualização de recursos e o isolamento de containers. O CGroup permite que os sistemas operacionais Linux limitem, contabilizem e isolam os recursos de sistema, como CPU, memória, armazenamento e largura de banda de rede, entre diferentes processos ou grupos de processos.

Aqui estão alguns pontos-chave sobre o CGroup e seu papel no contexto de containers:

1. **Gerenciamento de Recursos**: O CGroup permite que os administradores de sistema e os mecanismos de gerenciamento de containers aloquem recursos de sistema de forma controlada e previsível para diferentes containers e processos. Isso é essencial para garantir que os containers não monopolizem os recursos do sistema, causando degradação de desempenho ou falhas de aplicativos.

2. **Isolamento de Recursos**: O CGroup oferece isolamento de recursos, permitindo que diferentes containers executem em um mesmo sistema, mas com recursos segregados. Por exemplo, é possível limitar a quantidade de CPU que um container pode usar ou a quantidade de memória que pode ser alocada para ele. Isso evita que um container afete negativamente o desempenho de outros containers ou do sistema host.

3. **Limitação de Uso de Recursos**: O CGroup permite definir limites rígidos ou suaves para o uso de recursos por containers ou grupos de processos. Isso pode incluir limites de CPU, limites de memória, limites de E/S de disco e limites de largura de banda de rede. Os limites rígidos garantem que um container não exceda um determinado limite de recursos, enquanto os limites suaves permitem que um container utilize recursos extras temporariamente, se disponíveis, mas com restrições quando os recursos estão escassos.

4. **Contabilidade de Recursos**: Além de limitar o uso de recursos, o CGroup também fornece recursos para contabilizar o consumo de recursos por containers e processos. Isso é útil para monitorar e analisar o uso de recursos ao longo do tempo e identificar possíveis gargalos de desempenho ou otimizações.

Em resumo, o CGroup é uma funcionalidade fundamental do kernel do Linux que permite o gerenciamento e o isolamento de recursos de sistema entre diferentes containers e processos. Ele desempenha um papel crucial na virtualização de recursos e no fornecimento de ambientes de computação isolados e previsíveis para aplicativos em containers.

## Principais instruções do Dockerfile

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
