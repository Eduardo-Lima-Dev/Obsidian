Este documento detalha o escopo do projeto de desenvolvimento de software para o segmento de barbearia, bem como descreve o fluxo de trabalho, precificação e processos adotados na prestação de serviços como freelancer.

---

## 1. O Projeto: Catálogo Digital para Barbearia

### Visão Geral
O objetivo é desenvolver um sistema web simples e eficiente que permita ao profissional (barbeiro) gerenciar e exibir seu portfólio de trabalho. O foco central é permitir que o barbeiro faça o upload de fotos dos cortes realizados, criando um catálogo visual dos estilos que ele domina.

### Funcionalidades Principais
* **Upload de Imagens:** Interface para envio de fotos dos cortes.
* **Catálogo/Galeria:** Exibição organizada dos cortes para os clientes visualizarem.
* **Painel Administrativo:** Área restrita para o barbeiro gerenciar o conteúdo.

### Arquitetura e Stack Tecnológica
O projeto prioriza o uso de ferramentas gratuitas (Free Tier) para minimizar custos operacionais para o cliente.
* **Tipo de Aplicação:** Web System (Frontend desacoplado do Backend).
* **Hospedagem Frontend:** [Vercel](https://vercel.com/) (Gratuito, rápido e escalável).
* **Backend e Banco de Dados:** [Supabase](https://supabase.com/) (Open Source Firebase alternative). Será utilizado para:
    * Autenticação (Login do barbeiro).
    * Banco de Dados (PostgreSQL).
    * Storage (Armazenamento das fotos dos cortes).

---

## 2. Metodologia de Trabalho Freelance

O processo de trabalho é dividido em etapas claras para garantir a segurança de ambas as partes e a qualidade da entrega.

### 2.1. Briefing e Levantamento Inicial
* **Reunião de Diagnóstico:** Conversa inicial para entender as dores, problemáticas e necessidades do cliente.
* **Definição de Indispensáveis:** Identificação do que é o "MVP" (Mínimo Produto Viável), ou seja, o que não pode faltar no projeto.
* **Análise de Budget:** Conversa sobre valores disponíveis para investimento.

### 2.2. Precificação e Orçamento
O orçamento é composto pelos custos de infraestrutura (servidores, domínios, etc.) somados ao valor da mão de obra (horas de desenvolvimento).

#### Estratégia de Precificação (Hora Técnica)
* **Nível Júnior / Projetos Iniciais:**
    * Valor: R$ 10,00 a R$ 15,00 por hora.
    * Jornada: 4 horas por dia (Segunda a Sexta).
* **Nível Pleno / Atual:**
    * Valor: R$ 30,00 a R$ 50,00 por hora (dependendo da complexidade).

#### Negociação
* A flexibilidade é chave. É possível diminuir o valor da hora trabalhada para fechar o contrato, contanto que haja uma redução proporcional no escopo do projeto.

### 2.3. Contrato e Formalização
Após o aceite do orçamento, a formalização é feita via contrato (gerado com auxílio de IA para cláusulas padrão).

* **Entregáveis Claros:** O contrato deve listar explicitamente as entregas (X, Y, Z).
* **Escopo Fechado:** Cláusula especificando que mudanças bruscas de escopo implicarão em alteração de valor.
* **Segurança:** Proteção jurídica para ambas as partes quanto a pagamentos e entregas.

### 2.4. Planejamento e Requisitos
* **Tradução de Requisitos:** Apresentação das funcionalidades de forma não-técnica para o cliente.
* **Fluxogramas:** Criação de diagramas de fluxo para demonstrar o caminho do usuário no sistema.
* **Cronograma:** Para projetos com data limite (ex: 5 meses), cria-se um arquivo de cronograma detalhando as datas de cada entrega.

### 2.5. Design e Prototipagem
1.  **Wireframe / Baixa Fidelidade:** Esboço estrutural das telas.
2.  **Alta Fidelidade:** Protótipo visual próximo do resultado final para aprovação antes do código.

### 2.6. Desenvolvimento e Acompanhamento
Esta é a fase que demanda mais tempo. A estratégia de comunicação é vital:

* **Entregas Visíveis:** Focar em apresentar funcionalidades visuais e tangíveis nas reuniões.
* **Reuniões de Validação:**
    * Apresentar o que foi desenvolvido.
    * Perguntar explicitamente: "Está tudo ok?".
    * **Gravação Obrigatória:** Todas as reuniões de entrega devem ser gravadas para servirem como prova de aceite e alinhamento futuro.

### 2.7. Entrega Final e Garantia
* **Termo de Aceite:** Validação final de que o software cumpre o proposto.
* **Garantia:** Período de suporte para correção de bugs (não inclui novas funcionalidades).
    * Prazo: De 3 a 6 meses no máximo.