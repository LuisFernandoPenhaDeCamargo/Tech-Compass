# 1. Camadas de Imagens

As **camadas de imagens** (layers) são o conceito central que torna as imagens Docker leves e eficientes. Cada instrução de um **Dockerfile** cria uma nova camada sobre a anterior, formando uma pilha imutável:

```dockerfile
FROM ubuntu:22.04               # Camada 1: sistema básico
RUN apt-get update              # Camada 2: atualização de pacotes
RUN apt-get install -y python3  # Camada 3: instalação do Python
COPY app/ /app                  # Camada 4: cópia do código da aplicação
CMD ["python3", "/app/main.py"] # Camada 5: instrução de inicialização
```

## Como Funcionam as Camadas

- **Imutabilidade:** cada camada representa o resultado de uma instrução. Se você altera uma linha do Dockerfile, todas as camadas posteriores são invalidadas e precisam ser recriadas
- **Cache de build:** ao executar `docker build`, o Docker calcula um *hash* para cada instrução (baseado na instrução em si, no estado da camada anterior e no contexto de build)
    + Se já existir uma camada com esse *hash* armazenado, o Docker pula a execução daquela instrução e reutiliza a camada em cache
    + Caso contrário, executa o comando, gera a nova camada e grava seu *hash* nos metadados do daemon
- **Compartilhamento de camadas:** como cada camada é identificada por *hash* e armazenada fisicamente em disco (normalmente em **/var/lib/docker/overlay2**), várias imagens que compartilham instruções iniciais **apontam** para os mesmos diretórios de camada, evitando duplicação de dados no host

## Armazenamento em Disco e Índices de Cache

1. **Diretórios de camadas**
    + Cada camada corresponde a um diretório imutável no storage driver (overlay2, aufs, etc.)
    + Esses diretórios contêm somente os arquivos e alterações introduzidos por aquela camada
2. **Banco de metadados (cache)**
    + O daemon mantém um banco de dados interno que mapeia cada *hash* de instrução → ID de camada
    + Ao reiniciar o serviço Docker (`dockerd`), ele recarrega esses metadados em memória, mantendo o cache de build intacto
3. **Reaproveitamento após reinício:** mesmo após reiniciar a máquina ou o daemon, as camadas gravadas em disco e o índice de *hashes* permanecem disponíveis, permitindo que builds subsequentes continuem usando o cache sem refazer etapas já concluídas

## Vantagens de Usar Camadas

- **Velocidade de build:** apenas as camadas cujo *hash* mudou precisam ser reconstruídas, acelerando builds iterativos
- **Economia de espaço:** camadas idênticas aparecem uma única vez em disco, mesmo que façam parte de múltiplas imagens
- **Baixa transferência de dados:** ao puxar (`docker pull`) uma imagem, o cliente baixa somente as camadas que ainda não possui, reduzindo uso de banda

## Limpeza e Manutenção do Cache

Com o tempo, imagens antigas ou camadas órfãs podem acumular-se:

- **Remover imagens dangling**

```bash
docker image prune
```

- **Limpar todos os recursos não usados**

```bash
docker system prune --volumes
```

- **Limpar cache de build explicitamente**

```bash
docker builder prune
```

- **Otimizar Dockerfiles**
  + Agrupar comandos para diminuir o número de camadas
  + Ordenar instruções para maximizar reuse de cache (etapas menos voláteis primeiro)

Manter a limpeza do cache e a boa organização do Dockerfile garante builds rápidos e um ambiente de storage enxuto.

## [[ Voltar para: Estrutura Interna das Imagens ]](./estrutura-interna-imagens.md#camadas-imagens)