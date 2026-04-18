## 0:00–0:20 — Abertura

_(Tom: claro, objetivo)_

“Este é um sistema de Sistemas Distribuídos em Java: jogadores se avaliam em rede, o servidor calcula médias e divide os times de forma balanceada. Vou resumir o tema, os streams e a serialização.”

---

## 0:20–1:05 — Tema (divisão de times a partir das “votos” = notas)

“O ‘voto’ aqui é avaliação entre jogadores: cada um dá nota de zero a dez para os outros — sem autoavaliação e sem repetir a mesma avaliação. Enquanto o período está aberto, essas notas viram média para cada jogador.”

“Quando o administrador encerra, o servidor ordena todo mundo pela média e aplica um snake draft: distribui os melhores em zigue-zague entre os times, para equilibrar as médias — não é sorteio nem votação direta nos times, é um critério numérico coletivo mais um algoritmo fixo no servidor.”

---

## 1:05–1:45 — Streams


---

## 1:45–2:35 — Serialização

Parágrafo 1 — serialização manual

A serialização é manual e explícita: os objetos viram bytes com `writeInt`/`writeUTF`/etc., sem depender do mecanismo `Serializable` do Java — isso está documentado no projeto (`README.md` linhas 3–4 e 34) e materializado nas classes de stream, por exemplo o comentário de que `JogadorOutputStream` “serializa um array de Jogadores em bytes” (`src/streams/JogadorOutputStream.java` linhas 10–12). Para o canal UDP, o JSON também é montado à mão, com comentário de implementação mínima sem dependências externas (`src/utils/JsonMensagem.java` linhas 7–10).

---

Parágrafo 2 — TCP: opcode + payload + Jogador*

No TCP, cada mensagem segue o formato `[1 byte opcode][payload…]`, descrito no cabeçalho de `Protocolo` (`src/network/Protocolo.java` linhas 6–7 e 24–26). As operações que você citou aparecem nas constantes e nos comentários de payload: login `0x01` (`Protocolo.java` linhas 29–30), listar `0x10` / resposta `0x11` (`Protocolo.java` linhas 39–46), avaliar `0x20` (`Protocolo.java` linhas 49–50), encerrar `0x50` / resposta `0x51` (`Protocolo.java` linhas 79–87). O próprio `LIST_RESP` documenta que o servidor manda `JogadorOutputStream` e o cliente lê com `JogadorInputStream.receber()` (`Protocolo.java` linhas 42–45). Na prática, após escrever o opcode da lista, o servidor instancia `JogadorOutputStream` em cima do mesmo `DataOutputStream` do socket (`src/network/ManipuladorCliente.java` linhas 139–142); no encerramento, cada time vem como `numeroTime` + payload da mesma stream (`ManipuladorCliente.java` linhas 300–307, alinhado a `Protocolo.java` linhas 82–86).

---

Parágrafo 3 — UDP multicast + JSON + papéis TCP vs UDP

Para avisos e resultado para todo mundo, o servidor usa UDP multicast: o grupo e a porta estão em constantes (`Protocolo.java` linhas 102–104). O envio monta um `JsonMensagem`, converte com `toJson()` em bytes UTF-8 e dispara um `DatagramPacket` para o grupo (`ServidorMultiThread.java` linhas 95–109); existe atalho `"AVISO"` (`ServidorMultiThread.java` linhas 116–118) e envio dos times como texto multilinha com tipo `"TIMES"` (`ServidorMultiThread.java` linhas 121–142). O JSON string é gerado concatenando chaves e valores em `toJson()`, com escape manual em `esc` (`JsonMensagem.java` linhas 32–49). No cliente, `MulticastSocket` + `joinGroup` e `JsonMensagem.fromJson` ao receber (`ClienteMulticast.java` linhas 33–46). Em uma frase: TCP concentra sessão e dados tipados/opcodes; multicast UDP faz um-para-muitos para notificações (`ClienteInterativo.java` linhas 17–18 comentam o papel da thread UDP em paralelo ao TCP).

---

## 2:35–3:00 — Fechamento

“Em três ideias: avaliações geram médias, o snake draft monta os times; streams customizados levam os `Jogador` pelos bytes; dois formatos — binário no TCP e JSON manual no UDP.”