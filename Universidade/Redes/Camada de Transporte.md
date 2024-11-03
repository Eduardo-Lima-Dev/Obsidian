
### 1. **Funções e Serviços da Camada de Transporte**

- A camada de transporte gerencia a comunicação entre processos de sistemas finais e fornece serviços essenciais:
    - **Multiplexação e Demultiplexação**: garante que os dados de diferentes aplicativos sejam entregues ao processo correto.
    - **Protocolos de Transporte (TCP e UDP)**: são os principais protocolos utilizados na Internet para essa camada, cada um com características e usos específicos.

### 2. **UDP (User Datagram Protocol)**

- **Protocolo Não Confiável**: o UDP não garante a entrega dos dados em ordem nem retransmite pacotes perdidos.
- **Características**:
    - Sem conexão prévia entre remetente e receptor.
    - Cabeçalho de segmento simples (8 bytes), sem controle de congestionamento.
    - Usado em aplicações que toleram perda de dados e necessitam de baixa latência, como streaming multimídia e DNS.
- **Checksum**: utilizado para verificar a integridade dos dados, mas sem correção de erros.

### 3. **TCP (Transmission Control Protocol)**

- **Protocolo Confiável e Orientado à Conexão**: oferece uma comunicação ponto-a-ponto confiável, com troca sequencial de dados.
- **Características**:
    - **Conexão Full-Duplex**: permite troca simultânea de dados em ambas as direções.
    - **Estabelecimento de Conexão em 3 vias**: envolve troca de mensagens SYN e ACK para iniciar a comunicação.
    - **Controle de Fluxo**: ajusta a velocidade de envio para não sobrecarregar o receptor.
    - **Controle de Congestionamento**: ajusta a quantidade de dados enviados com base na capacidade da rede, evitando congestionamento.
- **Retransmissão de Dados**: utiliza temporizadores e duplicação de ACKs para detectar e retransmitir pacotes perdidos.

### 4. **Controle de Congestionamento no TCP**

- **Método Fim-a-Fim**: o TCP infere congestionamento a partir de atrasos e perdas observadas, sem suporte direto do IP.
- **Modos de Operação**:
    - **Início Lento**: a janela de congestionamento começa pequena e aumenta gradativamente.
    - **Evitar Congestionamento**: a janela aumenta mais lentamente quando atinge um certo limite.
    - **Critérios de Reação**: múltiplos ACKs duplicados indicam perdas pequenas; uma perda detectada por temporizador sugere congestionamento severo.
- **Objetivo de Equidade**: o TCP ajusta as taxas de envio para garantir que múltiplas conexões compartilhem a largura de banda de forma justa.

### 5. **Modelos de Retransmissão**

- **Go-Back-N**: permite retransmissão cumulativa com múltiplos pacotes não reconhecidos na "janela".
- **Repetição Seletiva**: armazena pacotes recebidos fora de ordem e retransmite apenas os pacotes perdidos.