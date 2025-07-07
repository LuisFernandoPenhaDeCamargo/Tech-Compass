# Imagens Pequenas

Imagens pequenas são versões enxutas de ambientes de execução que contêm apenas o que é estritamente necessário para rodar sua aplicação. Adotar bases minimalistas traz vários benefícios:

- **Velocidade de download e deploy:** menos dados para transferir significa builds e "pulls" mais rápidos
- **Economia de espaço em disco e cache:** camadas menores ocupam menos armazenamento e facilitam o gerenciamento de recursos
- **Superfície de ataque reduzida:** menos pacotes instalados quer dizer menos potenciais vulnerabilidades
- **Melhor performance de CI/CD:** processos de build e teste ficam mais ágeis por lidarem com menos arquivos

A seguir, dois dos casos mais comuns:

## Alpine Linux

- **O que é:** distribuição Linux minimalista (~5 MB) baseada em Musl libc e BusyBox
- **Quando usar:** em fases de desenvolvimento e debug, onde você ainda pode precisar de um shell ou instalar dependências adicionais
- **Vantagens:**
    + Shell disponível (`/bin/ash`) e gerenciador de pacote (`apk`)
    + Depuração e ajustes rápidos diretamente no contêiner
- **Desvantagens:**
    + Diferenças sutis entre Musl e Glibc podem quebrar bibliotecas específicas
    + Nem todos os pacotes comuns estão disponíveis

```dockerfile
FROM alpine:3.18

# Instala apenas o mínimo necessário.
RUN apk add --no-cache python3 py3-pip

WORKDIR /app
COPY . .
RUN pip3 install -r requirements.txt
CMD ["python3", "main.py"]
```

## Distroless

- **O que é:** imagens que contêm somente o runtime essencial para executar seu binário (< 100 KB), sem shell, pacotes de sistema ou gerenciadores de pacote
- **Quando usar:** em ambientes de produção e pipelines maduros, quando o foco é segurança máxima e footprint mínimo
- **Vantagens:**
    + Superfície de ataque quase nula
    + Imagens extremamente pequenas e rápidas de carregar
- **Desvantagens:**
    - Debug e inspeção, sem shell ou ferramentas internas, ficam complexos
    - Exige **multi-stage builds** para compilar seu binário em um estágio e copiar apenas o executável final para a imagem Distroless

```dockerfile
# Stage 1: compilação
FROM golang:1.20 AS builder
WORKDIR /src
COPY . .
RUN CGO_ENABLED=0 go build -o /out/myapp

# Stage 2: runtime mínimo
FROM gcr.io/distroless/base
COPY --from=builder /out/myapp /usr/local/bin/myapp
ENTRYPOINT ["/usr/local/bin/myapp"]
```

## Escolhendo a Melhor Base

|          Critério          |    Alpine    |          Distroless          |
|----------------------------|--------------|------------------------------|
|        **Tamanho**         |    ~5 MB     |           < 100 KB           |
|   **Shell e depuração**    |  Disponível  |        Não disponível        |
|**Gerenciamento de pacotes**|`apk` incluído|        Não disponível        |
|       **Segurança**        |     Boa      |          Excelente           |
| **Complexidade de build**  |    Baixa     |Alta (multi-stage obrigatório)|

## Recomendação de Fluxo

1. **Durante o desenvolvimento**, use Alpine para facilitar depuração e instalação de dependências
2. **Na produção**, migre para Distroless para obter a imagem mais enxuta e segura possível

## [[ Voltar para: Otimização do Dockerfile ]](./otimizacao-dockerfile.md#imagens-pequenas)