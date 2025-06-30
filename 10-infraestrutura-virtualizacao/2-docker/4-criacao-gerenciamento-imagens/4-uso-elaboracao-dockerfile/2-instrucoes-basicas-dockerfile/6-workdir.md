# 6. `WORKDIR` – Diretório de Trabalho

## O que é?

A instrução `WORKDIR` define o **diretório de trabalho** para todas as instruções subsequentes no Dockerfile e para o processo quando o contêiner for iniciado.

## Para que Serve?

- Evita o uso repetido de comandos `RUN cd /caminho` em cada instrução
- Garante que `COPY`, `RUN`, `CMD` e outras instruções sejam executadas no diretório correto, mantendo o Dockerfile mais claro e legível

## Exemplos

### Exemplo Didático



* **Sala de aula:** imagine que você está em uma escola com vários laboratórios.

  * Sem `WORKDIR`, toda vez que você quiser usar o laboratório de química, precisa caminhar até lá explicitamente antes de começar.
  * Com `WORKDIR /lab/quimica`, é como se você entrasse diretamente no laboratório de química, e todos os seus experimentos (`RUN`, `COPY`, etc.) acontecem ali automaticamente.

### Exemplo em Dockerfile

```dockerfile
FROM python:3.9

# Define o diretório de trabalho dentro do contêiner
WORKDIR /app

# As instruções a seguir serão executadas em /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .

# Comando padrão também utilizará /app como diretório atual
CMD ["python", "main.py"]
```

* Após `WORKDIR /app`, não é necessário usar caminhos absolutos em `COPY` ou `RUN`; o contexto passa a ser `/app`.

## [[ Voltar para: Instruções Básicas do Dockerfile ]](./instrucoes-basicas-dockerfile.md#workdir)