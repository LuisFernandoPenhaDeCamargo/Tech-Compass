# 10. `HEALTHCHECK` – Verificação de Saúde

## O que é?

Instrução que define um comando para o Docker monitorar periodicamente se o contêiner está **funcionando corretamente**.

## Para que Serve?

- **Detectar falhas automaticamente:** permite que o Docker marque o contêiner como "saudável" ou "não saudável" com base na saída do comando
- **Melhorar orquestração:** orquestradores (Docker Swarm, Kubernetes) usam o status de saúde para reiniciar ou redirecionar tráfego de contêineres defeituosos
- **Automação de operações:** facilitar monitoramento e alertas sem configurações externas

## Exemplos

### Exemplo Didático

Imagine um zelador que verifica periodicamente se as luzes de um corredor estão acesas:

- Se a luz apagar, ele registra um alerta e aciona o conserto
- No Docker, o `HEALTHCHECK` faz o mesmo: executa um comando como "ping" na aplicação e sinaliza se ela respondeu

### Exemplo em Dockerfile

```dockerfile
FROM nginx:stable

# Expõe a porta 80 para o serviço web.
EXPOSE 80

# Define a verificação de saúde.
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s \
    CMD curl -f http://localhost/ || exit 1

# Mantém o comando padrão do Nginx.
CMD ["nginx", "-g", "daemon off;"]
```

- `--interval=30s`**:** tempo entre cada checagem
- `--timeout=5s`**:** tempo máximo para a checagem responder
- `--start-period=5s`**:** tempo de espera após o contêiner iniciar antes da primeira checagem
- O comando `curl -f http://localhost/` deve retornar sucesso (`0`) para o contêiner ser considerado **saudável**; caso contrário, é marcado como **não saudável**

## [[ Voltar para: Instruções Básicas do Dockerfile ]](./instrucoes-basicas-dockerfile.md#healthcheck)