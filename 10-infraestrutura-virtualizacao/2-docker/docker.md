# Docker

<!--
TODO:
Updater

log: /home/zoe/logs/updater.log

"O gravador não estava subindo" -> "pasta /conteudo/stand estava esquisita" -> "extrai de novo o /conteudo/package-cache/stand.tar"

`sudo install -m 0755 -d /etc/apt/keyrings`

`curl -fsSL https://download.docker.com/linux/$(. /etc/os-release && echo "$ID")/gpg \
    | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg`

`echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
    https://download.docker.com/linux/$(. /etc/os-release && echo "$ID") \
    $(lsb_release -cs) stable" \
    | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`

`sudo apt update`

`sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

(adicionei o usuário ao grupo docker, mas não queria)

`sudo groupadd docker`

`sudo usermod -aG docker $USER`

`newgrp docker`

`groups` (deve listar algo como: lfernando docker)

`sudo apt install -y upx`

`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
`source $HOME/.cargo/env`

`cargo install cross` (É necessário ter o Docker instalado e rodando.)

`cargo install --locked cargo-make`

---

+ Processo de aprendizado do conteúdo
+ Processo de refinamento
+ Padronização
+ Categorização das dúvidas

+ Multi-stage builds podem gerar uma imagem menor? Porque ela vai possuir mais camadas, não? Como isso funciona?
+ Imagens derivadas de programas (como python:3.9) são mais leves do que imagens baseadas em sistemas operacionais (como ubuntu:22.04)?
+ Considerando que imagens são compostas por camadas que se encontram no file system, quando baixamos uma conseguimos ver como elas estão compostas? Como funciona a segurança?

- Criação e Gerenciamento de Imagens → Estrutura Interna das Imagens → O diretório /app é criado por padrão?
- Criar um exemplo prático — como uma analogia com uma receita de bolo — que utilize Dockerfile, imagens e contêineres
- Em relação às seções: a seção "Boas Práticas" requer um certo domínio do assunto. Acho interessante incluir, mais ao final do tema, uma seção "Dificuldades Enfrentadas", destacando situações vivenciadas e como foram superadas.
- Template: limitar o número de linhas por arquivo? Aproximadamente 50 linhas máximas?
- Template: quando o conteúdo do documento não for extenso, não há necessidade de incluir um sumário
- Template: definir o modelo para tabelas, padronizar a seção "Exemplos" e criar um documento explicando a estrutura hierárquica do repositório (há uma estrutura bem definida em study-resource/2025-06-30.md)
- Acredito ser necessário antecipar a categoria Sistemas Operacionais, devido a seções como "Kernel"

Estrutura do Repositório:

01. Introdução ao Docker
02. Instalação e Configuração
03. Arquitetura do Docker
04. Criação e Gerenciamento de Imagens
05. Gerenciamento de Contêineres
06. Networking no Docker
07. Persistência de Dados
08. Docker Compose
09. Segurança no Docker
10. Conceitos Avançados
11. Manutenção e Boas Práticas Gerais
12. Casos de Uso e Integração
13. Documentação
14. Ferramentas Complementares
15. Material Complementar
-->

## Sumário

01. <a id="introducao-docker">[Introdução ao Docker](./1-introducao-docker/introducao-docker.md)</a>  
    Apresentação dos conceitos fundamentais e do que é Docker.
02. <a id="instalacao-configuracao">[Instalação e Configuração](./2-instalacao-configuracao/instalacao-configuracao.md)</a>  
    Como instalar o Docker e configurar o ambiente para uso.
03. <a id="arquitetura-docker">[Arquitetura do Docker](./3-arquitetura-docker/arquitetura-docker.md)</a>  
    Entender a estrutura interna do Docker.
04. <a id="criacao-gerenciamento-imagens">[Criação e Gerenciamento de Imagens](./4-criacao-gerenciamento-imagens/criacao-gerenciamento-imagens.md)</a>  
    Aprender a construir imagens com Dockerfile, explorar a estrutura interna das imagens e publicá-las.
05. <a id="gerenciamento-conteineres">[Gerenciamento de Contêineres](./5-gerenciamento-conteineres/gerenciamento-conteineres.md)</a>  
    Rodar, parar, atualizar e monitorar contêineres.
06. <a id="networking-docker">[Networking no Docker](./6-networking-docker/networking-docker.md)</a>  
    Configurar e gerenciar redes entre contêineres e com o host.
07. <a id="persistencia-dados">[Persistência de Dados](./7-persistencia-dados/persistencia-dados.md)</a>  
    Trabalhar com volumes, bind mounts e estratégias de armazenamento para garantir que os dados não se percam.
08. <a id="docker-compose">[Docker Compose](./8-docker-compose/docker-compose.md)</a>  
    Orquestrar e gerenciar aplicações multi-contêiner com arquivos YAML.
09. <a id="seguranca-docker">[Segurança no Docker](./9-seguranca-docker/seguranca-docker.md)</a>  
    Adotar práticas e mecanismos de segurança para contêineres e imagens.
10. <a id="conceitos-avancados">[Conceitos Avançados](./10-conceitos-avancados/conceitos-avancados.md)</a>  
    Explorar funcionalidades mais complexas, como otimizações, técnicas avançadas de build e integração com outras ferramentas.
11. <a id="manutencao-boas-praticas-gerais">[Manutenção e Boas Práticas Gerais](./11-manutencao-boas-praticas-gerais/manutencao-boas-praticas-gerais.md)</a>  
    Estratégias para manter o ambiente Docker limpo, eficiente e alinhado com as melhores práticas de operação.
12. <a id="casos-uso-integracao">[Casos de Uso e Integração](./12-casos-uso-integracao/casos-uso-integracao.md)</a>  
    Aplicar o conhecimento em cenários reais e integrar Docker a fluxos de trabalho maiores.
13. <a id="documentacao">[Documentação](./13-documentacao/documentacao.md)</a>  
    Reunir todas as informações e referências para facilitar o acesso e atualização do conhecimento.
14. <a id="ferramentas-complementares">[Ferramentas Complementares](./14-ferramentas-complementares/ferramentas-complementares.md)</a>  
    Conjunto de utilitários que estendem e simplificam a experiência com Docker, desde a instalação e gestão visual até a análise de imagens e segurança.
15. <a id="material-complementar">[Material Complementar](./15-material-complementar/material-complementar.md)</a>  
    Seleção de recursos externos que enriquecem o aprendizado e oferecem aprofundamento prático no uso do Docker.

## [[ Voltar para: Infraestrutura e Virtualização ]](../infraestrutura-virtualizacao.md#docker)