# 5. Casos de Uso do Docker

Os casos de uso ajudam a contextualizar onde a tecnologia brilha na prática. Abaixo, alguns exemplos comuns que ilustram o valor do Docker:

### 1. Ambientes de Desenvolvimento Reprodutíveis

- **Problema:** o código funciona na máquina de um desenvolvedor, mas falha em outro ambiente devido a diferenças de versão de runtimes, bibliotecas ou configurações
- **Solução:** empacotar todo o ambiente (linguagem, dependências e configurações) em um contêiner único, garantindo que todos usem exatamente a mesma imagem
- **Exemplo:** um time define uma imagem Docker com Python 3.11 e Flask, e todos executam o mesmo `docker run`, eliminando "funciona na minha máquina"

### 2. Integração Contínua e Entrega Contínua (CI/CD)

- **Problema:** pipelines de build e teste apresentam resultados inconsistentes quando executados em ambientes diferentes (servidor de CI vs. máquina local)
- **Solução:** usar contêineres em cada etapa do pipeline, isoland build, teste e deploy em imagens idênticas ao ambiente de produção
- **Exemplo:** no GitHub Actions, o job de testes roda dentro de contêiner: node:16, garantindo que testes rodem sempre no mesmo ambiente

### 3. Microserviços

- **Problema:** aplicações monolíticas são difíceis de escalar e atualizar sem causar impacto em toda a stack
- **Solução:** quebrar a aplicação em serviços independentes, cada um em seu próprio contêiner, permitindo escalar, atualizar ou reiniciar um serviço sem afetar os demais
- **Exemplo:** no docker-compose.yml, define-se serviços API, auth e DB; cada um roda em contêineres separados, facilitando manutenção e escalonamento individual

### 4. Testes Automatizados

- **Problema:** testar em um ambiente "sujo" (restos de builds anteriores, caches indefinidos) gera falsos positivos ou erros esporádicos
- **Solução:** criar contêineres descartáveis para cada suíte de testes, garantindo um ambiente limpo e reproduzível a cada execução
- **Exemplo:** a etapa de teste em CI usa `docker run --rm test-image` para rodar testes e descartar o contêiner logo após, sem resíduos

### 5. Aplicações Legadas em Contêineres

- **Problema:** sistemas antigos ou monolíticos dependem de versões específicas de bibliotecas e de configurações de SO que são difíceis de reproduzir
- **Solução:** "dockerizar" a aplicação legada, encapsulando todas as dependências e configurações em uma imagem, simplificando deploy e evitando conflitos
- **Exemplo:** um servidor antigo que roda PHP 5.6 é empacotado em um contêiner `php:5.6-apache`, garantindo que tudo funcione igual em qualquer hospedagem

### 6. Prototipagem Rápida e POCs (Proof of Concept)

- **Problema:** configurar manualmente um ambiente completo para testar uma ideia consome tempo e recursos, retardando validações
- **Solução:** criar e descartar ambientes completos em minutos usando contêineres, permitindo validar conceitos sem investimento pesado em infraestrutura
- **Exemplo:** para testar um novo serviço em Go, a equipe executa `docker run --rm golang:1.20 go run main.go` e avalia o POC instantaneamente

### 7. Escalonamento Dinâmico

- **Problema:** ajustar manualmente a quantidade de servidores durante picos de tráfego é demorado e sujeito a erro
- **Solução:** usar orquestradores para replicar e escalar contêineres de forma automatizada, de acordo com métricas de uso
- **Exemplo:** um e-commerce sobe de 2 para 10 réplicas do serviço web automaticamente quando a CPU ultrapassa 70%, sem intervenção manual

### 8. Isolamento de Serviços

- **Problema:** rodar múltiplos serviços sensíveis (como bancos de dados e caches) no mesmo host gera conflitos de portas, dependências e configurações
- **Solução:** executar cada serviço em seu próprio contêiner, garantindo isolamento de processos, redes e volumes, e evitando interferências entre eles
- **Exemplo:** um cache Redis e um banco PostgreSQL rodam simultaneamente no mesmo servidor sem conflitos de porta ou biblioteca, pois cada um está containerizado

## [[ Voltar para: Introdução ao Docker ]](./introducao-docker.md#conteineres-vs-maquinas-virtuais)