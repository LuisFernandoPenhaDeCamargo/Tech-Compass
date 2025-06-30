# 5. `COPY` e `ADD` – Copiar Arquivos

## O que é?

`COPY` e `ADD` são instruções usadas para transferir arquivos e diretórios do **contexto de build** do host para o sistema de arquivos da imagem.

## Para que Serve?

Permitir que seu código-fonte, arquivos de configuração e outros recursos sejam incluídos na imagem, de modo que fiquem disponíveis em tempo de execução.

## Exemplos

### 1. Exemplo Didático

**Mala de viagem:** imagine que você está preparando uma mala para uma viagem

- Com `COPY`, você simplesmente coloca suas roupas e objetos pessoais dentro da mala (direto e sem tratamento extra)
- Com `ADD`, além de colocar itens na mala, você pode **descompactar uma bolsa fechada** (como um arquivo **.tar.gz**) diretamente dentro dela, ou até mesmo **buscar um item de uma URL** e colocá-lo na mala

#### Quando Usar cada um?

- `COPY`**:** use sempre que possível, para simples cópias; é mais previsível e tem comportamento restrito
- `ADD`**:** use somente quando precisar das funcionalidades extras:
    1. Extrair automaticamente um arquivo **.tar**, **.tar.gz** ou **.zip** no destino
    2. Baixar e copiar arquivos a partir de uma URL remota

### 2. Exemplos em Dockerfile

```dockerfile
# Usando COPY para trazer código-fonte.
COPY src/ /app/src/

# Usando ADD para descompactar um arquivo .tar.gz.
ADD release.tar.gz /app/

# Usando ADD para baixar um arquivo de uma URL.
ADD https://example.com/app/config.json /app/config.json
```

## [[ Voltar para: Instruções Básicas do Dockerfile ]](./instrucoes-basicas-dockerfile.md#copy-add)