---
tags:
  - Universidade
materia: GC
tipo: Revisão
---

## Conceitos e Importância

- **Gerência de Configuração** é um conjunto de práticas e processos para controlar e monitorar as alterações em produtos e sistemas de software ao longo de seu ciclo de vida.
- **Objetivo:** manter a integridade e funcionalidade do software, permitindo a identificação, monitoramento e gerenciamento das versões e mudanças.
- **Itens de Configuração**: Compreendem tudo o que faz parte do sistema, como código-fonte, documentação, e demais recursos. A GC visa a identificação, controle de versões, auditoria e relatórios desses itens para assegurar rastreabilidade e consistência.

## **Gerência de Mudanças**:

- **Escopo das Mudanças**: As mudanças no software podem ser pequenas (como correções de bugs) ou maiores (como a introdução de novas funcionalidades). A gerência de mudanças é um componente essencial da GC, pois coordena a solicitação, avaliação e implementação das mudanças.
- **Impacto e Análise de Mudanças**: Para evitar retrabalho e problemas de comunicação, cada mudança precisa ser avaliada quanto ao impacto no sistema e nas equipes. O processo inclui uma análise de custo-benefício e coordenação para garantir que mudanças não resultem em problemas maiores no projeto.

## Principais Problemas e Soluções

1. **Desafios em Equipes Grandes**:
    
    - Em equipes grandes, sincronizar modificações simultâneas em um mesmo artefato é um desafio. O PDF detalha como a GC ajuda a lidar com **conflitos de versões** e **cópias dessincronizadas**, permitindo a rastreabilidade de quem fez cada alteração, quando e por quê.
    - **Perguntas Importantes**: A GC responde a perguntas como "O que mudou e quando?", "Quem fez a mudança?" e "Podemos reverter a mudança?", permitindo transparência e histórico das alterações.
2. **Controle de Versão**:
    
    - **Definição**: O controle de versão é descrito como o alicerce da GC. É um sistema que registra as mudanças em arquivos ao longo do tempo, possibilitando a recuperação de versões específicas e apoio à auditoria de alterações.
    - **Serviços do Controle de Versão**: Inclui identificação e armazenamento de itens de configuração, criação de rótulos e ramificações (branches) e recuperação de configurações em momentos específicos. Ferramentas como Git e Subversion são exemplos comuns de sistemas de controle de versão.

## **Ferramentas e Termos**

- **Controle de Versão**: É o sistema que registra mudanças em arquivos ao longo do tempo, permitindo recuperar versões específicas. Suporta atividades como controle de mudanças e integração contínua.
- **Repositório**: Local onde todas as configurações são armazenadas e acessadas.
- **Baseline**: Versão estável do software a partir da qual novas versões podem ser desenvolvidas.
- **Check-out e Check-in**: Processo de fazer alterações e integrá-las de volta ao repositório.
- **Ramos (Branches)**: Permitem linhas de desenvolvimento paralelas ao desenvolvimento principal.
- **Construção (Build)**: Processo de compilar o sistema com itens de configuração definidos.
# Controle de Mudanças e Integração Contínua

## **Controle de Mudanças**

- Objetivo: **registrar, avaliar e rastrear todas as mudanças** aplicadas ao projeto desde a proposta até a implementação.
- Essencial para projetos com desenvolvimento iterativo, pois assegura rastreabilidade e adapta o software a mudanças no mercado ou nas estratégias de negócio.
- **Impacto das Mudanças**: É fundamental analisar o custo-benefício, impacto no escopo e necessidade de priorização, pois algumas mudanças podem aumentar a complexidade e custo de maneira significativa.

## **Integração Contínua**

- **Definição**: Processo para garantir que mudanças no projeto sejam construídas e testadas rapidamente após serem introduzidas, facilitando o feedback e minimizando problemas de integração.
- Integração contínua geralmente utiliza ferramentas que detectam mudanças no repositório e disparam uma nova build para testes.


> [!Camada Aplicação] Próximo Assunto 
> [[Aula 3 - Repositórios]]