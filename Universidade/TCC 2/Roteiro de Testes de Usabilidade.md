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

## 4. Cenário
> “Você é um estudante de Engenharia de Software que deseja acompanhar e gerenciar seu progresso acadêmico. Use este sistema para realizar uma sequência de tarefas típicas do seu dia a dia.”

## 5. Tarefas

| Nº  | Tarefa                                                        | Critério de Sucesso                                           |
|-----|---------------------------------------------------------------|---------------------------------------------------------------|
| T1  | **Login**: Acesse o sistema com email e senha.                | Entrar no dashboard sem erros.                                |
| T2  | **Cadastro**: Crie uma nova conta (nome, curso, semestre, email e senha). | Receber confirmação de cadastro e redirecionamento ao login. |
| T3  | **Recuperar senha**: Acesse a tela de “Esqueci a senha” e peça um link de recuperação. | Ver mensagem de que o e-mail foi enviado. |
| T4  | **Criar disciplina optativa**: Cadastre uma nova disciplina optativa (nome, tipo “livre/obrigatória”). | Ver a nova optativa listada. |
| T5  | **Adicionar optativa existente**: Escolha uma disciplina já cadastrada no BD e adicione-a ao seu plano. | Disciplina exibida em “Optativas”. |
| T6  | **Alterar status de disciplina**: Marque uma disciplina pendente como “Concluída” ou “Reprovada”. | Status atualizado corretamente. |
| T7  | **Marcar todas as disciplinas do semestre como concluídas**: Use a opção de “concluir tudo” em um semestre. | Todas as do período mudam para “Concluídas”. |
| T8  | **Filtrar disciplinas**: Aplique filtros “Completas”, “Pendentes”, “Optativas” e “Atrasadas”. | Apenas itens do tipo selecionado aparecem. |
| T9  | **Visualizar detalhes de disciplina**: Clique em uma disciplina para ver carga horária, tipo, semestre, pré-requisitos e disciplinas dependentes. | Card exibe corretamente todas as informações. |

---
## 6. Métricas Coletadas
- **Taxa de sucesso** por tarefa (participantes que completaram sem ajuda).
- **Tempo médio** para cada tarefa.
- **Número de erros** e pontos de auxílio.
- **Comentários qualitativos** (dificuldades, elogios, sugestões).

## 7. Análise e Relatório
- **Tempo médio**, **taxa de sucesso** e **SUS** para cada tarefa.  
- **Problemas recorrentes** e **sugestões** anotados.  
- **Recomendações** de melhorias baseadas em heurísticas de Nielsen e nos dados coletados.
