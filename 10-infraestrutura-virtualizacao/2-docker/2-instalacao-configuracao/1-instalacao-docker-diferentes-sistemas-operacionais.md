# Instalação do Docker em Diferentes Sistemas Operacionais

## Sumário

- [Instalação do Docker no Ubuntu](#instalacao-docker-ubuntu)

## <a id="instalacao-docker-ubuntu">Instalação do Docker no Ubuntu</a>

Siga os passos abaixo para instalar o Docker Engine em sistemas baseados em Ubuntu (20.04, 22.04 ou superior):

```bash
# 1. Atualize o índice de pacotes
sudo apt-get update
```

```bash
# 1. Atualize o índice de pacotes
sudo apt-get update

# 2. Instale dependências para usar o repositório HTTPS
sudo apt-get install -y \
  ca-certificates \
  curl \
  gnupg \
  lsb-release

# 3. Adicione a chave GPG oficial do Docker
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# 4. Configure o repositório estável do Docker
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 5. Atualize novamente o índice e instale o Docker Engine
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

# 6. Verifique a instalação executando o contêiner de teste
sudo docker run --rm hello-world
```

### Observações

* **Permissões**
  Por padrão, é necessário usar `sudo` em todos os comandos do Docker. Se preferir rodar sem `sudo`, adicione seu usuário ao grupo `docker`:

  ```bash
  sudo usermod -aG docker $USER
  # Em seguida, faça logout/login ou execute:
  newgrp docker
  ```

* **Versões específicas**
  Para instalar uma versão específica do Docker Engine, use:

  ```bash
  apt-cache madison docker-ce
  sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
  ```

* **Docker Compose integrado**
  O plugin `docker-compose` já é instalado junto com o Docker Engine; o comando passa a ser `docker compose` (sem hífen).

## [[ Voltar para: Instalação e Configuração ]](./instalacao-configuracao.md#instalacao-docker-diferentes-sistemas-operacionais)