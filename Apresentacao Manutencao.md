
# Slide 7 — Metodologia

**Tempo sugerido: 3min30s a 4min**

“Agora entrando na metodologia, o estudo foi organizado para responder uma pergunta central: se métodos dependentes de outros métodos são mais difíceis de comentar automaticamente, como podemos gerar comentários melhores para eles?”

“O primeiro passo dos autores foi montar uma base própria de dados. Eles não usaram apenas datasets tradicionais de sumarização de código, porque muitos desses datasets trazem somente pares de método e comentário, mas não trazem a informação sobre quais métodos auxiliares são chamados. Para este artigo, essa informação era essencial, porque o foco era justamente analisar dependências entre métodos.”

“Por isso, os autores coletaram dados de 10 projetos Java populares do GitHub. Esses projetos foram escolhidos por serem grandes, ativos e com bastante participação da comunidade. Depois disso, eles usaram o Tree-sitter para analisar os arquivos Java e extrair os métodos, os comentários e as chamadas entre métodos.”

“Na prática, eles identificavam quando um método chamava outro. Por exemplo, se o método A chama o método B, então o método A é considerado dependente, e o método B é considerado um helper method. Esse processo também podia formar cadeias maiores, como A chamando B, B chamando C, e assim por diante.”

“Com isso, os autores conseguiram classificar os métodos em dois grupos: métodos independentes, que não dependem de outros métodos, e métodos dependentes, que usam um ou mais métodos auxiliares.”

“Depois dessa extração, entra a proposta principal do artigo: o HelpCOM. A ideia do HelpCOM é simples, mas muito importante. Em vez de mandar para o modelo apenas o corpo do método principal, ele também envia os corpos dos helper methods dentro do prompt. Assim, o LLM recebe mais contexto para entender o que o método realmente faz.”

“Por fim, os comentários gerados foram avaliados por diferentes formas: métricas sintáticas, como BLEU, que olham para semelhança textual; métricas semânticas, como SentenceBERT, que tentam comparar o significado; avaliação baseada em LLM; e também uma avaliação com desenvolvedores. Ou seja, eles não confiaram apenas em uma métrica automática, mas combinaram diferentes formas de validação.”

“Então, resumindo a metodologia: eles coletaram projetos reais, extraíram métodos e dependências, geraram comentários com e sem contexto dos helper methods e compararam a qualidade desses comentários com modelos do estado da arte.”

O artigo informa que os autores extraíram métodos de 10 projetos Java, usaram Tree-sitter para mapear chamadas, criaram uma base com métodos dependentes e helper methods, e compararam o HelpCOM com baselines como CodeT5+, CodeBERT e ASAP.

---

# Slide 12 — Independência de Linguagem

**Tempo sugerido: 1min30s a 2min**

“Neste slide, os autores verificam se o HelpCOM funciona apenas para Java ou se a ideia pode ser aplicada em outras linguagens.”

“Isso é importante porque o experimento principal foi feito com projetos Java. Então poderia existir uma limitação: talvez a técnica funcionasse bem só nesse contexto. Para testar isso, eles aplicaram a mesma lógica em projetos de outras linguagens, especificamente Python e PHP.”

“O ponto central aqui é que a arquitetura do HelpCOM não depende diretamente da sintaxe do Java. O que ela precisa é conseguir identificar métodos ou funções e mapear quais chamadas existem entre eles. Se a linguagem permite esse mapeamento, a estratégia pode ser reaplicada.”

“Nos resultados, o HelpCOM teve um desempenho geral de 73,56 em Python e 66,05 em PHP na métrica geral OMS com avaliação sintática, semântica e por LLM. Esses valores ficaram até acima do resultado reportado para Java, que foi 56,82. Os autores explicam que isso pode ter relação com o tamanho menor da amostra em Python e PHP, mas ainda assim o teste reforça que a abordagem não é limitada a Java.”

“Então, a mensagem principal deste slide é: o HelpCOM não é apenas uma técnica para Java. Ele é uma estratégia baseada em dependência entre métodos, e essa ideia pode ser adaptada para outras linguagens.”

O artigo testou o HelpCOM em Python e PHP usando 50 métodos dependentes de cada linguagem e obteve OMSssl de 73,56 para Python e 66,05 para PHP, reforçando a independência de linguagem da abordagem.

---

# Slide 13 — Conclusão

**Tempo sugerido: 2min a 2min30s**

“Na conclusão do artigo, os autores reforçam quatro achados principais.”

“O primeiro é que métodos dependentes são muito comuns em projetos reais. Eles não são casos isolados. Pelo contrário, aparecem como a maioria dos métodos analisados. Isso mostra que qualquer ferramenta de geração automática de comentários precisa lidar bem com esse tipo de método.”

“O segundo ponto é que métodos dependentes também são mais propensos a mudanças. Como eles concentram mais commits e envolvem mais autores, eles acabam sendo partes mais sensíveis do sistema. Se a documentação desses métodos for ruim, isso pode dificultar manutenção, revisão de código e entrada de novos desenvolvedores no projeto.”

“O terceiro ponto é que as técnicas atuais de geração de comentários ainda têm dificuldade em capturar contexto semântico profundo. Modelos como CodeT5+, CodeBERT e ASAP conseguem gerar comentários, mas muitas vezes esses comentários ficam superficiais, porque descrevem apenas o nome do método ou uma parte visível do código.”

“O quarto ponto é a contribuição do HelpCOM: ao incluir os helper methods no prompt, o modelo passa a enxergar informações que antes ficavam escondidas. Com isso, os comentários se tornam mais completos e mais próximos do comportamento real do método.”

“Além das métricas automáticas, o artigo também validou isso com desenvolvedores. Cerca de 75% dos participantes preferiram os comentários gerados pelo HelpCOM. Isso é importante porque mostra que o ganho não foi apenas numérico, mas também percebido por pessoas reais que trabalham com código.”

“Então, a conclusão geral é que, para gerar comentários úteis, não basta olhar para o método isolado. É necessário olhar para o contexto de execução, principalmente para os métodos auxiliares que influenciam o comportamento do método principal.”

O artigo conclui que métodos dependentes representam uma parte expressiva do código, que os baselines têm dificuldade em comentá-los e que o HelpCOM melhora a qualidade dos comentários ao incorporar informações dos helper methods; o survey teve 156 respostas completas e aproximadamente 75% dos participantes escolheram comentários do HelpCOM.

---

# Slide 14 — Trabalho, Autor e Ordem Cronológica

**Tempo sugerido: 1min30s a 2min**

“Neste momento da apresentação, a gente entra na parte de inovação, trazendo uma tese relacionada ao artigo.”

“O trabalho relacionado é a tese de mestrado intitulada _Large Language Models for Code Generation and Program Comprehension: Exploring Capabilities, Context, and Developer Adaptation_.”

“O autor é Md Mustakim Billah, o mesmo autor principal do artigo do HelpCOM. A tese foi submetida à University of Saskatchewan, no Canadá, como requisito para o grau de Master of Science, em novembro de 2025.”

“A relação entre os dois trabalhos é direta. O artigo científico sobre o HelpCOM foi publicado antes, em junho de 2025, na conferência EASE. Já a tese de mestrado veio depois, em novembro de 2025, reunindo e ampliando essa linha de pesquisa.”

“Então, a ordem cronológica é: primeiro vem o artigo do HelpCOM, que foca especificamente em geração de comentários considerando dependências entre métodos; depois vem a tese, que coloca esse estudo dentro de uma pesquisa maior sobre LLMs, geração de código, compreensão de programas e adaptação ao perfil do desenvolvedor.”

“Por isso, usamos a tese como inovação: ela não é apenas um trabalho parecido, ela expande o artigo e mostra uma evolução da ideia.”

A tese é de Md Mustakim Billah, submetida à University of Saskatchewan para o grau de Master of Science em novembro de 2025; nela, o artigo do HelpCOM aparece como publicação relacionada ao trabalho.

---

# Slide 15 — Resumo e Objetivo

**Tempo sugerido: 2min a 2min30s**

“A tese investiga como os LLMs podem apoiar duas atividades importantes da Engenharia de Software: geração de código e compreensão de programas.”

“Ela é estruturada em três estudos. O primeiro avalia a capacidade de modelos como ChatGPT, Gemini e Meta AI em resolver problemas de programação em plataformas como LeetCode, Codeforces e HackerRank. Esse estudo serve para entender até que ponto esses modelos conseguem raciocinar sobre lógica, controle de fluxo e intenção de problemas.”

“O segundo estudo é justamente o HelpCOM, que vimos no artigo. Ele trata da geração de comentários considerando o contexto dos helper methods. Aqui, a ideia é que o LLM não deve olhar apenas para o método principal, mas também para as dependências que ajudam a explicar o comportamento real do código.”

“O terceiro estudo é a parte mais inovadora da tese: a sumarização adaptada ao perfil do desenvolvedor. A tese argumenta que desenvolvedores iniciantes e experientes não precisam necessariamente do mesmo tipo de comentário. Iniciantes tendem a precisar de explicações mais detalhadas, passo a passo, enquanto desenvolvedores experientes preferem resumos mais curtos, focados na intenção e na lógica de alto nível.”

“Então, o objetivo geral da tese é analisar como os LLMs podem melhorar a documentação e a compreensão de código, considerando dois fatores principais: o contexto técnico do código e o perfil de quem está lendo.”

“Essa é a evolução em relação ao artigo: o artigo mostra que o contexto dos métodos auxiliares melhora os comentários; a tese amplia essa ideia e mostra que também é importante adaptar a explicação ao nível de experiência do desenvolvedor.”

O resumo da tese apresenta três estudos conectados: avaliação de LLMs em programação, HelpCOM para comentários com dependências e sumarização adaptada ao nível do desenvolvedor; a tese também destaca que iniciantes preferem explicações mais detalhadas, enquanto especialistas preferem resumos mais concisos e focados em intenção.

---

# Slide 16 — Metodologia e Conclusão da Tese

**Tempo sugerido: 2min30s a 3min**

“Neste último slide, a gente resume como a tese foi conduzida e qual foi a principal conclusão dela.”

“A metodologia da tese é baseada em três estudos empíricos. No primeiro estudo, o autor avaliou LLMs em plataformas de programação. Foram usados problemas de diferentes categorias, níveis de dificuldade e plataformas, para observar em quais cenários os modelos funcionavam melhor e em quais tinham mais dificuldade.”

“No segundo estudo, que é o artigo do HelpCOM, a metodologia envolveu projetos reais do GitHub, extração de métodos, identificação de helper methods e geração de comentários com contexto. Esse estudo mostrou que incluir dependências no prompt melhora a qualidade dos comentários.”

“No terceiro estudo, a tese propõe a sumarização adaptativa. Nessa parte, o autor parte da ideia de que a mesma explicação não serve igualmente para todos os desenvolvedores. Então, foram criados prompts diferentes para gerar resumos voltados para iniciantes e para especialistas.”

“Essa abordagem também foi integrada ao GitHub Copilot Chat no VS Code. Ou seja, a tese não ficou apenas numa avaliação teórica ou isolada; ela tentou aproximar a técnica de um ambiente real de desenvolvimento.”

“A conclusão principal da tese é que LLMs podem ser úteis para apoiar a compreensão de código, mas sua utilidade aumenta quando eles recebem o contexto certo e quando a resposta é adaptada ao leitor.”

“Para desenvolvedores iniciantes, comentários mais explicativos ajudam a entender o que o código faz e como ele funciona. Para desenvolvedores experientes, comentários mais objetivos ajudam a entender rapidamente a intenção do método e sua função no sistema.”

“Assim, a tese amplia o HelpCOM em duas direções: primeiro, reforçando a importância do contexto dos helper methods; segundo, mostrando que a documentação gerada por IA pode ser personalizada de acordo com a experiência do desenvolvedor.”

“Fechando a apresentação, a principal mensagem é: a geração automática de comentários não deve ser genérica. Ela precisa ser contextual, porque o código depende de outros métodos, e adaptativa, porque diferentes desenvolvedores têm necessidades diferentes de compreensão.”

A tese relata a integração da sumarização adaptativa ao GitHub Copilot Chat no VS Code, com comandos para gerar resumos de métodos específicos ou de todos os métodos de um arquivo; também conclui que a adaptação ao perfil do desenvolvedor melhora compreensão, onboarding e revisão de código.
