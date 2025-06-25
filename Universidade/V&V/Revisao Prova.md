---
tags:
  - Universidade
materia: Validacao
tipo: Revisão
---
## 1. Diferencie **verificação** e **validação**. Quais os objetivos da V&V?
- **Verificação**: “Estamos construindo o **produto certo**?” – checa se cada artefato atende às especificações.
- **Validação**: “Estamos construindo **o produto certo**?” – evidencia que o software satisfaz a necessidade do usuário.
- **Objetivos gerais**: reduzir risco de falhas, encontrar defeitos cedo e fornecer evidência objetiva da qualidade.

## 2. Diferencie **verificação estática** e **verificação dinâmica**.
- **Estática**: analisa artefatos sem executar o código (revisões, linters, análise estática).
- **Dinâmica**: executa o software com dados de teste e observa saídas (testes, profiling).

## 3. Diferencie **falta (fault)** e **falha (failure)**.
- **Falta**: defeito interno introduzido pelo erro humano.
- **Falha**: manifestação visível de uma falta quando o código é executado.

## 4. Em que fase do ciclo de vida ocorrem as seguintes atividades?

| Atividade | Fase em que se **planeja** | Fase em que se **executa** |
|-----------|---------------------------|----------------------------|
| Plano‑mestre de testes | Início do projeto | — |
| **Testes de aceitação** | Levantamento de requisitos | Validação/implantação |
| **Testes de sistema** | Especificação externa | Pós‑integração total |
| **Testes de integração** | Design de arquitetura | Incrementalmente a cada build |
| **Testes de unidade** | Design detalhado / codificação | Durante/ logo após a codificação |

*(modelo‑V)*

## 5. Defina rapidamente cada tipo de teste.
| Tipo | Foco | Momento típico |
|------|------|----------------|
| Aceitação | requisitos de negócio | antes da entrega |
| Sistema | produto completo | após integração |
| Integração | interfaces entre módulos | incremental |
| Unidade | método/função isolada | na codificação |
| Regressão | defeitos reintroduzidos | todo build |
| Exploratório | investigação ad‑hoc | contínuo |
| Desempenho | tempo/uso de recurso | nível sistema |
| Usabilidade | experiência do usuário | UI estável |
| Carga | grande volume | ambiente de teste |
| Segurança | vulnerabilidades | CI + auditorias |

## 6. O que é um **caso de teste**?
Artefato rastreável que define **entradas, estado inicial, passos, resultado esperado e critério de aprovação**.

## 7. Diferencie **testes de caixa branca** e **caixa preta**. Cite as técnicas vistas.
- **Caixa branca**: análise da _estrutura interna_ (cobertura de comandos, decisões, caminhos, MC/DC, laços).
- **Caixa preta**: avaliação do _comportamento externo_ (particionamento de equivalência, valor‑limite, tabela de decisão, transição de estados, BDD).

## 8. Vantagens e desvantagens da **caixa branca**.
**+** Cobertura mensurável, encontra código morto.  
**–** Acoplada à implementação, não revela omissões de requisito, escala mal em sistemas grandes.

## 9. Vantagens e desvantagens da **caixa preta**.
**+** Visão do usuário, detecta requisitos ausentes, reutilizável após refatorações.  
**–** Cobertura interna incerta, depuração mais demorada, explosão combinatória.

## 10. O que é um **test smell**? Dê um exemplo.
*Test smell* = sintoma de que o código de teste é frágil/difícil de manter.  
Ex.: **Assertion Roulette** – vários `assert`s sem mensagem clara; quando falha não se sabe o que quebrou.

## 11. Problema **SIPPA**  
### a) Classes de equivalência  
- Média: `< 4`, `4–7`, `> 7`.  
- Nota final: `< 4`, `≥ 4`.  
- Faltas (%): `≤ 25 %`, `> 25 %`.

### b) Valores‑limite  
0, 4, 4.01, 7, 7.01, 10 (média/nota); 25 % / 25.01 % (faltas).

### c) Pseudocódigo
```python
def resultado(m, nf, faltas):
    if faltas > 25:
        return "Reprovado por falta"
    if m > 7:
        return "Aprovado por média"
    if m >= 4:
        if nf >= 4 and (m + nf)/2 > 5:
            return "Aprovado na final"
        return "Reprovado na final"
    return "Reprovado direto"
```

### d) Casos necessários  
- **Cobertura de comandos**: 5 casos.  
- **Caminhos independentes**: 6.

### e) Complexidade ciclomática  
`V(G) = 6`.

## 12. UC003 – Cadastrar Encomenda (casos de teste)
1. Fluxo principal (1–11).  
2. **CA001** cliente não cadastrado.  
3. **EXC001** sinal < 50 %.  
4. Falha ao gerar número automático.  
5. Impressora indisponível no recibo.

---

## 13. Qual o **objetivo** do BDD? Quais as **vantagens**?
**Objetivo:** converter requisitos em **exemplos concretos de comportamento**, legíveis por todos, que funcionem como testes de aceitação automatizados.  
**Vantagens:** alinhamento de papéis, documentação viva, critérios de pronto claros, fácil automação.

## 14. Qual o **formato** de um cenário BDD?
Linguagem **Gherkin**:

```gherkin
Funcionalidade: ...
  Cenário: ...
    Dado ...
    Quando ...
    Então ...
```

## 15. **Quem participa** da definição dos cenários BDD?
- **Product Owner / Analista de negócio**  
- **QA / Testador**  
- **Desenvolvedores**  
(sessões _Three Amigos_)

## 16. Em que **fase** do desenvolvimento o BDD deve ser aplicado?
Logo após a história entrar no **planejamento da sprint**, **antes** do início da codificação. Os cenários guiam design e desenvolvimento.

---

## 17. Estratégias de **integração de sistemas**

| Abordagem | Pontos positivos | Pontos negativos |
|-----------|-----------------|------------------|
| **Top‑down** | Exercita lógica cedo | Exige muitos *stubs* |
| **Bottom‑up**| Não precisa stubs | UI testada tardiamente |
| **Big‑bang** | Sem code‑harness | Depuração caótica |

## 18. Diferença entre **drivers** e **stubs**
- **Stub**: simula módulo **chamado** pela unidade em teste (usado em top‑down).  
- **Driver**: simula módulo **chamador** da unidade em teste (usado em bottom‑up).

## 19. Jogo da Velha – cenários de teste
1. Jogada em célula livre.  
2. Jogada em célula ocupada.  
3‑5. Vitória por linha, coluna, diagonal (6 cenários).  
3. Empate.  
4. Reinício limpa tabuleiro.  
5. Alternância correta de jogador X/O.

## 20. Diferença entre teste **de aceitação** e teste **de sistema**
- **Aceitação**: conduzido com usuário/cliente para validar requisitos.  
- **Sistema**: conduzido pela equipe QA no produto completo antes da aceitação.

## 21. Diferença entre mocks **strict** e **lenient**
- **Strict Mock**: falha em qualquer chamada inesperada ou fora de ordem.  
- **Lenient Mock**: ignora chamadas extras; mais flexível em refatorações.

---

## 22. Análise do teste `Quando_email_existe_retorna_mensagem_email_existente`

| Item | Resposta |
|------|----------|
| (a) Classe não pronta | `IListaDeEmails` (implementação real do repositório). |
| (b) Mock ou stub? | **Stub** – só se define retorno; não há verificação de interação. |
| (c) Configuração | `new Mock<IListaDeEmails>();` + `Setup(r => r.Existe(...)).Returns(true)`. |
| (d) Execução | Instanciar `EmailController` + chamar `Cadastrar(email_existente)`. |
| (e) Verificação | `Assert.AreEqual("E-mail já cadastrado.", retorno.JsonDataAsString());` |

## 23. Análise do teste `Quando_email_nao_existe_adiciona_na_lista_de_emails`

| Item | Resposta |
|------|----------|
| (a) Classe não pronta | `IListaDeEmails`. |
| (b) Mock ou stub? | **Mock** – há `Verify` de interação e comportamento **Strict**. |
| (c) Configuração | `new Mock<IListaDeEmails>(MockBehavior.Strict);` + `Setup(r => r.Existe(...)).Returns(false)`. |
| (d) Execução | Instanciar `EmailController` + executar `Cadastrar(email_novo)`. |
| (e) Verificação | `repositorioEmails.Verify(r => r.Inserir(email_novo), Times.Once());` |
