# 7. `EXPOSE` – Exposição de Portas

## O que é?

Instrução que **documenta** quais portas o contêiner irá escutar em tempo de execução.

## Para que Serve?

- Indicar à imagem quais portas devem estar disponíveis para comunicação entre contêineres ou entre contêineres e o host
- Auxiliar ferramentas de orquestração (como Docker Compose) a mapear automaticamente portas documentadas.

> **Importante:** o `EXPOSE` **não publica** a porta no host — para isso, é necessário usar `docker run -p` ou configuração equivalente em Compose.

## Exemplos

### Exemplo Didático

`EXPOSE` **é como colocar uma campainha do lado de fora da casa:** ela indica onde alguém pode tocar para chamar, mas **não abre o portão automaticamente** — é você (com `-p`) que decide se e como ela será conectada ao lado de fora.

### Exemplo em Dockerfile

```dockerfile
# Define que o contêiner escutará na porta 3000.
EXPOSE 3000
```

Depois de construir a imagem, você publica a porta ao iniciar o contêiner:

```bash
docker build -t minha-app .
```

```bash
docker run -p 3000:3000 minha-app
```

Dessa forma, o `EXPOSE` documenta a porta 3000, e o `-p` no `docker run` efetivamente a conecta ao host.

## Notas e Observações

### `EXPOSE` vs. `-p`: Declarando e Publicando Portas

**1. Como Funcionam** `EXPOSE` **e** `-p` **em Conjunto?**

- A instrução `EXPOSE 3000` **declara** (documenta) que dentro do **contêiner** há um serviço escutando na porta 3000. Ela **não** faz nenhuma configuração de rede no host
- Ao executar `docker run -p 8000:3000 minha-app`, você está dizendo:
    + `8000` é a porta do **host** (seu computador ou servidor)
    + `3000` é a porta **internamente no contêiner** — a mesma que você expôs com `EXPOSE`
- Dessa forma, as requisições que chegam na porta `8000` do host são **encaminhadas** para a porta 3000 dentro do contêiner

**2. A Aplicação Precisa Estar Realmente Escutando na Porta Exposta?**

Sim, o Docker só faz o **encaminhamento** de rede; quem efetivamente "escuta" na porta 3000 é o seu serviço ou aplicação dentro do contêiner. Se a aplicação não estiver configurada para atender naquela porta, não haverá resposta, mesmo que você tenha exposto e mapeado corretamente.

## [[ Voltar para: Instruções Básicas do Dockerfile ]](./instrucoes-basicas-dockerfile.md#expose)