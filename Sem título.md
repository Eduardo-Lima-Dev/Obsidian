classDiagram
direction LR

class Usuario {
  +UUID id
  +String nome
  +String email
  +String telefone
  +String senhaHash
  +Role role
  +Boolean ativo
  +Date createdAt
  +Date updatedAt
}

class Cliente {
  +UUID id
  +UUID usuarioId
  +CanalNotificacao canalPreferido
}

class Barbeiro {
  +UUID id
  +UUID usuarioId
  +String bio
  +String[] especialidades
  +Boolean ativo
}

class Servico {
  +UUID id
  +String nome
  +String descricao
  +Integer duracaoMin
  +Decimal preco
  +Boolean ativo
}

class Disponibilidade {
  +UUID id
  +UUID barbeiroId
  +DiaSemana dia
  +LocalTime inicio
  +LocalTime fim
}

class BloqueioHorario {
  +UUID id
  +UUID barbeiroId
  +DateTime inicio
  +DateTime fim
  +String motivo
}

class Agendamento {
  +UUID id
  +UUID clienteId
  +UUID barbeiroId
  +UUID servicoId
  +DateTime inicio
  +DateTime fim
  +StatusAgendamento status
  +CanalNotificacao canalConfirmacao
  +DateTime criadoEm
  +DateTime atualizadoEm
}

class Notificacao {
  +UUID id
  +UUID agendamentoId
  +CanalNotificacao canal
  +StatusNotificacao status
  +String mensagem
  +DateTime enviadoEm
}

class Sessao {
  +UUID id
  +UUID usuarioId
  +String token
  +DateTime expiraEm
  +Boolean ativa
}

class RecuperacaoSenha {
  +UUID id
  +UUID usuarioId
  +String token
  +DateTime expiraEm
  +DateTime usadoEm
}

enum Role {
  CLIENTE
  BARBEIRO
  ADMIN
}

enum StatusAgendamento {
  PENDENTE
  CONFIRMADO
  CANCELADO
  NAO_COMPARECEU
}

enum CanalNotificacao {
  EMAIL
  WHATSAPP
}

enum DiaSemana {
  SEG
  TER
  QUA
  QUI
  SEX
  SAB
  DOM
}

enum StatusNotificacao {
  PENDENTE
  ENVIADA
  FALHA
}

Cliente --> Usuario : 1:1 (perfil)
Barbeiro --> Usuario : 1:1 (perfil)
Agendamento --> Cliente : N:1
Agendamento --> Barbeiro : N:1
Agendamento --> Servico : N:1
Notificacao --> Agendamento : N:1
Disponibilidade --> Barbeiro : N:1
BloqueioHorario --> Barbeiro : N:1
Sessao --> Usuario : N:1
RecuperacaoSenha --> Usuario : N:1
