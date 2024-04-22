---

---

## 1. Requisitos de Negócio

### 1.1 Contexto
Caracterização do problema/oportunidade.

-  O problema identificado reside na dificuldade que indivíduos com limitado conhecimento tecnológico enfrentam ao tentar utilizar aplicativos para gestão financeira. A solução proposta é a criação de um sistema intuitivo que permita a esses usuários administrar suas finanças e dívidas de maneira simplificada.

### 1.2 Posicionamento do Problema
- **O Problema de:** Dificuldade no uso de aplicativos de gerenciamento financeiro por pessoas com conhecimento tecnológico limitado.
- **Afeta:** Indivíduos que não estão familiarizados com a tecnologia, o que pode incluir uma faixa etária mais velha ou pessoas sem acesso regular à educação tecnológica.
- **Cujo impacto é:** Uma gestão ineficiente das finanças pessoais, o que pode levar a atrasos no pagamento de contas, acúmulo de dívidas e estresse financeiro.
- **Uma boa solução seria:** Um sistema intuitivo e acessível de gerenciamento de finanças que permita aos usuários inserir facilmente despesas, prazos e datas de vencimento.

### 1.3 Alternativas e Concorrência
[descrição das alternativas e concorrência]

### 1.4 Posicionamento do Produto
- **Para quem?** Pessoas com conhecimento tecnológico limitado.
- **Que:** Queiram organizar despesas e ter uma gestão financeira adequada.

### 1.5 Objetivos de Requisitos de Negócio:
- Facilitar a administração financeira de maneira simplificada.
- Proporcionar o monitoramento de despesas de forma ágil e eficiente.
- Oferecer uma introdução facilitada ao uso de tecnologias para a gestão financeira e controle de gastos.

---
## 2. Caracterização dos Usuários

### 2.1 Personas

| Nome            | Detalhes                                                                                                                                                                                                                                                                               | Objetivos                                                                                                                                                         |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Maria Silva     | Maria é uma mulher de 50 anos, dona de casa, com conhecimento básico de tecnologia. Ela precisa de uma maneira simples de acompanhar as despesas domésticas e garantir que todas as contas sejam pagas em dia.                                                                         | - Facilitar a administração financeira de maneira simplificada.                             - Proporcionar o monitoramento de despesas de forma ágil e eficiente. |
| João Oliveira   | João tem 65 anos e é aposentado. Ele não possui experiência com smartphones ou aplicativos financeiros. João deseja uma ferramenta que o ajude a controlar seus gastos e a acompanhar o recebimento de sua aposentadoria.                                                              | - Facilitar a administração financeira de maneira simplificada.                             - Proporcionar o monitoramento de despesas de forma ágil e eficiente. |
| Carlos Oliveira | Carlos tem 55 anos e é autônomo. Ele possui um pequeno negócio e precisa de uma maneira simples de controlar suas receitas e despesas comerciais. Carlos prefere uma solução que não exija muito tempo para aprendizado.                                                               | - Facilitar a administração financeira de maneira simplificada.                             - Proporcionar o monitoramento de despesas de forma ágil e eficiente. |
| Fernanda Santos | Fernanda é uma profissional de 39 anos que trabalha em período integral. Ela busca uma ferramenta que a auxilie a acompanhar seus gastos mensais, incluindo contas fixas, alimentação e lazer. Como Fernanda tem pouco tempo livre, ela precisa de uma solução rápida e fácil de usar. | - Facilitar a administração financeira de maneira simplificada.                            - Proporcionar o monitoramento de despesas de forma ágil e eficiente.  |
### 2.2 Ambiente de Usuários

| Nome            | Ambiente de Trabalho                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Maria Silva     | **Plataformas Atuais:** Maria utiliza principalmente um smartphone Android para tarefas simples.                                                                          **Plataformas Novas:** Ela planeja usar o novo sistema principalmente em seu smartphone.                                                                                                **Outros Sistemas:** Maria não usa muitos outros sistemas tecnológicos além de aplicativos de mensagens. Ela precisa que o novo produto seja fácil de integrar ao seu dia a dia. |
| João Oliveira   | **Plataformas Atuais:** João utiliza um smartphone básico sem acesso à internet.                                                                                              **Plataformas Novas:** Ele usará o novo sistema principalmente em seu smartphone.                                                                                                            **Outros Sistemas:** João não interage com muitos outros sistemas, portanto, a integração com o novo produto deve ser direta e sem complicações.                        |
| Carlos Oliveira | **Plataformas Atuais:** Carlos usa um computador desktop para gerenciar seu negócio e um smartphone Android para comunicação.                        **Plataformas Novas:** Ele usará o novo sistema principalmente em seu smartphone.                                                                                                **Outros Sistemas:** Carlos utiliza alguns aplicativos de comunicação e redes sociais, mas está aberto a uma solução integrada e eficiente.                                                                  |
| Fernanda Santos | **Plataformas Atuais:** Fernanda utiliza um computador desktop no trabalho e um smartphone Android para atividades pessoais.                        **Plataformas Novas:** Ela usará o novo sistema principalmente em seu smartphone.                                                                                                **Outros Sistemas:** Fernanda interage com vários aplicativos de produtividade e de mídia social. A nova solução deve complementar esses sistemas existentes.                                                 |
## 3. Requisitos do Produto
[[O que é um requisito?]]
### 3.1 Requisitos Funcionais
[O  que é um requisito Funcional?]
- RF001: **Cadastro de Usuário:**
    - Permitir que os usuários se cadastrem no sistema fornecendo informações básicas, como nome e idade.
- RF002:**Adicionar Despesas:**
    - Permitir que os usuários adicionem novas despesas ao sistema, incluindo detalhes como categoria, valor e data.
- RF003:**Editar Despesas:**
    - Permitir que os usuários editem despesas existentes, alterando detalhes como valor, estado ou data.
- RF004:**Excluir Despesas:**
    - Permitir que os usuários excluam despesas registradas no sistema.
- RF005: **Visualizar Despesas:**
    - Permitir que os usuários visualizem suas despesas registradas em uma lista, organizadas por categoria ou período de tempo.

### 3.2 Requisitos não Funcionais
[O que é um requisito não funcional?]
- RNF001: **Usabilidade:**
    - O sistema deve ser intuitivo e de fácil utilização, adequado para usuários com conhecimento tecnológico limitado.
- RNF002: **Segurança:**
	- O sistema deve garantir a segurança das informações dos usuários, incluindo dados pessoais e financeiros.
- RNF003:1. **Compatibilidade:**
    - O sistema deve ser compatível com uma variedade de dispositivos, garantindo uma experiência consistente para todos os usuários.
- RNF004: **Disponibilidade:**
    - O sistema deve estar disponível 24 horas por dia, 7 dias por semana, com tempo de inatividade mínimo para manutenção programada.