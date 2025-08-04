# 4. Imagens Oficiais vs. Imagens Personalizadas



## Imagens Oficiais vs. Imagens Personalizadas

Ao trabalhar com Docker Hub, você encontrará dois tipos principais de imagens:

1. **Imagens Oficiais**
2. **Imagens Personalizadas**

### 1. Imagens Oficiais

* **O que são?**
  Imagens mantidas pela equipe Docker ou por fornecedores certificados (por exemplo, `nginx`, `redis`, `python`, `ubuntu`).
* **Características:**

  * **Vetting e segurança:** passam por processo de revisão e são atualizadas regularmente.
  * **Documentação completa:** geralmente vêm com instruções claras sobre uso e variáveis de configuração.
  * **Suporte e compatibilidade:** seguem boas práticas de base e recebem correções de vulnerabilidades.
* **Vantagens:**

  * Confiança e estabilidade para produção.
  * Ótima documentação e comunidade extensa.
* **Quando usar:**

  * Para serviços genéricos (bancos de dados, servidores web, runtimes).
  * Sempre que possível, como ponto de partida, antes de criar algo do zero.

#### Exemplo de uso

```bash
docker pull nginx:latest
docker run -d -p 80:80 nginx:latest
```

---

### 2. Imagens Personalizadas

* **O que são?**
  Imagens criadas por você ou pela sua equipe, que contêm o seu código, dependências e configurações específicas.
* **Características:**

  * **Totalmente sob seu controle:** você escolhe a imagem base, as instruções de build e as otimizações.
  * **Flexibilidade:** pode incluir apenas componentes necessários, adaptados ao seu fluxo de trabalho.
* **Vantagens:**

  * Ambiente exato para sua aplicação.
  * Permite otimizações de tamanho, segurança e performance específicas do seu projeto.
* **Quando usar:**

  * Sempre que precisar empacotar sua aplicação e suas dependências.
  * Para workflows de CI/CD que exigem imagens preparadas sob medida.

#### Exemplo de Dockerfile personalizado

```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]
```

```bash
docker build -t seu-usuario/minha-app:1.0 .
docker push seu-usuario/minha-app:1.0
```

---

### Comparação Rápida

| Critério          | Imagens Oficiais                     | Imagens Personalizadas     |
| ----------------- | ------------------------------------ | -------------------------- |
| **Manutenção**    | Docker Inc. e parceiros              | Sua equipe ou comunidade   |
| **Segurança**     | Atualizações e patches               | Você gerencia atualizações |
| **Flexibilidade** | Genéricas, às vezes genéricas demais | Totalmente adaptáveis      |
| **Tamanho**       | Podem incluir extras                 | Otimizáveis ao mínimo      |
| **Documentação**  | Robusta e padronizada                | Depende de você criar      |

---

**Dica:** comece sempre a partir de uma **imagem oficial** confiável e, em seguida, crie sua **versão personalizada** para incluir seu código e ajustes específicos. Dessa forma você alia a segurança e estabilidade das oficiais com a flexibilidade das suas próprias imagens.

## [[ Voltar para: Publicação e Gerenciamento de Imagens em Registries (Docker Hub, etc.) ]](./publicacao-gerenciamento-imagens-registries.md#imagens-oficiais-vs-imagens-personalizadas)