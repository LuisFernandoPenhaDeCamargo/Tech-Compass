# Multi-stage Builds

## O que são?

**Multi-stage builds** são uma técnica poderosa no Docker que permite usar **várias imagens base** em um mesmo Dockerfile, separando o processo de **construção** do de **execução**. Isso é ideal para manter a imagem final **menor, mais segura e eficiente**.

Em vez de instalar compiladores, ferramentas de build e dependências pesadas diretamente na imagem final, você os usa em um estágio inicial e depois **copia apenas os arquivos realmente necessários** para um estágio posterior mais limpo.

## Por que Usar?

- Reduz o **tamanho da imagem final**
- Evita que ferramentas de build fiquem na imagem de produção
- Melhora a **segurança** e a **portabilidade**
- Mantém o Dockerfile limpo, declarativo e eficiente

## Exemplos

### Exemplo Clássico: Aplicação Go

```dockerfile
# Etapa 1: Build.
FROM golang:1.22 AS builder
WORKDIR /app
COPY . .
RUN go build -o main .

# Etapa 2: Imagem final.
FROM debian:bullseye-slim
WORKDIR /app
COPY --from=builder /app/main .
CMD ["./main"]
```

**O que Acontece Aqui?**

- A imagem `golang` é usada **apenas** para compilar o projeto (ela é grande e cheia de ferramentas de desenvolvimento)
- O binário final `main` é copiado para uma imagem menor (`debian:bullseye-slim`)
- O resultado é uma imagem final **muito menor**, com **apenas o necessário para rodar a aplicação**

### Exemplo Didático

Imagine que você quer preparar um prato e precisa de:

- Utensílios de cozinha pesados (batedeira, panelas, forno industrial)
- Ingredientes básicos (massa, molho)

Você **cozinha tudo em uma cozinha equipada** (primeira imagem) e, no final, **leva só o prato pronto para servir em uma bandeja leve** (imagem final). Não faz sentido carregar o fogão junto com a comida.

## Dicas

- Use nomes claros para os estágios: `AS build`, `AS test`, `AS final`
- Você pode ter quantos estágios quiser (por exemplo, build → test → prod)
- Sempre que possível, combine com imagens minimalistas (como `alpine` ou `distroless`) na imagem final

## Resumo

|        Vantagem        |                    Impacto                    |
|------------------------|-----------------------------------------------|
|      Imagem menor      |  Menor uso de disco e tempo de transferência  |
|Sem ferramentas de build| Maior segurança e menor superfície de ataque  |
|     Build separado     |Possibilita mais controle e clareza no processo|
| Manutenção facilitada  |   Dockerfile mais organizado e sustentável    |

## [[ Voltar para: Otimização do Dockerfile ]](./otimizacao-dockerfile.md#multi-stage-builds)