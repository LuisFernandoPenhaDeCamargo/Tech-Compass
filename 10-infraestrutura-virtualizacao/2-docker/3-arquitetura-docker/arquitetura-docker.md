# Arquitetura do Docker

O Docker segue um modelo **cliente-servidor** onde componentes distintos interagem para construir, distribuir e executar contêineres. A seguir, os principais elementos dessa arquitetura:

## Docker Engine

Plataforma que reúne o **daemon**, a **API** e a **CLI**, servindo como base para todas as operações com contêineres.

## Docker Daemon (`dockerd`)

- **Serviço em background** que gerencia imagens, contêineres, redes e volumes
- **Escuta** requisições via socket UNIX ou TCP (Docker API)
- **Responsabilidades:**
    + Armazenar e limpar imagens locais
    + Construir imagens a partir de Dockerfiles
    + Criar, iniciar, parar e remover contêineres
    + Provisionar redes (bridge, overlay, host)
    + Gerenciar volumes persistentes

## Docker API

- **Interface HTTP/REST** pela qual o daemon se comunica com clientes e ferramentas de terceiros
- **Endpoints principais:**
    + `/images` (build, list, remove)
    + `/containers` (create, start, stop, list)
    + `/networks` (create, inspect, connect)
    + `/volumes` (create, inspect, remove)
- **Uso:** tanto a CLI oficial (`docker <...>`) quanto bibliotecas e GUIs externas consomem essa API

## Docker CLI (`docker`)

- **Ferramenta de linha de comando** que o usuário final utiliza para interagir com o Docker
- **Comunica-se** com o daemon via Docker API
- **Principais comandos:**
    + `docker build` → constrói imagens
    + `docker run` → cria e inicia contêineres
    + `docker ps` → lista contêineres em execução
    + `docker pull` / `docker push` → interage com registries

## Fluxo de Operação

1. **Iniciação:** o daemon é iniciado como serviço do sistema (`systemd`, `service` etc.)
2. **Requisição:** usuário executa um comando CLI, que traduz a ação em chamada HTTP à API
3. **Processamento:** o daemon recebe, valida e executa a solicitação, manipulando imagens, contêineres, redes ou volumes
4. **Resposta:** o daemon retorna o status e a saída da operação à CLI, que exibe o resultado no terminal

## [[ Voltar para: Docker ]](../docker.md#arquitetura-docker)