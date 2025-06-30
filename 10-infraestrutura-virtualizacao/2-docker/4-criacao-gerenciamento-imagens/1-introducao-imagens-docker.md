# 1. Introdução às Imagens Docker

As **imagens Docker** são o ponto de partida para criar contêineres. Elas consistem em um conjunto de camadas empilhadas (layers), cada uma representando uma instrução do Dockerfile, e formam um artefato **imutável** que pode ser compartilhado e executado em qualquer host com Docker.

## Por que Usar Imagens?

- **Reprodutibilidade:** a mesma imagem gera contêineres idênticos, eliminando variações entre ambientes
- **Portabilidade:** uma imagem pode ser transferida via registries (Docker Hub, AWS ECR, GitHub Packages etc.) e executada em qualquer máquina
- **Eficiência de armazenamento:** camadas são reutilizadas; se duas imagens tiverem mesmas instruções iniciais, o Docker compartilhará essas camadas em cache

## Componentes de uma Imagem

1. **Camadas (Layers):** cada comando do Dockerfile (`RUN`, `COPY`, `ADD` etc.) cria uma nova camada sobre a anterior
2. **Manifesto:** arquivo JSON que lista as camadas e metadados (autor, comandos padrão, variáveis de ambiente)
3. **Sistema de arquivos UnionFS:** mecanismo que "cola" as camadas em um único sistema de arquivos, permitindo acesso transparente

## Ciclo Básico de Trabalho

1. **Construir:** executar `docker build -t name-image:tag .` a partir de um Dockerfile
2. **Listar:** verificar as imagens locais com `docker images` ou `docker image ls`
3. **Excluir:** remover imagens obsoletas com `docker rmi name-image:tag` ou `docker image prune`

## Exemplos

### 1. Exemplo Rápido

Constrói uma imagem chamada myapp:latest

```bash
docker build -t myapp:latest .
```

Lista todas as imagens presentes

```bash
docker images
```

Remove imagens não utilizadas

```bash
docker image prune -f
```

## [[ Voltar para: Criação e Gerenciamento de Imagens ]](./criacao-gerenciamento-imagens.md#introducao-imagens-docker)