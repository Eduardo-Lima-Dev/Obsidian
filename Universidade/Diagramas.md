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