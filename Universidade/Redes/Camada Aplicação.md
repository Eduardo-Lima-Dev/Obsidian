
### 1. **Princípios das Aplicações de Rede**

- As aplicações de rede operam na camada de aplicação e são executadas em sistemas finais, sem interação direta com dispositivos no núcleo da rede. Exemplos de aplicações incluem e-mail, Web, mensagens instantâneas, login remoto, telefonia via Internet e jogos multiusuário.

### 2. **Arquiteturas de Aplicação**

- **Cliente-Servidor**: o cliente se comunica com um servidor sempre ativo com endereço IP fixo. O cliente inicia a comunicação.
- **Peer-to-Peer (P2P)**: não há necessidade de um servidor fixo; os pares se comunicam diretamente, compartilhando a carga.
- **Híbrida**: combina cliente-servidor e P2P, como em alguns serviços de mensagem instantânea.

### 3. **Requisitos de Aplicação**

- Algumas aplicações, como áudio e vídeo, toleram perdas de dados, enquanto outras, como transferência de arquivos, exigem confiabilidade completa.
- Aplicações como telefonia e jogos interativos requerem baixa latência para serem eficazes, enquanto multimídia exige uma banda mínima de dados.

### 4. **Serviços dos Protocolos de Transporte**

- **TCP**: oferece conexão confiável e controle de fluxo, adequado para aplicações que exigem transferência de dados sem perdas.
- **UDP**: é mais simples e rápido, sem garantias de conexão ou controle de congestionamento, utilizado para aplicações que podem tolerar perdas.

### 5. **Protocolos da Camada de Aplicação**

- **HTTP (Hypertext Transfer Protocol)**: usado para a Web, é sem estado, o que significa que o servidor não armazena informações sobre pedidos passados. Pode usar conexões persistentes (HTTP/1.1) para transferir múltiplos objetos em uma única conexão.
- **FTP (File Transfer Protocol)**: permite transferência de arquivos com uma conexão de controle separada e múltiplas conexões de dados.
- **SMTP, POP3, IMAP**: protocolos usados para envio e recuperação de e-mails, com SMTP focado em envio e POP3/IMAP em recebimento.
- **DNS (Domain Name System)**: traduz nomes de domínio em endereços IP, usando uma estrutura distribuída e hierárquica com servidores raiz, TLDs e servidores autoritativos.

### 6. **Cookies e Proxy**

- **Cookies**: usados para manter o estado do usuário no servidor, como informações de autenticação ou preferências.
- **Proxy (Web Cache)**: armazena cópias locais de objetos Web para reduzir o tempo de resposta e o tráfego, mas pode servir objetos desatualizados.

### 7. **P2P e Compartilhamento de Arquivos**

- **Napster e KaZaA**: exemplos de redes P2P onde os usuários compartilham arquivos diretamente. O Napster usava um servidor central para localização de arquivos, enquanto o KaZaA utilizava líderes de grupo para distribuição e gerenciamento da rede.

> [!Camada Aplicação] Próximo Assunto 
> [[Camada de Transporte]]