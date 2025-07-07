# Estratégias de Cache (`RUN` e `COPY` Inteligentes)

## Visão Geral

O docker possui um mecanismo de **cache em camadas** que reaproveita instruções idênticas de Dockerfile para acelerar o `docker build`. Utilizar esse cache de forma inteligente torna o processo de build **mais rápido** e **eficiente**, priNcipalmente em pipelines de CI/CD.

## Como o Cache Funciona

Durante a construção da imagem, o Docker analisa **cada instrução** (`FROM`, `COPY`, `RUN`, etc.) em sequência. Ele reutiliza o cache se **todas estas condições forem verdadeiras**:

- A instrução é **idêntica** à de builds anteriores
- O conteúdo **copiado** (como arquivos com `COPY`) **não foi alterado**
- O resultado da instrução **não depende de conteúdo externo modificado**

Se alguma dessas condições mudar, o Docker **invalida o cache** a partir daquela camada e **reconstrói todas as instruções seguintes**.

## Estratégias para Aproveitar Melhor o Cache

### 1. Ordenar `COPY` com Inteligência

Evite copiar tudo de uma vez com `COPY . .`, pois **qualquer alteração** em qualquer arquivo invalidará o cache. Em vez disso:

```dockerfile
# Copie apenas arquivos de dependências primeiro.
COPY requirements.txt .

# Instale as dependências (essa camada raramente muda).
RUN pip install -r requirements.txt

# Agora copie o restante da aplicação.
COPY . .
```

### 2. Use `RUN` Combinados

Cada `RUN` gera uma nova camada. Múltiplos comandos podem ser combinados:

```dockerfile
# Evite:
RUN apt-get update
RUN apt-get install -y curl

# Prefira:

RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*
```

Isso **minimiza camadas** e evita cache desnecessário (além de economizar espaço com limpeza de cache de pacotes).

### 3. Separar Arquivos Mutáveis dos Estáticos

Arquivos que mudam com frequência (ex: **.env**, arquivos temporários) devem ser copiados **o mais tarde possível** no Dockerfile, para que alterações neles não invalidem as camadas de build anteriores.

## Exmplos

### Exemplo Didático

Imagine que você está construindo um prédio, **andar por andar**. Cada comando no Dockerfile é como construir **um andar**:

- O primeiro andar é a fundação (imagem base)
- O segundo andar são as dependências
- O terceiro andar é o código da aplicação
- O quarto andar são configurações finais

Agora, pense em **reformas**:

- Se você **trocar uma janela do 3º andar**, não precisa reconstruir os andares de baixo
- Mas se você **mexer na fundação**, todos os andares acima **precisam ser refeitos**

+ Da mesma forma, se você muda o código-fonte, o Docker **reutiliza o cache das camadas anteriores** (como dependências)
+ Mas se você muda o `requirements.txt`, ele precisa **reinstalar as dependências** e reconstruir tudo que vem depois

### Exemplo em Dockerfile



Imagine que você está construindo uma API Python com Flask:

```dockerfile
FROM python:3.11-slim

WORKDIR /app

# Copie só o arquivo de dependências
COPY requirements.txt .

# Instale dependências
RUN pip install -r requirements.txt

# Agora copie o código da aplicação
COPY . .

CMD ["python", "app.py"]
```

Se você mudar apenas o código, o `requirements.txt` continua igual, e o `pip install` não será reexecutado — ganhando velocidade e evitando reinstalações desnecessárias.

---

## Resumo

| Boas Práticas com Cache                 | Benefício                                           |
| --------------------------------------- | --------------------------------------------------- |
| Ordenar `COPY` de dependências primeiro | Aproveita camadas já construídas                    |
| Usar `RUN` combinados                   | Reduz número de camadas e melhora performance       |
| Evitar `COPY . .` no início             | Impede invalidar todo o cache por arquivos mutáveis |
| Separar código e configuração           | Mantém builds rápidos mesmo com mudanças frequentes |

## [[ Voltar para: Otimização do Dockerfile ]](./otimizacao-dockerfile.md#estrategias-cache)