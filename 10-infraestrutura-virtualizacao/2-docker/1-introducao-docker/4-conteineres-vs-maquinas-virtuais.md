# 4. Contêineres vs. Máquinas Virtuais

Ao contrário das máquinas virtuais, que replicam um sistema operacional completo para cada instância, os contêineres compartilham o mesmo kernel do sistema operacional do host. Isso os torna **mais leves, rápidos e eficientes**, reduzindo o consumo de recursos e melhorando a escalabilidade das aplicações.

|      Característica      |                                  Contêineres                                  |                    Máquinas Virtuais                   |
|--------------------------|-------------------------------------------------------------------------------|-------------------------------------------------------|
|     **Arquitetura**      |   Compartilham o mesmo kernel do host; cada contêiner é um processo isolado   |    Cada VM executa um hipervisor e seu próprio sistema operacional completo           |
|**Sobrecarga de Recursos**|Muito leve — inicia em milissegundos e consome apenas o que a aplicação precisa|Mais pesado — cada VM carrega um SO completo, demora segundos a minutos para iniciar|
|  **Tamanho da Imagem**   |                 Pequeno (tamanho de aplicação + dependências)                 |                  Grande (SO completo + aplicação + dependências)                  |
|      **Isolamento**      |             Bom isolamento de processo e rede; compartilha kernel             |                 Isolamento forte: cada VM possui kernel próprio                 |
|    **Portabilidade**     |           Imagens menores e padronizadas; mais ágeis de distribuir            |                Imagens grandes; distribuição e startup mais lentos                    |
|    **Gerenciamento**     |              Ferramentas como Docker, Kubernetes, Docker Compose              |                 Ferramentas como VMware, Hyper-V, KVM, VirtualBox                     |

## Quando Usar Cada um

Contêineres

- Em **microserviços**, onde cada serviço roda de forma independente e pode ser escalado rapidamente
- Em **pipelines de CI/CD**, para tarefas de build, teste e deploy ágeis
- Para **ambientes de desenvolvimento**, garantindo que "funciona na minha máquina" se replica em produção

Máquinas Virtuais

- Quando é necessário **isolamento completo** de kernel
- Em **cenários legados** que dependem de configurações de SO específicas ou de hipervisores
- Para **segurança mais rígida**, quando o compartilhamento de kernel não atende aos requisitos de compliance

Essa comparação ajuda a entender por que o Docker (e a containerização) tornou-se tão popular: ele combina portabilidade e leveza, mantendo isolamentos suficientes para a maioria das aplicações modernas.

## [[ Voltar para: Introdução ao Docker ]](./introducao-docker.md#conteineres-vs-maquinas-virtuais)