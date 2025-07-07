# 9. `ARG` – Argumentos

## O que é?

`ARG` define **variáveis de build** que existem apenas durante a etapa de construção da imagem. Diferente de `ENV`, seus valores não ficam disponíveis no contêiner em runtime.

## Para que Serve?

- **Parametrizar o build:** permitir alterar comportamentos do Dockerfile sem modificar o próprio arquivo
- **Controle de versões:** passar versões de dependências, caminhos de download ou flags de compilação dinamicamente
- **Segurança leve:** armazenar valores temporários (como tokens de build) sem incluí-los em runtime

## Exemplos

### Exemplo Didático

Pense num confeiteiro que ajusta a quantidade de açúcar na massa conforme a preferência do cliente, sem precisar alterar a receita base.

**O** `ARG SUGAR_LEVEL=medium` **funciona como um parâmetro de build:** você pode definir `--build-arg SUGAR_LEVEL=low` para um bolo menos doce, ou `high` para um bolo mais doce, sem mudar a receita original.

### Exemplo em Dockerfile

```dockerfile
# Define o argumento de build com valor padrão.
ARG NODE_VERSION=18

# Usa o argumento para escolher a imagem base.
FROM NODE:${NODE_VERSION}

WORKDIR /app
COPY package*.json ./
RUN npm install

COPY . .
CMD ["node", "index.js"]
```

- Para usar outra versão do Node.js ao construir, execute:

```bash
docker build --build-arg NODE_VERSION=16 -t minha-app:node16 .
```

- O `ARG NODE_VERSION` só existe durante o build; depois, no contêiner em execução, `process.env.NODE_VERSION` **não** estará definido

## [[ Voltar para: Instruções Básicas do Dockerfile ]](./instrucoes-basicas-dockerfile.md#arg)