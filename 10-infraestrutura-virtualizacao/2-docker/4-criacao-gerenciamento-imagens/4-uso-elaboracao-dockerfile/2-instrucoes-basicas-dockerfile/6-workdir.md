# 6. `WORKDIR` – Diretório de Trabalho

## O que é?

A instrução `WORKDIR` define o **diretório de trabalho** para todas as instruções subsequentes no Dockerfile e para o processo quando o contêiner for iniciado.

## Para que Serve?

- Evita o uso repetido de comandos `RUN cd /caminho` em cada instrução
- Garante que `COPY`, `RUN`, `CMD` e outras instruções sejam executadas no diretório correto, mantendo o Dockerfile mais claro e legível

## Exemplos

### Exemplo Didático

**Sala de aula:** imagine que você está em uma escola com vários laboratórios

- Sem `WORKDIR`, toda vez que você quiser usar o laboratório de química, precisa caminhar até lá explicitamente antes de começar
- Com `WORKDIR /lab/quimica`, é como se você entrasse diretamente no laboratório de química, e todos os seus experimentos (`RUN`, `COPY`, etc.) acontecem ali automaticamente

### Exemplo em Dockerfile

```dockerfile
FROM python:3.9

# Define o diretório de trabalho dentro do contêiner.
WORKDIR /app

# As instruções a seguir serão executadas em /app.
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .

# Comando padrão também utilizará /app como diretório atual.
CMD ["python", "main.py"]
```
Após `WORKDIR /app`, não é necessário usar caminhos absolutos em `COPY` ou `RUN`; o contexto passa a ser `/app`.

## Notas e Observações

### `RUN` vs. `WORKDIR`: Escopo e Persistência do Diretório

Quando você usa:

```dockerfile
RUN cd /app && do-something
```

o `cd /app` **só vale dentro** daquele único comando `RUN`; assim que o Docker termina de executar esse `RUN`, ele volta ao diretório padrão (normalmente `/`) para o próximo passo.

Já o `WORKDIR`:

```dockerfile
WORKDIR /app
```

faz com que **todas** as instruções seguintes (`RUN`, `COPY`, `CMD`, etc.) **já** comecem dentro de `/app`, e esse diretório também será o **current working directory** quando o contêiner for iniciado.

**Resumindo**

|                         |             `RUN cd /app && ...`             |                       `WORKDIR /app`                       |
|-------------------------|----------------------------------------------|------------------------------------------------------------|
|       **Escopo**        |    Só dentro do comando `RUN` específico     |  Persiste para todas as instruções seguintes e no runtime  |
|**Leitura do Dockerfile**|        Cada `RUN` é um passo isolado         |Define o contexto contínuo até redefinido por novo `WORKDIR`|
|    **Legibilidade**     |Pode ficar verboso se repetido em vários `RUN`|                    Mais claro e conciso                    |

Por isso, em quase todos os casos `WORKDIR` é a melhor prática para definir seu diretório de trabalho.

### `WORKDIR` também Cria Diretórios Automaticamente

O `WORKDIR` **cria automaticamente o diretório** se ele **não existir** no momento em que a instrução for interpretada pelo Docker durante o build.

```dockerfile
WORKDIR /app/logs
```

Se `/app` ou `/app/logs` **ainda não existirem**, o Docker irá **criá-los automaticamente** no momento dessa instrução. Isso evita a necessidade de adicionar comandos como `RUN mkdir -p /app/logs`.

## [[ Voltar para: Instruções Básicas do Dockerfile ]](./instrucoes-basicas-dockerfile.md#workdir)