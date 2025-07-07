# Criação e Gerenciamento de Imagens

## Sumário

1. <a id="introducao-imagens-docker">[Introdução às Imagens Docker](./1-introducao-imagens-docker.md)</a> *(redireciona para outro documento)*
2. <a id="estrutura-interna-imagens">[Estrutura Interna das Imagens](./2-estrutura-interna-imagens/estrutura-interna-imagens.md)</a> *(redireciona para outro documento)*
3. [Armazenamento Local](#armazenamento-local)
4. <a id="uso-elaboracao-dockerfile">[Uso e Elaboração de Dockerfile](./4-uso-elaboracao-dockerfile/uso-elaboracao-dockerfile.md)</a> *(redireciona para outro documento)*
5. <a id="boas-praticas-criacao-imagens">[Boas Práticas na Criação de Imagens](./5-boas-praticas-criacao-imagens/boas-praticas-criacao-imagens.md)</a>

- <a id="publicacao-gerenciamento-imagens-registries">[Publicação e Gerenciamento de Imagens em Registries (Docker Hub, etc.)](./6-publicacao-gerenciamento-imagens-registries/publicacao-gerenciamento-imagens-registries.md)</a>

## <a id="armazenamento-local">3. Armazenamento Local</a>

O Docker armazena **imagens, camadas, metadados e volumes** no disco local da máquina onde está instalado. Compreender como esse armazenamento funciona ajuda a manter o ambiente limpo, economizar espaço e evitar problemas de desempenho.

### 1. Onde o Docker Armazena os Dados

O local padrão varia conforme o sistema operacional e o driver de armazenamento utilizado.

|  Sistema Operacional   |                              Caminho Padrão                               |
|------------------------|---------------------------------------------------------------------------|
|         Linux          |                             `/var/lib/docker`                             |
|    Windows (WSL 2)     |                     `\\wsl$\docker-desktop-data\...`                      |
| macOS (Docker Desktop) |Armazenado internamente via VM (HyperKit ou Apple Virtualization Framework)|

> No Linux, esse diretório contém subpastas que armazenam as camadas das imagens, os sistemas de arquivos dos contêineres, volumes, metadados e logs de execução.

### 2. Como as Camadas São Armazenadas

Cada camada da imagem é armazenada como um conjunto de arquivos sob um hash único. Camadas idênticas entre diferentes imagens são **reutilizadas**, reduzindo o uso de espaço em disco.

O Docker utiliza **drivers de armazenamento** para gerenciar essas camadas, como:

- `overlay2` (o mais comum e recomendado)
- `aufs` (mais antigo, obsoleto em algumas distros)
- `btrfs`, `zfs`, `devicemapper` (usos mais específicos)

Você pode verificar qual driver está em uso com:

```bash
docker info | grep Storage
```

### 3. Como Verificar o Uso de Espaço

O Docker fornece comandos úteis para acompanhar o que está armazenado localmente:

Lista as imagens locais.

```bash
docker images
```

Mostra uso de disco (imagens, volumes, etc.).

```bash
docker system df
```

Mostra detalhes da imagem, incluindo camadas.

```bash
docker image inspect <imagem>
```

### 4. Como Limpar e Gerenciar o Espaço

Ao longo do tempo, o armazenamento local pode crescer muito devido a imagens antigas, contêineres parados e volumes órfãos. Use os comandos abaixo para limpar:

- Remover imagens não utilizadas:

```bash
docker image prune
```

- Remover contêineres, redes e imagens não usados:

```bash
docker system prune
```

- Remover tudo, incluindo volumes (atenção!):

```bash
docker system prune --volumes
```

> Use com cautela.

## [[ Voltar para: Docker ]](../docker.md#criacao-gerenciamento-imagens)