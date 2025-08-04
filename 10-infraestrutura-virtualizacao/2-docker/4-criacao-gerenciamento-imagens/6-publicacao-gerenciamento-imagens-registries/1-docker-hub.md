# 1. O que é o Docker Hub?

O **Docker Hub** é o registro público oficial de imagens Docker, mantido pela Docker Inc. Ele funciona como um **repositório centralizado** onde você pode:

- **Compartilhar** imagens criadas por você com outros desenvolvedores ou equipes
- **Descobrir** e **baixar** imagens oficiais (maintained by Docker) e da comunidade (por exemplo, `nginx`, `redis`, `node`, entre muitos)
- **Gerenciar** versões e metadados das suas imagens por meio de **tags** e **labels**
- **Automatizar** builds e testes de imagens, integrando-se a repositórios GitHub ou Bitbucket
- **Configurar** repositórios públicos ou privados, controlando quem pode puxar (pull) ou enviar (push) as suas imagens

## Principais Funcionalidades

|      Funcionalidade      |                                    Descrição                                     |
|--------------------------|----------------------------------------------------------------------------------|
|        **Search**        |        Procure por imagens oficiais e de terceiros usando palavras-chave         |
|   **Automated Builds**   |      Vincule um repositório Git e gere imagens automaticamente a cada push       |
|       **Webhooks**       |         Dispare integrações externas (CI/CD) após novos pushes de imagem         |
|**Organizations & Teams** |     Gerencie acesso colaborativo a repositórios privados em nível de equipe      |
|**Docker Official Images**|Imagens mantidas por Docker ("official images") com padrões de segurança e suporte|

## Como Funciona na Prática

1. **Login no CLI**

```bash
# Digite usuário e senha (ou token de acesso).
docker login
```

2. **Push de uma imagem**

```bash
docker tag minha-imagem:latest seu-usuario/minha-imagem:latest
docker push seu-usuario/minha-imagem:latest
```

3. **Pull de uma imagem**

```bash
docker pull seu-usuario/minha-imagem:latest
```

## Exemplos

### Exemplo Didático

Pense no **Docker Hub** como o **GitHub das imagens de contêiner**.

- Você desenvolve um sistema (uma aplicação web, por exemplo) e empacota tudo em uma imagem Docker
- Assim como você versiona seu código no GitHub, você também pode **versionar e publicar** sua imagem no Docker Hub com um simples `docker push`
- Outros desenvolvedores (inclusive seu time) podem **fazer** `docker pull` e executar exatamente a mesma imagem, com o mesmo ambiente, sem precisar configurar nada manualmente

Assim como no GitHub:

- Existem **repositórios públicos** (qualquer pessoa pode baixar e usar)
- E **repositórios privados** (visíveis apenas para você ou sua equipe)
- Também é possível usar **tags**, como `1.0`, `latest` ou `dev`, para versionar suas imagens

---

Com o Docker Hub, toda a sua equipe e a comunidade global têm um ponto único para **colaborar**, **compartilhar** e **descobrir** imagens de contêiner, acelerando fluxos de trabalho de desenvolvimento e implantação.

## [[ Voltar para: Publicação e Gerenciamento de Imagens em Registries (Docker Hub, etc.) ]](./publicacao-gerenciamento-imagens-registries.md#docker-hub)