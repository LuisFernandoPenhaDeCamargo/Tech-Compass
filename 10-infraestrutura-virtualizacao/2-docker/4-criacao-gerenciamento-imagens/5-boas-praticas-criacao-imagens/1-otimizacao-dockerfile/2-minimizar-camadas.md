# Minimizar Camadas (Fundir Comandos `RUN`, Evitar Duplicações)

No Docker, cada instrução no Dockerfile (`RUN`, `COPY`, `ADD`, etc.) gera uma nova **camada** na imagem final. Essas camadas são imutáveis e armazenadas separadamente no disco. Quanto mais camadas forem criadas, maior pode ser o tamanho da imagem e mais tempo levará para construí-la, transferi-la e carregá-la.

Minimizar o número de camadas é uma das boas práticas mais importantes para manter suas imagens pequenas, eficientes e rápidas de construir.

## Fundir Comandos `RUN`

Cada comando `RUN` cria uma camada. Por isso, é recomendado **combinar múltiplos comandos shell** em uma única instrução `RUN`, usando `&&` e finalizando com `\` para melhor legibilidade.

### Exemplos

**Exemplo Ruim (Várias Camadas Desnecessárias)**

```dockerfile
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y git
```

**Exemplo Melhor (Uma Única Camada)**

```dockerfile
RUN apt-get update && \
    apt-get install -y curl git && \
    rm -rf /var/lib/apt/lists/*
```

> **Nota:** o `rm -rf /var/lib/apt/lists/*` remove arquivos de cache que não são mais necessários após a instalação. Isso reduz o tamanho da imagem final

## Evitar Comandos Duplicados

Duplicar comandos em diferentes etapas do Dockerfile pode gerar camadas redundantes e aumentar o tempo de build.

## Exemplos

**Exemplo Ruim**

```dockerfile
RUN pip install -r requirements.txt
RUN pip install flask
```

**Exemplo Melhor**

```dockerfile
RUN pip install -r requirements.txt flask
```

## Cuidado com `COPY` e `ADD`

Cada uso de `COPY` e `ADD` também gera uma nova camada. Quando possível, agrupe cópias de arquivos em uma única instrução.

### Exemplos

**Exemplo Ruim**

```dockerfile
COPY app.py /app/
COPY config.yaml /app/
COPY utils.py /app/
```

**Exemplo Melhor**

```dockerfile
COPY . /app/
```

> **Atenção:** certifique-se de que o **.dockerignore** esteja bem configurado para evitar copiar arquivos desnecessários com `COPY .`.


## Quando *não* Fundir Camadas

Apesar da recomendação geral, há casos em que **separar comandos em diferentes camadas pode ser útil para aproveitar o cache** do Docker ou para manter o Dockerfile mais claro e debuggável. Avalie o custo-benefício.

## Resumo

|        Estratégia         |                     Benefício                      |
|---------------------------|----------------------------------------------------|
|   Fundir comandos `RUN`   |  Menos camadas, build mais rápido e imagem menor   |
|    Evitar duplicações     |Reduz camadas desnecessárias e mantém o cache eficaz|
|   Agrupar `COPY`/`ADD`    |      Evita múltiplas camadas para cada cópia       |
|Limpar arquivos temporários|          Reduz o tamanho final da imagem           |

## [[ Voltar para: Otimização do Dockerfile ]](./otimizacao-dockerfile.md#minimizar-camadas)