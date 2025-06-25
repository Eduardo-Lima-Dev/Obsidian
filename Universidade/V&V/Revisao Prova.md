---
tags:
  - Universidade
materia: Validacao
tipo: Revisão
---

# Gabarito da Lista de Exercícios – Verificação e Validação de Software

## 1. Verificação × Validação
- **Verificação**: garantir que o software está sendo construído corretamente conforme os requisitos.
- **Validação**: garantir que o software construído atende à necessidade do usuário final.

## 2. Verificação estática × dinâmica
- **Estática**: verifica artefatos sem executar o código (ex: revisão de código).
- **Dinâmica**: exige execução do software com entradas para observar saídas (ex: testes).

## 3. Diferença entre Falta e Falha
- **Falta**: defeito interno no código.
- **Falha**: manifestação visível de uma falta durante a execução.

## 4. Atividades de teste nas fases do ciclo de vida
Ver tabela baseada no modelo-V com planejamento de testes em paralelo ao desenvolvimento dos artefatos.

## 5. Tipos de teste (resumo)
- **Aceitação**: cliente valida requisitos.
- **Sistema**: teste do sistema completo.
- **Integração**: teste entre módulos.
- **Unidade**: teste de métodos/funções isoladas.
- **Regressão**: checar se o que funcionava continua funcionando.
- **Exploratório**: descobrir falhas fora do script.
- **Desempenho**: tempo de resposta, eficiência.
- **Usabilidade**: facilidade de uso e satisfação.
- **Carga**: comportamento sob grande volume.
- **Segurança**: resistência a ataques, proteção de dados.

## 6. Caso de teste
Contém: entradas, estado inicial, passos, resultado esperado e critério de aprovação.

## 7. Caixa branca × preta + técnicas
- **Caixa branca**: testes com base na estrutura do código (comandos, caminhos, MC/DC, loops).
- **Caixa preta**: testes baseados na especificação (partições, limites, tabelas de decisão, estados).

## 8. Vantagens e desvantagens da caixa branca
+ Alta cobertura, detecta código morto.
- Acoplamento ao código, não detecta omissões.

## 9. Vantagens e desvantagens da caixa preta
+ Foco no usuário, detecta omissões.
- Cobertura interna incerta, difícil rastreamento de falhas.

## 10. Test Smell
Exemplo: *Assertion Roulette* – muitos asserts sem descrição clara.

## 11. Problema SIPPA – Respostas
### a) Classes de equivalência
Para média, nota final e faltas.
### b) Valores-limite
0, 4, 4.01, 7, 7.01, 10.
### c) Pseudocódigo
Inclui regras de aprovação por média, final e reprovações.
### d) Casos de teste
5 comandos diferentes; 6 caminhos.
### e) Complexidade ciclomática
6

## 12. UC003 – Cadastrar Encomenda
Casos com base em fluxo normal e exceções: cliente não existe, valor do sinal inválido etc.

## 13–16. BDD
- Técnica de especificação com exemplos concretos.
- Usa linguagem natural (Gherkin).
- Envolve negócio, QA e devs.

## 17. Integração de Sistemas
- **Top-down**: testa da interface para o núcleo, usa stubs.
- **Bottom-up**: começa no núcleo, usa drivers.
- **Big-bang**: tudo junto, sem harness.

## 18. Drivers × Stubs
- **Stub**: simula módulo chamado.
- **Driver**: simula módulo que chama.

## 19. Jogo da Velha – Casos de Teste
Jogadas válidas/ocupadas, vitória por linha/coluna/diagonal, empate, reinício, alternância de jogador.

## 20. Aceitação × Sistema
Aceitação → cliente valida requisitos.
Sistema → equipe testa sistema completo.

## 21. Mocks strict × lenient
- **Strict**: falha em chamadas inesperadas.
- **Lenient**: ignora chamadas extras.

## 22–23. Código com mocks/stubs
Identificação de simulações, execução e verificação com base nos testes unitários/mocks.
> [!Camada Aplicação] Próximo Assunto 
> [[Lista de Exercı́cios 1|Lista de Exercı́cios 1]]