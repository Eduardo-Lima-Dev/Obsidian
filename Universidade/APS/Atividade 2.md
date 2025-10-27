**Alunos:**
Luiz Eduardo - 500623
Carlos Jeferson - 552568
Ryan Gonçalves - 508281

## Diagrama

![[Pasted image 20251007092108.png]]

## Caso de Uso (Segunda via do cartão)

# Caso de Uso: Solicitar Segunda Via do Cartão

## Fluxo Principal de Eventos (Fluxo Básico):

1. O usuário acessa o sistema do restaurante universitário.
2. O usuário realiza login com suas credenciais válidas.
3. O sistema autentica o usuário e exibe a tela principal.
4. O usuário seleciona a opção “Solicitar Segunda Via do Cartão”.
5. O sistema exibe as informações da taxa de segunda via e solicita confirmação.
6. O usuário confirma a solicitação e é redirecionado para a tela de pagamento.
7. O usuário realiza o pagamento da taxa via sistema (boleto, PIX, cartão etc.).
8. O sistema valida o pagamento com sucesso.
9. O sistema registra a solicitação de segunda via como “Pendente de Aprovação”.
10. A nutricionista acessa o sistema com sua conta administrativa.
11. A nutricionista visualiza a lista de solicitações pendentes.
12. A nutricionista analisa a solicitação do usuário.
13. A nutricionista aprova a solicitação.
14. O sistema registra a aprovação e gera o novo cartão virtual.
15. O usuário é notificado de que sua segunda via está pronta para uso ou retirada.

## Fluxos Alternativos

### Solicitação Rejeitada pela Nutricionista

1. A nutricionista rejeita a solicitação, informando o motivo.
2. O sistema marca a solicitação como “Rejeitada” e notifica o usuário com o motivo da rejeição.

## Exceções

### Falha no Login do Usuário

1. Se o usuário informar credenciais inválidas, o sistema exibe mensagem de erro e permite nova tentativa.
2. Após 5 tentativas inválidas, a conta pode ser temporariamente bloqueada.

### Pagamento Não Concluído

1. Se o pagamento não for concluído ou for recusado, o sistema informa o erro e não registra a solicitação.
2. O usuário pode tentar novamente ou escolher outro método de pagamento.

### Falha na Comunicação com Sistema de Pagamento

1. Se houver erro na comunicação com o provedor de pagamento, o sistema exibe mensagem de erro e aguarda nova tentativa.

### Erro de Sistema ao Aprovar Solicitação

1. Se houver falha técnica ao aprovar a solicitação, o sistema registra erro e solicita nova tentativa à nutricionista.
