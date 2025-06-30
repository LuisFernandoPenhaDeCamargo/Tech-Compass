# 2. `RUN` – Comando de Execução

## O que é?

`RUN` executa comandos no **contexto da imagem** durante o processo de build.

## Para que Serve?

Permite instalar pacotes, compilar código ou fazer qualquer configuração necessária antes de gerar a imagem final.

## Exemplos

### 1. Exemplo Didático

- **Instalar dependências:** como adicionar ingredientes à massa pronta antes de assar o bolo
- **Configurar o ambiente:** por exemplo, instalar Python ou Node.js

### 2. Exemplo em Dockerfile

```dockerfile
FROM ubuntu:22.04

# Atualiza a lista de pacotes e instala o Python
RUN apt-get update && apt-get install -y python3
```

## [[ Voltar para: Instruções Básicas do Dockerfile ]](./instrucoes-basicas-dockerfile.md#run)