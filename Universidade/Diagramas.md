## **Diagrama de Sequência – Criar Conta**
1. O **Ator** preenche o formulário com e-mail, telefone, CPF e senha e envia para a **TelaCriarConta**.
2. A tela dispara `preencherDados(...)` no **ControleCriarConta**, que internamente chama `validarCPF(cpf:string): boolean`.
3. Confirmado que o CPF é válido e não existe na base, o controller cria a instância de **Cliente** (`<<create>> Cliente`).
4. Em seguida, ele chama `enviarConfirmacao()` no serviço de **Email**, enviando ao usuário o link de ativação da conta.
---
## **Diagrama de Sequência – Fazer Login**
1. O **Ator** informa CPF e senha na **TelaLogin**, que envia `fazerLogin(cpf:string, senha:string): boolean` ao **ControleLogin**.
2. O controller verifica `verificaCPF(cpf:string): boolean`. Se for falso, retorna imediatamente “CPF não cadastrado” à tela.
3. Se o CPF estiver ok, chama `validarSenha(senha:string): boolean`.
    - **Senha correta** → cria e devolve o objeto **Cliente** à interface (`<<create>> Cliente`), permitindo o acesso ao sistema.
    - **Senha incorreta** → entra em loop de retry enquanto `tentativas < 3`, chamando novamente `fazerLogin(...)`.
    - Ao atingir 3 tentativas falhas, executa `bloquearConta(cpf:string): void` e `enviarLinkParaDesbloqueio(): void`, bloqueando a conta e enviando e-mail de desbloqueio.
---
## Diagrama de Sequência – Cadastrar Agendamento
1. O **Ator** informa dia e mês desejados à **TelaCriarAgendamento** (`data:int, mes:int`).
2. A tela solicita `consultarDisponibilidade(data, mes): horarios[]` ao **ControleCriarAgendamento**, que retorna a lista de horários livres.
3. O usuário escolhe um horário (`selecionarHorario(horario:time)`) e a tela chama `realizarAgendamento(dia, mes, horario)`.
4. O controller obtém o `idCliente` logado, cria um novo **Agendamento** (`<<create>> Agendamento(dia, mes, horario, idCliente)`) e aciona `enviarConfirmacao()` no serviço de **Email**.
5. Por fim, retorna à tela `mensagemSucesso()`, confirmando visualmente o agendamento.
---
## Diagrama de Atividade – “Criar Conta”

1. **Início**
    - O usuário envia seus dados para cadastro.
2. **Recepção e Validação**
    - O sistema recebe os dados e verifica se já existe outra conta com o mesmo CPF informado.
3. **Caso exista conta**
    - O sistema informa ao usuário que já há uma conta com aquele CPF e sugere que ele faça login.
    - Se o usuário tiver esquecido a senha, o sistema envia um link de recuperação por e-mail.
    - Depois que o usuário acessa o link, ele pode alterar a senha e retorna ao fluxo de **Fazer Login**.
4. **Caso não exista conta**
    - O sistema verifica o e-mail informado e dispara um link de confirmação.
    - Há uma decisão:
        - **Se o e-mail for confirmado em até 2 h**, prossegue para **Criar conta** (fim do fluxo).
        - **Se não for confirmado** dentro desse prazo, o fluxo se encerra aguardando ou expirando a confirmação.
---
## Diagrama de Atividade – “Fazer Login”

1. **Início**
    - O usuário informa CPF e senha de login.
2. **Verificação de CPF**
    - O sistema checa se o CPF está cadastrado:
        - **Não cadastrado** → informa ao usuário que o CPF não existe e encerra o processo.
        - **Cadastrado** → segue para verificação de senha (inicia contador de tentativas em 1).
3. **Verificação de Senha**
    - O sistema valida se a senha inserida está correta:
        - **Senha correta** → o usuário entra no sistema.
            - Há teste de **primeiro acesso**:
                - **Sim** → solicita nome completo e data de nascimento, depois direciona para **Cadastrar Agendamento**.                    
                - **Não** → fim do fluxo de login.
        - **Senha incorreta** → informa que a senha está errada e avalia o número de tentativas:
            - **Menos de 3 tentativas** → solicita que o usuário digite a senha novamente.
            - **3 ou mais tentativas** → informa que a conta será bloqueada, executa o bloqueio e envia um link de desbloqueio por e-mail; fim do fluxo.
---
## Diagrama de Atividade – “Cadastrar Agendamento”

1. **Início**
    - O usuário informa o dia desejado para agendamento.
2. **Checagem de Disponibilidade**
    - O sistema verifica se, naquele dia, há horários disponíveis.
3. **Decisão de Disponibilidade**
    - **Não há horários** → o sistema solicita ao usuário que informe um novo dia (loop de volta ao início).
    - **Há horários disponíveis** → o sistema informa ao usuário quais horários podem ser agendados.
4. **Confirmação**
    - O usuário escolhe o horário desejado.
    - O sistema envia um e-mail confirmando o agendamento; fim do fluxo.