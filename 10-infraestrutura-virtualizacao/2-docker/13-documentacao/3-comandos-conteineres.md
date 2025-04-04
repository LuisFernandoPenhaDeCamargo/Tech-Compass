# Comandos de Contêineres

## Sumário

- `docker run <imagem>` – cria e executa um contêiner a partir de uma imagem
- `docker run -it <imagem> /bin/bash` – inicia um contêiner interativo com acesso ao shell Bash
- `docker ps` – lista os contêineres em execução
- `docker ps -a` – lista todos os contêineres (parados e ativos)
- `docker start <ID/nome>` – inicia um contêiner parado
- `docker stop <ID/nome>` – para um contêiner em execução
- `docker kill <ID/nome>` – finaliza um contêiner forçadamente
- `docker restart <ID/nome>` – reinicia um contêiner
- `docker rm <ID/nome>` – remove um contêiner
- `docker logs <ID/nome>` – visualiza logs do contêiner
- `docker exec -it <ID/nome> /bin/bash` – acessa o terminal de um contêiner em execução
- `docker cp <caminho de origem> <caminho de destino>` – copia arquivos entre contêiner e host
- `docker attach <ID/nome>` – conecta-se ao terminal de um contêiner em execução
- `docker commit <ID/nome> <nome da imagem>` – cria uma imagem a partir de um contêiner existente

## [[ Voltar para: Documentação ]](./documentacao.md#comandos-conteineres)