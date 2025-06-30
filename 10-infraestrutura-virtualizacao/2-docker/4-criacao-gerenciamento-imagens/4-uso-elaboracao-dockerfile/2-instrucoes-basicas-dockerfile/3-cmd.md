# 3. `CMD` – Comando Principal

## O que é?

`CMD` define o comando padrão que será executado **quando você iniciar** um contêiner a partir da imagem.

## Para que Serve?

Define o processo principal do contêiner (por exemplo, iniciar o servidor ou script da aplicação). Pode ser sobrescrito na linha de comando do `docker run`.

## Exemplos

### 1. Exemplo Didático

- **Rádio com estação padrão:** imagine uma rádio que, ao ser ligada, já começa sintonizada em uma estação pré-definida (por exemplo, sua estação favorita). Você ainda pode mudar de estação depois, mas essa é a seleção inicial
- **Aplicação Python:** no Docker, o `CMD` funciona da mesma forma, ao iniciar o contêiner, ele executa um comando padrão (como rodar o seu script), mas você pode sobrescrevê-lo se quiser executar outra coisa

### 2. 

```dockerfile
FROM python:3.9

WORKDIR /app
COPY . .

# Comando padrão: executa o script principal
CMD ["python3", "main.py"]
```

Nesse cenário, assim que o contêiner inicia, é como se a "rádio" ligasse automaticamente na sua aplicação (`main.py`), mas você ainda pode passar outro comando via `docker run` para substituir esse comportamento.

## [[ Voltar para: Instruções Básicas do Dockerfile ]](./instrucoes-basicas-dockerfile.md#cmd)