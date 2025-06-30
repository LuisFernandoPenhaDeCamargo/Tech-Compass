# 1. `FROM` – Imagem Base

## O que é?

Define a **imagem base** que servirá de ponto de partida para o seu contêiner.

## Para que Serve?

Estabelece o ambiente inicial (sistema operacional ou runtime) sobre o qual você adicionará sua aplicação e dependências.

## Exemplos

### 1. Exemplo Didático

- **Usar uma imagem pronta:** imagine comprar uma massa de bolo pré-pronta. Ela já traz farinha e fermento, e você só precisa adicionar recheio e cobertura
- **Começar do zero (**`scratch`**):** é como fazer a massa do zero, você mesmo mistura farinha, açúcar, ovos, fermento — mais trabalho, mas máximo controle

### 2. Exemplo em Dockerfile

```dockerfile
# Usando Ubuntu 22.04 como base (massa pronta)
FROM ubuntu:22.04

# Ou — começar do zero (massa do zero)
FROM scratch
```

> **Começar do zero** (usando `FROM scratch`) significa partir de um **sistema de arquivos completamente vazio** — sem qualquer biblioteca, utilitário de shell, 
arquivo de configuração de ambiente, usuário ou demais componentes de um sistema operacional típico.
>
> Nesse cenário, **tudo** o que você precisa inserir na imagem deve ser incluído manualmente:
>
> - Binários (por exemplo, um executável compilado estáticamente)
> - Bibliotecas de runtime (como `libc`)
> - Arquivos de configuração (como `/etc/passwd`, `/etc/resolv.conf`)
> - Estrutura de diretórios (por exemplo, `/bin`, `/lib`, `/etc`)
>
> **Importante:** mesmo partindo do zero, o contêiner **ainda usa o kernel do host**; o "do zero" se refere apenas ao espaço de usuário (filesystem).

## [[ Voltar para: Instruções Básicas do Dockerfile ]](./instrucoes-basicas-dockerfile.md#from)