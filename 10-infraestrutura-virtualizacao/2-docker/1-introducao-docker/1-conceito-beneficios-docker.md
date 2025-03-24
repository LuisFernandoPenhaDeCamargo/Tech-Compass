# Conceito e Benefícios do Docker

<!--
TODO:
- Linkar este ponto com "Máquinas Virtuais"
- Linkar este ponto com "CI/CD"
- Linkar este ponto com "Kernel"
- Linkar este ponto com "Testes Automatizados"
- Linkar este ponto com "Node.js"
- Linkar este ponto com "Docker Swarm"
- Linkar este ponto com "Kubernetes"
-->

## Sumário

- [O que é Docker?](#docker)
- [Para que serve o Docker?](#para-serve-docker)

## <a id="docker">O que é Docker?</a>

**Docker** é uma plataforma de código aberto que permite empacotar e executar aplicações de forma isolada em contêineres (**plataforma de conteinerização**). Contêineres são ambientes independentes que incluem todas as dependências necessárias para a execução de uma aplicação, incluindo:

- **Código-fonte** da aplicação
- **Dependências** (bibliotecas, pacotes, etc.)
- **Variáveis de ambiente**
- **Configurações de sistema**

Essa abordagem garante que o software funcione de maneira consistente em qualquer ambiente, seja no desenvolvimento local, em servidores ou na nuvem.

Ao contrário das máquinas virtuais (VMs), que replicam um sistema operacional completo para cada instância, os contêineres compartilham o mesmo kernel do sistema operacional do host. Isso os torna **mais leves, rápidos e eficientes**, reduzindo o consumo de recursos e melhorando a escalabilidade das aplicações.

## <a id="para-serve-docker">Para que serve o Docker?</a>

O Docker tem diversas aplicações práticas no desenvolvimento, entrega e operação de software. Algumas das principais são:

### 1 Ambientes de Desenvolvimento Consistentes

- **Problema:** um desenvolvedor cria uma aplicação que funciona no seu computador, mas falha ao ser executada em outro ambiente, como um servidor ou a máquina de outro desenvolvedor
- **Solução:** o Docker padroniza o ambiente, garantindo que a aplicação funcione de forma idêntica em **qualquer máquina**, seja local, em um servidor ou dentro de um pipeline CI/CD
- **Exemplo:** um time de desenvolvimento pode usar Docker para definir o mesmo ambiente de desenvolvimento para todos, incluindo a versão exata do Node.js, Python, e outras dependências

### 2 Portabilidade

- **Problema:** migrar uma aplicação de um servidor para outro exige ajustes de configuração e instalação de dependências
- **Solução:** o Docker empacota a aplicação e suas dependências dentro de um contêiner, tornando-a altamente portátil entre diferentes servidores e provedores de nuvem
- **Exemplo:** um aplicativo criado e testado no ambiente local pode ser implantado em produção sem necessidade de modificar o código ou as configurações

### 3 Desempenho e Eficiência

- **Problema:** **máquinas virtuais (VMs)** consomem muitos recursos, pois cada VM possui seu próprio sistema operacional
- **Solução:** o Docker compartilha o kernel do sistema operacional do host, tornando os contêineres mais leves, rápidos e eficientes em relação às VMs
- **Exemplo:** enquanto uma VM pode levar minutos para iniciar, um contêiner Docker sobe em **milissegundos**

### 4 Entrega Contínua (CI/CD)

- **Problema:** pipelines de CI/CD precisam de ambientes consistentes para executar testes e builds sem variações
- **Solução:** o Docker permite que cada etapa do pipeline (build, teste e deploy) seja executada dentro de contêineres **isolados**, garantindo que o ambiente de teste seja idêntico ao de produção
- **Exemplo:** ferramentas de CI/CD como GitHub Actions, Jenkins e GitLab CI utilizam Docker para rodar **testes automatizados** e compilar aplicações de forma previsível

### 5 Execução Isolada de Aplicações

- **Problema:** rodar múltiplas aplicações ou serviços no mesmo servidor pode gerar conflitos (exemplo: portas, dependências ou versões diferentes de bibliotecas)
- **Solução:** cada contêiner Docker roda em um ambiente isolado, possuindo seu próprio espaço de processos, rede, sistema de arquivos e recursos, evitando conflitos com outras aplicações
- **Exemplo:** é possível rodar duas versões diferentes do **Node.js** (exemplo: v16 e v18) no mesmo servidor, sem conflitos, pois cada versão estará em seu próprio contêiner

### 6 Facilidade de Escalabilidade

- **Problema:** escalar uma aplicação manualmente exige a configuração de novos servidores e ambientes, tornando o processo demorado e complexo
- **Solução:** com ferramentas como **Docker Swarm** ou **Kubernetes**, é possível replicar e escalar contêineres de maneira automatizada, ajustando a capacidade conforme a demanda
- **Exemplo:** uma aplicação de e-commerce pode iniciar com apenas uma instância de um contêiner e, em momentos de alta demanda, escalar automaticamente para dez ou mais instâncias

<!-- SA: retomar a elaboração do tópico a partir do subtópico abaixo. -->

## Benefícios do Docker  

A adoção do Docker traz diversas vantagens para o desenvolvimento, implantação e manutenção de aplicações. Alguns dos principais benefícios incluem:  

### 1. **Portabilidade e Consistência**  
Os containers Docker garantem que uma aplicação funcione da mesma maneira em diferentes ambientes, eliminando problemas de compatibilidade entre máquinas. Se um software roda em um container no ambiente de desenvolvimento, ele rodará da mesma forma em produção.  

🔹 **Exemplo:** Uma equipe desenvolve uma aplicação web localmente usando um container Docker. Quando essa aplicação é enviada para um servidor de produção, o container garante que ela funcione exatamente como no ambiente de desenvolvimento.  

### 2. **Eficiência e Menor Consumo de Recursos**  
Diferente das máquinas virtuais, que carregam um sistema operacional inteiro, os containers compartilham o kernel do sistema operacional do host. Isso reduz drasticamente o consumo de recursos, permitindo que várias aplicações sejam executadas simultaneamente sem desperdício de processamento e memória.  

🔹 **Exemplo:** Um servidor que poderia rodar apenas duas máquinas virtuais pode executar **vários containers**, otimizando o uso de CPU e RAM.  

### 3. **Escalabilidade Facilitada**  
O Docker simplifica a escalabilidade horizontal de aplicações. Com ferramentas como **Docker Compose** e **Docker Swarm**, é possível gerenciar múltiplos containers e distribuir cargas automaticamente, garantindo alta disponibilidade.  

🔹 **Exemplo:** Um site de e-commerce pode aumentar o número de containers durante a Black Friday para suportar um alto volume de acessos e reduzir novamente depois do evento.  

### 4. **Rapidez no Desenvolvimento e Implantação**  
Os containers são leves e iniciam rapidamente, tornando os processos de desenvolvimento e implantação mais ágeis. Além disso, permitem o uso de **integração contínua e entrega contínua (CI/CD)**, reduzindo o tempo entre a escrita do código e a disponibilização da aplicação para os usuários.  

🔹 **Exemplo:** Em um fluxo CI/CD, o código atualizado é automaticamente empacotado em um novo container e implantado em produção em poucos segundos.  

### 5. **Isolamento de Ambientes e Maior Segurança**  
Cada container é isolado do sistema operacional do host e de outros containers, evitando conflitos entre aplicações e aumentando a segurança. Além disso, é possível configurar permissões e restrições para cada container, garantindo que apenas os serviços necessários tenham acesso a determinados recursos.  

🔹 **Exemplo:** Um banco de dados pode ser executado em um container isolado para evitar que aplicações externas tenham acesso direto aos seus arquivos.  

### 6. **Facilidade de Manutenção e Reprodutibilidade**  
Docker permite que um ambiente de desenvolvimento completo seja descrito em um arquivo de configuração, chamado **Dockerfile**. Isso facilita a reprodutibilidade, pois qualquer desenvolvedor pode recriar o mesmo ambiente com um simples comando.  

🔹 **Exemplo:** Uma equipe de desenvolvimento pode configurar um **Dockerfile** contendo todas as dependências do projeto. Qualquer novo membro da equipe pode rodar `docker build` e ter o ambiente pronto rapidamente.  

---

## Conclusão  

Docker revolucionou a forma como aplicações são desenvolvidas, testadas e implantadas. Com seus containers leves, portáveis e eficientes, ele permite que equipes de desenvolvimento **trabalhem com mais agilidade**, reduzam custos operacionais e garantam a consistência entre diferentes ambientes.  

Ao adotar Docker, empresas podem melhorar sua produtividade, reduzir falhas na implantação e tornar suas aplicações mais escaláveis e seguras.

## [[ Voltar para: Introdução ao Docker ]](./introducao-docker.md#conceito-beneficios-docker)