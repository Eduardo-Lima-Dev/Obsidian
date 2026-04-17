## 0:00–0:20 — Abertura

_(Tom: claro, objetivo)_

“Este é um sistema de Sistemas Distribuídos em Java: jogadores se avaliam em rede, o servidor calcula médias e divide os times de forma balanceada. Vou resumir o tema, os streams e a serialização.”

---

## 0:20–1:05 — Tema (divisão de times a partir das “votos” = notas)

“O ‘voto’ aqui é avaliação entre jogadores: cada um dá nota de zero a dez para os outros — sem autoavaliação e sem repetir a mesma avaliação. Enquanto o período está aberto, essas notas viram média para cada jogador.”

“Quando o administrador encerra, o servidor ordena todo mundo pela média e aplica um snake draft: distribui os melhores em zigue-zague entre os times, para equilibrar as médias — não é sorteio nem votação direta nos times, é um critério numérico coletivo mais um algoritmo fixo no servidor.”

---

## 1:05–1:45 — Streams

“No código, stream é a API `java.io`: o projeto usa `JogadorOutputStream` e `JogadorInputStream`, no estilo Decorator, para empacotar e desempacotar arrays de `Jogador` em qualquer destino — inclusive o socket TCP.”

“A conexão principal é TCP em unicast: um servidor multithread aceita vários clientes; cada um tem uma thread. Detalhe importante: não se fecha o stream de jogador dentro do loop, senão fecha o socket.”

---

## 1:45–2:35 — Serialização

“A serialização é manual: não usa `Serializable` do Java.”

“No TCP, as mensagens têm opcode de um byte — login, listar, avaliar, encerrar — e payloads em tipos binários; listas e times usam o protocolo binário dos `Jogador*Stream`.”

“Já para avisos e resultado ‘para todo mundo’, entra UDP multicast em um grupo da rede, com JSON montado à mão — sem biblioteca — com tipos como aviso e times prontos em texto. TCP para sessão e dados estruturados; multicast para um-para-muitos.”

---

## 2:35–3:00 — Fechamento

“Em três ideias: avaliações geram médias, o snake draft monta os times; streams customizados levam os `Jogador` pelos bytes; dois formatos — binário no TCP e JSON manual no UDP.”