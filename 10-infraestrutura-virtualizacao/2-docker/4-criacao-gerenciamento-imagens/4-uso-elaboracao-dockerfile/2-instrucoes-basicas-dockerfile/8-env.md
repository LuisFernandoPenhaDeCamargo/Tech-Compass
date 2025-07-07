# 8. `ENV` – Variáveis de Ambiente

## O que é?

Instrução que define **variáveis de ambiente** dentro da imagem, tornando-as disponíveis para processos em tempo de build e em tempo de execução do contêiner.

## Para que Serve?

- **Configurar o comportamento** da aplicação sem alterar o código (por exemplo, definir porta, modo de execução, credenciais de serviços)
- **Passar informações** dinâmicas durante o `docker build` ou ao iniciar o contêiner
- **Padronizar valores** entre diferentes ambientes (desenvolvimento, teste, produção)

## Exemplos

### Exemplo Didático

Imagine que você está preparando um sanduíche em uma cozinha industrial automatizada, onde o mesmo equipamento serve diferentes filiais de restaurantes:

- Cada filial pode pedir o sanduíche com ingredientes diferentes (vegetariano, com bacon, sem picles)
- Em vez de alterar a "máquina" (o código), você define parâmetros antes de rodá-la — por exemplo, `INGREDIENTS=veggie` ou `INGREDIENTS=bacon`

### Exemplo em Dockerfile

```dockerfile
FROM node:18

# Define variáveis de ambiente.
ENV NODE_ENV=production
ENV API_URL=https://api.exemplo.com

WORKDIR /app
COPY . .

RUN npm install

CMD ["npm", "start"]
```

Aqui, `NODE_ENV` e `API_URL` estarão disponíveis para o processo Node.js em `process.env`.

## Notas e Observações

### `ENV` vs. .env: Prioridade e Sobreposição de Variáveis

Quando você combina `ENV` no Dockerfile com um arquivo **.env** do seu projeto (lido por bibliotecas como `dotenv` ou usado pelo Docker Compose), é assim que o fluxo funciona:

1. **Variáveis definidas em** `ENV` **:** são incorporadas à imagem no build e ficam disponíveis no ambiente do contêiner desde o início
2. **Arquivo .env do projeto:**
    - Se você usa uma biblioteca como `dotenv` em sua aplicação, esse arquivo será carregado **em runtime** para popular `process.env`
    - Se você usa **Docker Compose**, o arquivo **.env** é lido pelo Compose **antes** de processar o **docker-compose.yml** (para interpolar variáveis), mas não é automaticamente injetado no contêiner — a menos que você use a diretiva `env_file:` no Compose

**Quem Vence no Empate?**

- Bibliotecas como `dotenv` **não sobrescrevem** variáveis que já existem em `process.env`
- Logo, **o valor definido via** `ENV` (ou passado com `-e`/`--env` ou `env_file:`) **prevalece** sobre o **.env** do projeto

**Exemplo Prático com Node.js +** `dotenv`

```dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
ENV API_URL=https://api.dockerfile.example.com
CMD ["node", "index.js"]
```

Se **index.js** usar `require('dotenv').config()`, e seu **.env** contiver `API_URL=https://api.envfile.example.com`, então `process.env.API_URL` será `https://api.dockerfile.example.com`, pois o valor de `ENV` venceu

## [[ Voltar para: Instruções Básicas do Dockerfile ]](./instrucoes-basicas-dockerfile.md#env)