### 1. **Classificação das Redes**

- As redes de computadores são tradicionalmente classificadas pela sua extensão geográfica:
    - **LAN (Local Area Network)**: cobre pequenas áreas como salas ou prédios.
    - **MAN (Metropolitan Area Network)**: cobre áreas metropolitanas, como uma cidade.
    - **WAN (Wide Area Network)**: abrange grandes áreas, podendo cobrir países ou continentes.
    - **Internet**: uma rede global que conecta várias redes no mundo.

### 2. **Definição da Internet**

- A Internet é uma “rede de redes” composta de milhões de computadores interligados (hospedeiros ou sistemas finais), conectados por diversos meios de comunicação como fibra óptica, cabos de cobre, rádio e satélite.
- Os dados trafegam na Internet por meio de pacotes que são gerenciados e enviados pelos roteadores.

### 3. **Protocolos de Rede**

- Protocolos são regras que controlam o envio e recebimento de mensagens entre máquinas, como o TCP/IP e o HTTP.
- Eles definem o formato, a ordem das mensagens e as ações realizadas quando mensagens são recebidas.
- A Internet é regulada por padrões, como os RFCs (Request for Comments) criados pela IETF (Internet Engineering Task Force).

### 4. **Estrutura e Componentes da Internet**

- **Borda da Rede**: onde estão as aplicações e os hospedeiros (ex.: clientes e servidores de Web e e-mail).
- **Núcleo da Rede**: composto por uma malha de roteadores interconectados, responsáveis por transportar os pacotes de dados através da rede.
- **Redes de Acesso e Meio Físico**: meios pelos quais os dispositivos finais se conectam ao roteador mais próximo, incluindo redes residenciais, institucionais e móveis.

### 5. **Estrutura Hierárquica da Internet**

- A Internet possui uma hierarquia composta de ISPs (Internet Service Providers) organizados em níveis.
- Pacotes podem enfrentar atrasos e perdas ao passar por várias redes e roteadores, onde filas de pacotes podem se formar em buffers.

### 6. **Camadas de Protocolos e Modularização**

- A rede é organizada em camadas, onde cada camada executa funções específicas e confia nas camadas inferiores para serviços auxiliares.
- A modularização facilita a manutenção e atualização, tornando as mudanças em uma camada transparentes para as demais.

### 7. **Modelo OSI e TCP/IP**

- O modelo OSI é uma referência conceitual com sete camadas, enquanto o modelo TCP/IP, amplamente implementado, possui quatro camadas:
    - **Aplicação**: suporta as aplicações de rede (FTP, SMTP, HTTP).
    - **Transporte**: cuida da transferência de dados entre hospedeiros (TCP e UDP).
    - **Rede**: realiza o roteamento de pacotes (IP e protocolos de roteamento).
    - **Enlace e Física**: cuida da transmissão de dados entre elementos vizinhos e da transferência de bits nos canais físicos (ex.: Ethernet).

![[Pasted image 20241103152044.png]]
### 8. **Encapsulamento de Dados**

- O encapsulamento é o processo pelo qual cada camada adiciona seu próprio cabeçalho ao dado antes de enviá-lo para a próxima camada, permitindo que as informações sejam adequadamente processadas na rede.


> [!Camada Aplicação] Próximo Assunto 
> [[Camada Aplicação]]
