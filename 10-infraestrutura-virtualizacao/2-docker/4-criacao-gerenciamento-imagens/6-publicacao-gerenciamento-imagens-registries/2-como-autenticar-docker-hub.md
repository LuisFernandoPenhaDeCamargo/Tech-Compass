# 2. Como Autenticar no Docker Hub (`docker login`)?

Para enviar imagens para o Docker Hub (ou puxar de repositórios privados), é necessário **autenticar** sua sessão do Docker CLI. A autenticação garante que apenas usuários autorizados possam fazer **push** em repositórios protegidos ou acessar imagens privadas.

## O que é?

Autenticar no Docker Hub significa **fazer login** no seu registro de imagens, entregando suas credenciais (usuário/senha ou token) ao Docker CLI, que então mantém uma sessão válida para operações subsequentes.

## Para que Serve?

- **Enviar imagens privadas** (`docker push`) sem receber erros de permissão
- **Baixar imagens privadas** (`docker pull`)
- **Automatizar pipelines de CI/CD**, usando tokens de acesso ao invés de senhas
- **Gerenciar** vários registros (Docker Hub, AWS ECR, GitHub Packages) de forma transparente

## Passo a Passo

1. **Login interativo**

No terminal, execute:

```bash
docker login
```

Você será solicitado a informar:

- **Username:** seu nome de usuário no Docker Hub
- **Password:** sua senha (ou [token de acesso](https://hub.docker.com/settings/security) para maior segurança)

2. **Login via argumentos**

Para scripts ou automações, você pode passar credenciais diretamente (menos seguro em terminais compartilhados):

```bash
docker login --username meu-usuario --password meu-token
```

3. **Logout**

Para encerrar sua sessão local:

```bash
docker logout
```

## Exemplos

### Exemplo em CI/CD

Em um pipeline do GitHub Actions, use um *secret* para armazenar o token e adicionar este passo antes de publicar imagens:

```yaml
- name: Log in to Docker Hub
    run: echo "${{ secrets.DOCKERHUB_TOKEN }}" | docker login --username ${{ secrets.DOCKERHUB_USER }} --password-stdin

- name: Build and psuh
    run: |
        docker build -t ${{ secrets.DOCKERHUB_USER }}/minha-app:latest .
        docker push ${{ secrets.DOCKERHUB_USER }}/minha-app:latest
```

> **Dica de segurança:** prefira **tokens de acesso** no lugar da sua senha de conta, e use `--password-stdin` para não expor suas credenciais nos históricos de comandos.

## [[ Voltar para: Publicação e Gerenciamento de Imagens em Registries (Docker Hub, etc.) ]](./publicacao-gerenciamento-imagens-registries.md#como-autenticar-docker-hub)