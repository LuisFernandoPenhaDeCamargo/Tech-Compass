# 6. Por que Usar Docker?

Docker traz diversas vantagens que aceleram e simplificam todo o ciclo de vida de uma aplicação:

- **Portabilidade:** ao empacotar código, dependências e configurações em uma imagem, garante-se que o mesmo contêiner execute de forma idêntica em qualquer ambiente com Docker
- **Isolamento:** cada contêiner roda de maneira segregada (espaço de processo, rede e sistema de arquivos), evitando conflitos entre aplicações no mesmo host
- **Consistência:** usar a mesma imagem em desenvolvimento, testes e produção elimina o problema do "funciona na minha máquina"
- **Leveza e desempenho:** contêineres compartilham o kernel do host e iniciam em milissegundos, consumindo apenas o necessário — muito mais eficiente que máquinas virtuais
- **Escalabilidade:** facilita escalar serviços manualmente (Compose) ou automaticamente (Swarm, Kubernetes), adaptando-se a picos de demanda
- **Agilidade em CI/CD:** builds e testes isolados em contêineres descartáveis tornam o pipeline mais rápido e previsível
- **Ecossistema e comunidade:** amplo suporte de imagens oficiais, ferramentas de orquestração e integrações nativas com provedores de nuvem

Esses benefícios fazem do Docker uma peça-chave em ambientes que demandam rapidez, confiabilidade e flexibilidade.

## [[ Voltar para: Introdução ao Docker ]](./introducao-docker.md#por-que-usar-docker)