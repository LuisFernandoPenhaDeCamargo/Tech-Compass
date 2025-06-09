# Introdução ao Docker

<!-- TODO: linkar este ponto com "Python". -->

## Sumário

1. [O que é Containerização?](#containerizacao)
2. [O que é Docker?](#docker)
3. [Principais Conceitos de Docker](#principais-conceitos-docker)
4. <a id="conteineres-vs-maquinas-virtuais">[Contêineres vs. Máquinas Virtuais](./1-conteineres-vs-maquinas-virtuais.md)</a> *(redireciona para outro documento)*
5. <a id="casos-uso-docker">[Casos de Uso do Docker](./2-casos-uso-docker.md)</a>  *(redireciona para outro documento)*
6. <a id="">[Por que Usar Docker?]()</a>
7. <a id="">[Primeiro Exemplo "Hello World"]()</a>

## <a id="containerizacao">1. O que é Containerização?</a>

**Containerização** é a técnica de empacotar aplicações junto com as suas dependências — como bibliotecas, configurações e runtimes — em unidades isoladas chamadas **contêineres**. Isso garante que a aplicação seja executada de forma consistente em qualquer ambiente.

### Exemplo

Imagine que você criou uma aplicação web que depende do **Python 3.11**, da biblioteca **Flask**, e de um arquivo de configuração específico. Se você compartilhar apenas o código com outra pessoa, ela terá que:

- Instalar a versão correta do Python
- Instalar as mesmas dependências
- Garantir que o ambiente esteja configurado da mesma forma que o seu

Esse processo pode facilmente causar erros — o famoso "funciona na minha máquina, mas não na sua".

Com containerização você empacota tudo isso num contêiner:

- Base com Python 3.11
- Bibliotecas já instaladas (como Flask)
- Código da aplicação
- Arquivos de configuração prontos

Esse contêiner pode ser executado **em qualquer lugar** que tenha uma plataforma de containerização instalada — sem a necessidade de configuração adicional. Ele funcionará exatamente da mesma forma na sua máquina, em um servidor de produção ou no notebook de outra pessoa.

## <a id="docker">2. O que é Docker?</a>

**Docker** é uma plataforma de **containerização** de código aberto que automatiza a criação, distribuição e execução de aplicações em contêineres. Ele simplifica o processo de empacotar o ambiente da aplicação, garantindo portabilidade, consistência e agilidade no desenvolvimento e na implantação.

## <a id="principais-conceitos-docker">3. Principais Conceitos de Docker</a>

1. **Dockerfile:** arquivo de texto que define as instruções necessárias para construir uma imagem Docker
2. **Imagem:** artefato imutável que contém o sistema de arquivos e as dependências da aplicação; serve como base para a criação de contêineres
3. **Contêiner:** instância em execução de uma imagem, que agrupa a aplicação e todas as suas dependências em um ambiente isolado
4. **Registro:** repositório de imagens — como o Docker Hub (público) ou soluções privadas — onde as imagens são armazenadas, versionadas e compartilhadas
5. **Volume:** mecanismo de armazenamento persistente utilizado para manter dados fora do ciclo de vida do contêiner
6. **Rede:** subsistema que permite a comunicação entre contêineres e entre contêineres e o host
7. **Tag:** identificador utilizado para versionar e distinguir diferentes versões de uma mesma imagem
8. **Orquestração:** processo de coordenar a execução de múltiplos contêineres, incluindo criação, inicialização, comunicação entre eles, gerenciamento de volumes, redes e escalabilidade

## [[ Voltar para: Docker ]](../docker.md#introducao-docker)