# 4. `ENTRYPOINT` – Comando de Entrada

## O que é?

`ENTRYPOINT` define um comando **fixo** que sempre será executado quando o contêiner iniciar. Os argumentos adicionais podem ser passados via `CMD` ou linha de comando.

## Para que Serve?

Tornar o contêiner num "wrapper" de execução, onde você garante que o binário ou script principal nunca seja alterado inadvertidamente.

## Exemplos

### 1. Exemplo Didático

- **Máquina de café programável:** imagine uma máquina em que o botão "Iniciar" sempre aciona o processo de preparar café. Você pode ajustar a quantidade de água ou intensidade (argumentos), mas o comando de preparo — a lógica da máquina — permanece sempre o mesmo
- **Cliente Git:** ao usar `git` no terminal, você sempre invoca o mesmo binário `git` (o entrypoint). Os comandos específicos (`clone`, `commit`, `push`) são passados como argumentos (via `CMD` ou linha de comando)

### 2. Exemplo em Dockerfile

```dockerfile
FROM alpine:3.18

# Copia nosso script para dentro do contêiner
COPY backup.sh /usr/local/bin/backup.sh
RUN chmod +x /usr/local/bin/backup.sh

# ENTRYPOINT fixa o binário/script que será executado
ENTRYPOINT ["/usr/local/bin/backup.sh"]

# CMD define argumentos padrão que podem ser substituídos
CMD ["--daily"]
```

- Aqui, o `ENTRYPOINT` faz com que **sempre** seja executado o script `backup.sh`
- O `CMD` fornece `--daily` como argumento padrão, mas você pode rodar `docker run mybackup --weekly` — onde `mybackup` é o **nome da imagem** — para modificar esse parâmetro sem alterar o entrypoint

## [[ Voltar para: Instruções Básicas do Dockerfile ]](./instrucoes-basicas-dockerfile.md#entrypoint)