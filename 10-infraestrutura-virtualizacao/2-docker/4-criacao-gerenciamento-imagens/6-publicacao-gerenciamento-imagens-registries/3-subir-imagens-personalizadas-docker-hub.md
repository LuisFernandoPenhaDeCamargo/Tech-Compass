# 3. Subir Imagens Personalizadas para o Docker Hub (`docker push`)

## O que é?

O processo de **subir (push)** uma imagem personalizada ao Docker Hub consiste em enviar, a partir da sua máquina local, uma imagem Docker para um repositório remoto no Docker Hub. Isso torna a imagem disponível para download (`pull`) por qualquer usuário autorizado.

## Para que Serve?

- **Compartilhamento:** permite distribuir sua aplicação em contêiner para colegas de equipe ou comunidade
- **Reutilização:** automatiza deployments em diferentes ambientes (desenvolvimento, staging, produção) sem reconstruir a imagem localmente
- **Versionamento:** mantém múltiplas versões da mesma imagem usando **tags** (`latest`, `v1.0`, `dev`, etc.)

## Exemplos

### Exemplo em CLI

1. **Tagueie** sua imagem local para apontar ao seu repositório no Docker Hub:

```bash
docker build -t seu-usuario/minha-imagem:1.0 .
```

2. **Faça login** (se ainda não estiver autenticado):

```bash
docker login
```

3. **Envie** (`push`) a imagem para o Docker Hub:

```bash
docker push seu-usuario/minha-imagem:1.0
```

4. **Verifique** no Docker Hub — você verá `seu-usuario/minha-imagem` com a tag `1.0` disponível.

---

> **Dica:** use tags significativas (versionamento semântico, `latest` para produção, `dev` para builds de desenvolvimento) e mantenha seu repositório organizado.

## [[ Voltar para: Publicação e Gerenciamento de Imagens em Registries (Docker Hub, etc.) ]](./publicacao-gerenciamento-imagens-registries.md#subir-imagens-personalizadas-docker-hub)