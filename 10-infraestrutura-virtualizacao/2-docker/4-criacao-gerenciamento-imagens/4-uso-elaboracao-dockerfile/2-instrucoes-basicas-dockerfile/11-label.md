# 11. `LABEL` – Metadados

## O que é?

Instrução que adiciona **metadados** à imagem, permitindo incluir informações como autor, versão, descrição e outras tags arbitrárias.

## Para que Serve?

- **Documentação interna:** facilita identificar quem criou a imagem, para qual propósito e qual versão
- **Integração com ferramentas:** alguns sistemas de resposta automática lêem labels para organizar pipelines, relatórios de segurança ou políticas de compliance
- **Pesquisa e filtragem:** ao usar `docker images --filter`, você pode buscar imagens por labels específicas

## Exemplos

### Exemplo Didático

Pense em um livro que tem na capa etiquetas informando título, autor e ano de publicação.

- Essas etiquetas ajudam bibliotecários a catalogar e usuários a encontrar informações rapidamente
- No Docker, `LABEL` faz o mesmo: "etiqueta" sua imagem com dados úteis para quem for utilizá-la

### Exemplo em Dockerfile

```dockerfile
FROM alpine:3.18

# Adiciona metadados à imagem.
LABEL maintainer="dev@exemplo.com"
LABEL version="1.2.0"
LABEL description="Imagem mínima para executar o serviço X"

# Resto do Dockerfile...
CMD ["sh"]
```

- `maintainer`**:** contato do responsável pela imagem
- `version`**:** versão da aplicação ou do ambiente
- `description`**:** breve descrição do propósito da imagem

## [[ Voltar para: Instruções Básicas do Dockerfile ]](./instrucoes-basicas-dockerfile.md#label)