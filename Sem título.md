## 0:00–0:20 — Abertura

_(Tom: claro, objetivo)_

“Este é um sistema de Sistemas Distribuídos em Java: jogadores se avaliam em rede, o servidor calcula médias e divide os times de forma balanceada. Vou resumir o tema, os streams e a serialização.”

---

## 0:20–1:05 — Tema (divisão de times a partir das “votos” = notas)

“O ‘voto’ aqui é avaliação entre jogadores: cada um dá nota de zero a dez para os outros — sem autoavaliação e sem repetir a mesma avaliação. Enquanto o período está aberto, essas notas viram média para cada jogador.”

“Quando o administrador encerra, o servidor ordena todo mundo pela média e aplica um snake draft: distribui os melhores em zigue-zague entre os times, para equilibrar as médias — não é sorteio nem votação direta nos times, é um critério numérico coletivo mais um algoritmo fixo no servidor.”

---

## 1:05–1:45 — Streams

Versão curta (para caber no vídeo):  
“No código, stream é o fluxo de bytes da API `java.io`(29 Output). O projeto define `JogadorOutputStream` e `JogadorInputStream`: classes que embrulham um `DataOutputStream` / `DataInputStream` (31, 40–47 Output) e implementam o contrato de `OutputStream` / `InputStream` — no mesmo espírito dos filtros da biblioteca (composição sobre outro stream). Elas serializam e desserializam arrays de `Jogador` para qualquer origem ou destino, por exemplo o `OutputStream` do socket TCP no `ManipuladorCliente`.”

Por que mudou: deixa claro que não é só “decorator” de nome (em Java os filtros oficiais são `FilterInputStream`/`FilterOutputStream`), mas o mesmo padrão de uso: um stream “de cima” delega para um stream “de baixo” (`Data*` + bytes do socket).

---

## Onde apontar enquanto fala (ordem sugerida)

| O que você está dizendo                                                   | Arquivo                    | Linhas (aponte o dedo/cursor aqui)                                         |
| ------------------------------------------------------------------------- | -------------------------- | -------------------------------------------------------------------------- |
| “fluxo de bytes da `java.io`”, “OutputStream / InputStream”               | `JogadorOutputStream.java` | 29 — `extends OutputStream`                                                |
| mesmo para entrada                                                        | `JogadorInputStream.java`  | 25 — `extends InputStream`                                                 |
| “embrulham DataOutputStream / DataInputStream”, “destino pode ser socket” | `JogadorOutputStream.java` | 31, 40–47 — campo `destino` e construtor que recebe `OutputStream destino` |
| idem para leitura                                                         | `JogadorInputStream.java`  | 27–34 — campo `origem` e construtor com `InputStream origem`               |
| “empacotar / serializar o array”                                          | `JogadorOutputStream.java` | 50–57 — `enviar()` escreve quantidade e cada jogador                       |
| “desempacotar / montar o array”                                           | `JogadorInputStream.java`  | 42–50 — `receber()` lê quantidade e chama `lerJogador()`                   |
| “no socket TCP, na prática”                                               | `ManipuladorCliente.java`  | 139–142 — `LIST_RESP` + `new JogadorOutputStream(..., dos)` + `enviar()`   |

Detalhe extra se sobrar 5 s: no Output, o protocolo binário está no comentário do topo — `JogadorOutputStream.java` 14–24 (e o espelho em `JogadorInputStream.java` 13–23).

---

“A conexão principal é TCP em unicast: um servidor multithread aceita vários clientes; cada um tem uma thread. Detalhe importante: não se fecha o stream de jogador dentro do loop, senão fecha o socket.”

---

## 1:45–2:35 — Serialização

“A serialização é manual: não usa `Serializable` do Java.”

“No TCP, as mensagens têm opcode de um byte — login, listar, avaliar, encerrar — e payloads em tipos binários; listas e times usam o protocolo binário dos `Jogador*Stream`.”

“Já para avisos e resultado ‘para todo mundo’, entra UDP multicast em um grupo da rede, com JSON montado à mão — sem biblioteca — com tipos como aviso e times prontos em texto. TCP para sessão e dados estruturados; multicast para um-para-muitos.”

---

## 2:35–3:00 — Fechamento

“Em três ideias: avaliações geram médias, o snake draft monta os times; streams customizados levam os `Jogador` pelos bytes; dois formatos — binário no TCP e JSON manual no UDP.”