# 4. Uso e Elaboração de Dockerfile

## Sumário

1. [O que é o Dockerfile e seu Propósito](#dockerfile-proposito)
2. <a id="instrucoes-basicas-dockerfile">[Instruções Básicas do Dockerfile](./2-instrucoes-basicas-dockerfile/instrucoes-basicas-dockerfile.md)</a> *(redireciona para outro documento)*

## <a id="dockerfile-proposito">1. O que é o Dockerfile e seu Propósito</a>

O **Dockerfile** é um arquivo de texto que contém um conjunto de instruções usadas para **construir imagens Docker**. Cada linha define **como a imagem será composta** — desde a base do sistema até os arquivos, dependências e comandos da aplicação.

> Ele é, essencialmente, **uma receita para construir contêineres** de forma automatizada e reprodutível.

## Por que Usar um Dockerfile?

- **Automação:** elimina a necessidade de configurar manualmente o ambiente
- **Padronização:** garante que todos construam a mesma imagem, da mesma forma
- **Portabilidade:** permite que o ambiente de execução da aplicação seja replicado em qualquer lugar
- **Controle de versões:** alterações no Dockerfile permitem rastrear modificações no ambiente

## Exemplo

### 1. Exemplo Básico de um Dockerfile

```dockerfile
# Usa a imagem oficial do Node.js como base.
FROM node:18

# Define o diretório de trabalho no contêiner.
WORKDIR /app

# Copia os arquivos de dependência.
COPY package*.json ./

# Instala as dependências.
RUN npm install

# Copia o restante da aplicação.
COPY . .

# Expõe a porta 3000
EXPOSE 3000

# Define o comando padrão de execução
CMD ["npm", "start"]
```

Neste exemplo, o Dockerfile define todos os passos necessários para criar um ambiente Node.js funcional a partir de uma imagem oficial.

## [[ Voltar para: Criação e Gerenciamento de Imagens ]](../criacao-gerenciamento-imagens.md#uso-elaboracao-dockerfile)