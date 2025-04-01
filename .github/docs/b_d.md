# Bloco D - Melhorando a Performance Alpine e Stretch

## Sumário

- [Bloco D - Melhorando a Performance Alpine e Stretch](#bloco-d---melhorando-a-performance-alpine-e-stretch)
  - [Sumário](#sumário)
  - [Links Importantes](#links-importantes)
  - [Conceitos e Explicações](#conceitos-e-explicações)
    - [O que é Alpine?](#o-que-é-alpine)
    - [O que é Stretch?](#o-que-é-stretch)
  - [Aulas](#aulas)
    - [Alpine e Stretch](#alpine-e-stretch)
    - [Adicionando o Alpine na nossa imagem](#adicionando-o-alpine-na-nossa-imagem)
    - [Criando múltiplos estágios](#criando-múltiplos-estágios)

## Links Importantes

- [Docker Hub Node](https://hub.docker.com/_/node/tags?name=20-alpine)

## Conceitos e Explicações

### O que é Alpine?

Alpine Linux é uma distribuição de Linux leve, simples e segura, conhecida por seu tamanho pequeno e eficiência. Ela é projetada especialmente para ambientes onde recursos de hardware são limitados, como em servidores, contêineres Docker e sistemas embarcados.

Algumas características distintivas do Alpine Linux incluem:

1. **Tamanho pequeno**: O Alpine é notável por seu tamanho compacto. A imagem mínima do sistema é geralmente menor que 10 MB, tornando-o uma escolha popular para ambientes onde o espaço em disco é limitado.

2. **Eficiência**: Por causa de seu tamanho pequeno, o Alpine consome menos recursos de hardware em comparação com outras distribuições Linux. Isso o torna ideal para implantações em servidores e contêineres, onde a eficiência é essencial.

3. **Segurança**: Alpine Linux segue práticas de segurança rigorosas. Utiliza o projeto de segurança de encaminhamento (grsecurity) e a biblioteca musl libc, conhecida por sua abordagem focada na segurança.

4. **Simplicidade**: O Alpine Linux adota uma abordagem minimalista e simplificada. Isso significa que tende a ter menos componentes e configurações pré-instalados, permitindo aos usuários adicionar apenas o que precisam, o que também contribui para sua segurança e eficiência.

Devido a essas características, o Alpine Linux é frequentemente usado em cenários onde a segurança, o tamanho e a eficiência são prioridades, como em servidores web, servidores de contêineres e dispositivos de rede.

### O que é Stretch?

No contexto de contêineres e Docker, "Stretch" refere-se à versão específica de uma imagem do Docker baseada no sistema operacional Debian. Essa imagem é derivada da distribuição Debian e inclui o sistema operacional Debian Stretch (versão 9.x) como sua base.

Assim, quando alguém menciona uma imagem Docker com "Stretch", estão se referindo a uma imagem que utiliza o Debian Stretch como sistema operacional base. Isso significa que qualquer contêiner criado a partir dessa imagem herdará as características e configurações do Debian Stretch.

Essas imagens são úteis para desenvolvedores e operadores que desejam executar aplicativos ou serviços em um ambiente baseado em Debian Stretch dentro de contêineres Docker. O uso de imagens baseadas no Debian Stretch pode fornecer uma plataforma estável e confiável para a execução de aplicativos, além de oferecer acesso a um vasto ecossistema de pacotes e ferramentas disponíveis no Debian.

## Aulas

### Alpine e Stretch

Nesta aula, abordamos a otimização de containers, destacando a importância de reduzir o tamanho das imagens para melhorar a performance. Introduzimos o Alpine, uma distribuição Linux enxuta e otimizada para containers. Comparamos diferentes versões do Node, mostrando a redução significativa de tamanho e vulnerabilidades ao utilizar o Alpine em vez do Debian. Exploramos também outras versões do Debian, como Stretch, Buster e Jessie. Na próxima aula, faremos a transição para o Alpine para otimizar ainda mais nossos containers.

- tamanho imagem `node:20` antes do Alpine e do `-slim`: `api-rocket:v0` = 1.39GB
- tamanho imagem `node:20-slim` antes do Alpine: `api-rocket:v1` = 655.19MB

### Adicionando o Alpine na nossa imagem

Commit: [Adicionando o Alpine na nossa imagem](https://github.com/rocketseat-education/devops-docker-containers/commit/f54fb9b11c870f8120dd70c29e420c727ed08201)

Nesta aula, foi abordado o processo de configuração de uma aplicação com Alpine, uma imagem leve do Docker. Foi destacada a importância de seguir a lógica de nomenclatura ao trabalhar com diferentes tecnologias. Foi demonstrado como realizar o build da imagem Docker, aproveitando o mecanismo de cache para economizar tempo. Ao trocar a base image para Alpine, houve uma redução significativa no tamanho da imagem, mostrando a eficiência dessa prática. O próximo passo será abordar estágios múltiplos para otimização.

- tamanho imagem `node:20-alpine3.21`: `api-rocket:v2` = 613.17MB

### Criando múltiplos estágios

Commit: [Criando múltiplos estágios](https://github.com/rocketseat-education/devops-docker-containers/commit/2e1bf92194fe5e19c10fd7b979303d52b91f2091)

Nesta aula, abordo o conceito de multi-stage building para otimização de containers. Explico como dividir o processo de build em diferentes estágios, evitando incluir itens desnecessários na imagem final. Demonstro na prática como utilizar aliases e copiar arquivos entre estágios, resultando em uma imagem mais leve e otimizada. Ao final, realizo um docker build para mostrar a redução do tamanho da imagem com o multi-stage build.

- tamanho imagem `node:20-alpine3.21` com multiplios estágios de `build`: `api-rocket:v3` = 335.45MB
