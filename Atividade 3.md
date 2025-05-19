### **1. Como informações são passadas de um objeto a outro em um sistema OO? Explique esse processo.**

Em um sistema orientado a objetos (OO), as informações são passadas entre objetos por meio de **mensagens**, que nada mais são do que **chamadas de métodos**. Quando um objeto precisa que outro realize uma ação ou forneça dados, ele envia uma mensagem para esse objeto, geralmente na forma `objeto.metodo(parametros)`. O objeto receptor, ao receber essa mensagem, executa o método correspondente, utilizando os dados recebidos e possivelmente retornando um resultado.

---

### **2. Quando utilizar diagramas de interações (sequência ou comunicação)? Há alternativas para esse momento?**

Utilizamos **diagramas de interação** para **modelar o comportamento dinâmico** do sistema, especialmente:

- **Diagrama de sequência**: quando queremos representar a **ordem temporal das mensagens** entre objetos.
- **Diagrama de comunicação**: quando o foco está na **estrutura de colaboração entre os objetos**, e não na ordem das mensagens.

**Alternativas**:

- **Máquinas de estados**: úteis para modelar o comportamento interno de um único objeto.
- **Atividades (diagrama de atividade)**: úteis para modelar fluxos de trabalho e decisões.
- **Casos de uso**: fornecem visão mais ampla das interações do usuário com o sistema.

---

### **3. Qual é a consequência da construção do Modelo de Interação sobre os demais artefatos do sistema?**

A construção do **Modelo de Interação** afeta diretamente os seguintes artefatos:

- **Modelo de classes**: os métodos e atributos necessários aparecem a partir das mensagens trocadas.
- **Código fonte**: os métodos modelados devem ser implementados conforme descrito nas interações.
- **Testes**: os fluxos definidos nos diagramas orientam os **casos de teste**.

Além disso, ajuda a validar e refinar requisitos e identificar responsabilidades dos objetos.

### **4. Há possibilidade de geração de código a partir de um diagrama de interações?**

Sim, algumas ferramentas de modelagem (como Enterprise Architect, Visual Paradigm, StarUML) permitem a **geração automática de esqueletos de código** (stubs) a partir de diagramas de interação. Contudo, essa geração costuma ser limitada ao **esqueleto da classe** e às **assinaturas de métodos**, exigindo implementação manual do comportamento interno.