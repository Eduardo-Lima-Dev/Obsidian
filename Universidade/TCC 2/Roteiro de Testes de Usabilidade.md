---
tags:
  - Universidade
materia: TCC
tipo: Atividade
---
## 1. Objetivo do Teste
Avaliar a **eficácia**, **eficiência** e **satisfação** das principais funcionalidades do sistema de monitoramento de progresso acadêmico:
1. Cadastro e login  
2. Redefinição de senha  
3. Navegação e uso de filtros (semestre, completas, pendentes, optativas)  
4. Adição de disciplinas optativas  
5. Visualização de progresso (disciplinas completas, pendentes, em andamento e reprovadas)  
6. Alteração de status de disciplina  
7. Consulta de pré-requisitos e dependentes  
8. Exibição de detalhes no modal de disciplina (semestre, tipo, carga horária, pré-requisitos e dependentes)

## 2. Perfil dos Participantes
- **Quantidade**: 5–8 estudantes de graduação (idealmente Engenharia de Software, Sistemas de Informação ou áreas afins)  
- **Critério**: sem experiência prévia com o protótipo  
- **Ambiente**: laboratório ou sessão remota (Zoom/Teams) com gravação de tela e áudio

## 3. Materiais e Métricas
- **Materiais**: computador com navegador, cronômetro, questionários (pré e pós), consentimento informado  
- **Métricas**:  
  - **Tempo em cada tarefa**  
  - **Taxa de sucesso** (completar x sem ajuda)  
  - **Número de erros e obstáculos**  
  - **SUS** (System Usability Scale)  
  - **Feedback qualitativo** (comentários espontâneos)

## 4. Roteiro de Sessão
| Etapa                       | Duração | Atividade                                                                                               |
|-----------------------------|---------|---------------------------------------------------------------------------------------------------------|
| **1. Boas-vindas & Consent.**     | 5 min   | Apresentar objetivo do teste, pedir permissão para gravação, reforçar que “o sistema é testado, não você”. |
| **2. Questionário Pré-teste**     | 5 min   | Dados demográficos (curso, semestre), familiaridade com sistemas acadêmicos                              |
| **3. Tarefas de Usabilidade**     | 45 min  | Conduzir tarefas descritas na próxima seção                                                               |
| **4. Questionário Pós-teste**     | 10 min  | SUS (10 itens) + escala de satisfação (1–5) + perguntas abertas                                         |
| **5. Debriefing & Agradecimento** | 5 min   | Perguntas finais e encerramento                                                                           |

## 5. Tarefas
### T1. Cadastro de Novo Usuário
- **Cenário**: Você acabou de ingressar no curso.  
- **Passos**: Clique em “Cadastre-se”, preencha Nome, Email, Senha, Curso e Ano de Ingresso.  
- **Critério de sucesso**: Conta criada e redirecionado ao dashboard.

### T2. Login
- **Cenário**: Já tem conta.  
- **Passos**: Insira Email e Senha e clique em “Entrar”.  
- **Critério**: Acesso ao dashboard sem erros.

### T3. Redefinição de Senha
- **Cenário**: Esqueceu sua senha.  
- **Passos**: Clique em “Esqueci a senha”, digite seu email, siga o link (simulado) e defina nova senha.  
- **Critério**: Conseguir logar com a nova senha.

### T4. Adicionar Disciplina Optativa
- **Cenário**: Quer incluir uma disciplina livre.  
- **Passos**: Acesse “Minhas Disciplinas → Optativas → Adicionar”, busque “Introdução à Filosofia” e confirme.  
- **Critério**: Disciplina aparece na lista de optativas.

### T5. Filtrar Disciplinas
- **Cenário**: Quer ver apenas pendentes no 4º semestre.  
- **Passos**: Abra o painel de filtros, selecione “Pendentes” e “4º Semestre”.  
- **Critério**: Apenas disciplinas pendentes do 4º são exibidas.

### T6. Visualização de Progresso no Dashboard
- **Cenário**: Conferir status geral.  
- **Passos**: Observe os cards no topo com número de disciplinas concluídas e faltantes.  
- **Critério**: Card “Concluídas” e “Faltam” refletem corretamente seu histórico.

### T7. Alterar Status de Disciplina
- **Cenário**: Deseja marcar “Algoritmos” como concluída.  
- **Passos**: Na lista de disciplinas, clique em “Em andamento” ao lado de “Algoritmos” e selecione “Concluída”.  
- **Critério**: Status é atualizado e refletido no dashboard.

### T8. Consulta de Pré-requisitos e Disciplinas Dependentes
- **Cenário**: Planejando seu próximo semestre.  
- **Passos**: Clique na disciplina “Cálculo I”, abra o modal e leia pré-requisitos e as que dependem dela.  
- **Critério**: Modal mostra claramente lista de pré-requisitos e dependentes.

### T9. Explorar Modal de Detalhes
- **Cenário**: Quer todos os detalhes de “Algoritmos”.  
- **Passos**: Abra o modal de “Algoritmos” e verifique semestre, tipo, carga-horária, pré-requisitos e dependentes.  
- **Critério**: Você consegue listar mentalmente todas as informações apresentadas.

### T10. Marcar Todas as Disciplinas do Semestre como Concluídas
- **Cenário**: Deseja concluir rapidamente todas as disciplinas cursadas em um semestre.  
- **Passos**: No painel de disciplinas, selecione o filtro do semestre desejado e clique em “Marcar tudo como concluído”.  
- **Critério**: Todas as disciplinas daquele semestre mudam para o status “Concluída” e os cards do dashboard são atualizados.
---
## 6. Questionário Pós-teste
1. **SUS**: 10 afirmações com escala 1–5.  
2. **Satisfação Geral**: “Em uma escala de 1 a 5, quão satisfeito você está com o sistema?”  
3. **Feedback Aberto**: “O que você mais gostou?” / “O que você sugere melhorar?”

## 7. Análise e Relatório
- **Tempo médio**, **taxa de sucesso** e **SUS** para cada tarefa.  
- **Problemas recorrentes** e **sugestões** anotados.  
- **Recomendações** de melhorias baseadas em heurísticas de Nielsen e nos dados coletados.
