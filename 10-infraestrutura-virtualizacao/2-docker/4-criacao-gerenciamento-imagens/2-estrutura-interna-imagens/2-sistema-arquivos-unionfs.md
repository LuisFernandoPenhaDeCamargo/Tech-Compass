# 2. Sistema de Arquivos UnionFS

O Docker utiliza um **sistema de arquivos em camadas**, baseado em técnicas de *Union File System* (UnionFS), para montar todas as layers de uma imagem como um único sistema de arquivos coeso.

## Como Funciona

1. **Pilhas de camadas:** cada layer é um diretório independente contendo apenas as alterações introduzidas por aquela etapa do Dockerfile
2. **Union Mounting:** quando você inicia um contêiner, o Docker "cola" (faz *mount*) todas as layers em ordem, da mais antiga (base) para a mais recente (top), criando um **view** única e unificada para o processo em execução
3. **Diretório de escrita (Writable Layer):**
   - Sobre as layers somente-leitura da imagem, o Docker adiciona uma **camada de escrita** temporária para o contêiner em execução
   - Todas as alterações realizadas em tempo de execução (novos arquivos, modificações, exclusões) ocorrem nessa camada de escrita, sem alterar as camadas de imagem originais

## Benefícios do UnionFS

- **Imutabilidade das imagens:** as layers de imagem permanecem intactas; qualquer modificação ocorre apenas na camada de escrita do contêiner
- **Desempenho e eficiência:** como somente a camada de escrita é mutável, a sobrecarga de I/O é minimizada, e as camadas somente-leitura podem ser compartilhadas entre múltiplos contêineres
- **Economia de espaço:** arquivos idênticos existentes em layers inferiores não são duplicados; cada instrução adiciona apenas o delta (diferença)

# Exemplos

### 1. Exemplo Visual

```
┌─────────────────────────────────┐
│   Camada de Escrita (contêiner)│  ← modificações em runtime
├─────────────────────────────────┤
│   Camada 5: CMD …               │
├─────────────────────────────────┤
│   Camada 4: COPY app/ /app      │
├─────────────────────────────────┤
│   Camada 3: RUN apt-get install │
├─────────────────────────────────┤
│   Camada 2: RUN apt-get update  │
├─────────────────────────────────┤
│   Camada 1: FROM ubuntu:22.04   │
└─────────────────────────────────┘
          ↓ UnionFS mount
┌─────────────────────────────────┐
│       Sistema de Arquivos      │
│       unificado para o         │
│       contêiner em runtime     │
└─────────────────────────────────┘
```

## [[ Voltar para: Estrutura Interna das Imagens ]](./estrutura-interna-imagens.md#sistema-arquivos-unionfs)