
# Atividade de desenvolvimento dos Requisitos

## Aluno: Luiz Eduardo Borges de Lima - 500623

#  1 - Requisitos Funcionais

**RF-01. Crud Auxilio/Bolsa**
- Criação/Edição/Exclusão de bolsas e auxílios

**RF-02. Listagem Auxilio/Bolsa**
- Exibição paginada dos registros de bolsas e auxílios

**RF-03. Busca Auxilio/Bolsa**
- Pesquisa por nome, tipo, unidade gestora e campus

**RF-04. Crud Frequencia**
- Criação/Edição/Exclusão de registros de frequência do bolsista

**RF-05. Listagem Frequencia**
- Exibição paginada de frequências por bolsista, mês e programa

**RF-06. Notificações Frequencia**
- Envio de alertas sobre pendências, atrasos e reprovação de frequência

**RF-07. Resultados Auxilios/Bolsas**
- Publicação de listas preliminares e finais (aprovados, suplentes, indeferidos)

**RF-08. Envio de Documentos**
- Upload de arquivos exigidos por edital com validação de formato e tamanho

**RF-09. Crud de Cronogramas**
- Criação/Edição/Exclusão de etapas e prazos dos editais

**RF-10. Listagem de Cronogramas**
- Exibição das etapas e datas por programa/edital com status atual

---
# 2 - Requisitos Funcionais (SRS) – Sistema de Bolsas e Auxílios da UFC 

> **Prompt:** Analise o texto abaixo e gere os requisitos funcionais e não funcionais seguindo o padrão do mercado de tecnologia e desenvolvimento de software.

## 1) Escopo Funcional por Módulo

### 2.1 Catálogo de Programas
**RF-01 – Listagem de Programas**  
Exibir todos os programas (Ajuda de Custos, Auxílio Moradia, PIBAD, Cultura e Arte, Extensão, Internacionais, Informática, Iniciação Acadêmica, Iniciação Científica, Desporto, PACCE, PID, Monitoria de Projetos, PET).

**RF-02 – Busca e Filtros**  
Permitir busca por texto e filtros por **tipo** (ex.: assistência, monitoria, pesquisa, extensão, internacional), **unidade gestora** (PRAE, PROGRAD, PREX, PRPPG, PROINTER, STI), **campus** (Fortaleza, Sobral, Cariri, Quixadá), **status** (com edital aberto/fechado).

**RF-03 – Detalhe do Programa**  
Exibir página do programa com: objetivos, público-alvo, critérios gerais, campus elegíveis, unidade gestora, **links oficiais** e **editais ativos**.

**RF-04 – Links Oficiais**  
Registrar e exibir URLs oficiais por programa (ex.: PRAE, PROGRAD, PREX, PRPPG, PROINTER, STI).

**RF-05 – Taxonomia e Tipos**  
Manter taxonomias (tipo de programa; natureza: mérito/assistência; modalidade: bolsa/auxílio/monitoria) para classificação e filtros.

**Critérios de Aceite (RF-01..05)**  
- Dado que existam ≥ 10 programas, quando o usuário pesquisar “Extensão”, **então** retornar apenas programas PREX/Extensão.  
- Em “Auxílio Moradia”, **deve** constar campus (Sobral, Cariri, Quixadá) e nota “não impede bolsas por mérito”.

---

### 2.2 Editais e Cronogramas
**RF-06 – CRUD de Edital**  
Gestor cria/edita/encerra edital: título, período de inscrição, vagas (se aplicável), requisitos, documentos exigidos, critérios de avaliação, **campus** e **curso(s)** elegíveis.

**RF-07 – Publicação e Versões**  
Suportar rascunho, publicação e histórico de versões (log de alterações).

**RF-08 – Cronograma**  
Configurar marcos: inscrições, análise, recursos, resultado preliminar/definitivo, início da bolsa.

**Critérios de Aceite (RF-06..08)**  
- Ao publicar edital com período válido, **então** o programa passa a exibir “Inscrições Abertas” com contagem regressiva.  
- Alterações em edital **devem** gerar nova versão e registrar quem alterou.

---

### 2.3 Inscrições (Candidaturas)
**RF-09 – Formulário Dinâmico por Edital**  
Gestor define campos obrigatórios/opcionais: dados pessoais/ acadêmicos, renda (quando aplicável), histórico, plano de atividades (quando aplicável), **uploads** (PDF, JPG/PNG) com limite de tamanho e tipo.

**RF-10 – Comprovação de Critérios**  
Regra de elegibilidade por edital (ex.: campus, curso, período, situação socioeconômica, CR mínimo, não acumulação de bolsas, impedimentos legais). Validações automáticas no envio.

**RF-11 – Rascunho e Envio**  
Discente pode salvar rascunho e enviar candidatura até o prazo. Após envio, edição só é possível enquanto o edital permitir “retificação”.

**RF-12 – Protocolo e Notificação**  
Gerar número de protocolo e notificar por e-mail/in-app (confirmação de envio; pendências; deferimento/indeferimento; resultados).

**Critérios de Aceite (RF-09..12)**  
- Envio sem todos os anexos obrigatórios **deve** bloquear submissão e listar pendências.  
- Ao enviar, **então** gerar protocolo e e-mail de confirmação.

---

### 2.4 Análise e Seleção
**RF-13 – Triagem (De/Indeferimento)**  
Gestor/Comissão visualiza candidaturas, verifica critérios obrigatórios, marca como **Deferida** ou **Indeferida** (com motivo padronizado e texto livre).

**RF-14 – Avaliação com Pontuação**  
Definir rubricas/ pesos por edital (ex.: vulnerabilidade, mérito acadêmico, aderência ao projeto, produção, experiência). Calcular pontuação e ranking.

**RF-15 – Empate e Critérios de Desempate**  
Configurar regras (ex.: maior CR, maior vulnerabilidade, veterano/ingressante, idade, sorteio auditável).

**RF-16 – Recursos Administrativos**  
Abrir janela de recursos; discente envia justificativa/anexos; comissão reavalia e registra decisão.

**RF-17 – Resultado Preliminar e Final**  
Publicar listas (aprovados, suplentes, indeferidos) com **carimbo de data** e **ata/relatório** de critérios utilizados.

**Critérios de Aceite (RF-13..17)**  
- Ao finalizar avaliação, o sistema **gera ranking** ordenado e destaca a linha de corte (vagas).  
- Registro de indeferimento **deve** conter motivo padronizado.

---

### 2.5 Acompanhamento da Bolsa/Auxílio
**RF-18 – Termo de Compromisso**  
Gerar termo para assinatura (digital ou upload), com regras específicas: carga horária (ex.: PACCE 12h/semana), proibições (ex.: PID remunerado não pode acumular outra remuneração), metas e entregas.

**RF-19 – Frequência/Atividades**  
Lançamento de frequência e atividades (monitorias, grupos de estudo, extensão, pesquisa, gestão esportiva). Anexos de comprovação (relatórios, certificados, produção científica – ex.: PET).

**RF-20 – Renovação/Prorrogação**  
Fluxo para renovar a bolsa conforme desempenho, frequência e adimplência de relatórios.

**RF-21 – Desligamento/Suspensão**  
Ações com motivo (descumprimento de carga, trancamento, formatura, reprovação em critérios).

**Critérios de Aceite (RF-18..21)**  
- Ao registrar frequência < limite, **então** o sistema sinaliza risco de desligamento e notifica discente e gestor.  
- PET: exigir comprovação anual de publicação/apresentação.

---

### 2.6 Integrações e Dados Institucionais
**RF-22 – Integração Acadêmica (Opcional)**  
Consultar dados do discente (matrícula, curso, campus, CR, situação) via integração institucional (ex.: SIGAA/ equivalentes) ou importação segura.

**RF-23 – Comprovação Socioeconômica (Quando Aplicável)**  
Registrar/validar renda per capita, documentos de vulnerabilidade e cruzar com regras do edital (Auxílio Moradia, Iniciação Acadêmica).

**RF-24 – Links Externos**  
Abrir links oficiais em nova aba com rastreio (cliques) para auditoria de acesso.

**Critérios de Aceite (RF-22..24)**  
- Se integração estiver indisponível, permitir **autodeclaração** com anexos e marcação de “a validar”.

---

### 2.7 Publicidade e Transparência
**RF-25 – Mural de Editais**  
Página pública com editais abertos/encerrados, filtros e exportação (CSV/PDF).

**RF-26 – Resultados e Relatórios**  
Publicar resultados (preliminar/final) e permitir download de relatórios consolidados (inscrições por campus/curso, índices de deferimento, perfil socioeconômico quando aplicável).

**RF-27 – Trilhas de Auditoria**  
Registrar ações críticas (publicação de edital, alterações, decisões de avaliação, resultados), com data/hora/usuário.

---

### 2.8 Administração e Segurança
**RF-28 – RBAC (Papéis e Permissões)**  
Papéis: Administrador, Gestor do Programa, Avaliador, Discente, Visitante. Permissões granulares por ação e por **escopo de unidade** (PRAE/PROGRAD/PREX/PRPPG/PROINTER/STI).

**RF-29 – Unidades e Campus**  
Cadastro de unidades gestoras e vínculo de programas/editais a campus específicos.

**RF-30 – Templates de Edital/Formulário**  
Modelos reutilizáveis por tipo de programa (ex.: Extensão, Monitoria, Pesquisa, Assistência, Internacional).

**RF-31 – Notificações**  
Configurar templates de e-mail/in-app para: confirmação de inscrição, pendências, decisões, abertura de recursos, publicação de resultados, renovação, frequência pendente.

---

## 3) Requisitos Não Funcionais (essenciais ao desenvolvimento)
- **RNF-01 – LGPD/Privacidade**: consentimento, finalidade, minimização de dados, perfis de acesso, logs, DPA para processadores.  
- **RNF-02 – Acessibilidade**: WCAG 2.1 AA (teclado, contraste, ARIA, foco).  
- **RNF-03 – Disponibilidade**: 99,5% mensal; janelas de manutenção comunicadas.  
- **RNF-04 – Desempenho**: busca/filtros < 2s (p95) com até 50k candidaturas/ano.  
- **RNF-05 – Segurança**: OAuth2/OIDC, MFA opcional, criptografia em trânsito (TLS 1.2+), repouso (AES-256), proteção contra upload malicioso (antivírus/clamav e validação MIME).  
- **RNF-06 – Auditabilidade**: logs imutáveis dos eventos críticos (RF-27).  
- **RNF-07 – Internacionalização**: PT-BR default; estrutura pronta p/ EN.

---

# 3. Requisitos Funcionais

### 3.1. Catálogo de Programas
- **RF001:** O sistema deve listar todos os programas de bolsas e auxílios disponíveis.  
- **RF002:** O sistema deve permitir busca e filtros por tipo, unidade gestora, campus e status.  
- **RF003:** O sistema deve exibir detalhes do programa com objetivos, público-alvo, links oficiais e editais ativos.  
- **RF004:** O sistema deve registrar e apresentar links oficiais de cada programa.  
- **RF005:** O sistema deve manter taxonomias de tipo, natureza e modalidade para classificação e filtros.  

### 3.2. Editais e Cronogramas
- **RF006:** O sistema deve permitir criação, edição e encerramento de editais.  
- **RF007:** O sistema deve permitir salvar rascunhos, publicar e manter histórico de versões.  
- **RF008:** O sistema deve gerenciar cronogramas de etapas dos editais.  

### 3.3. Inscrições
- **RF009:** O sistema deve disponibilizar formulário dinâmico configurável por edital.  
- **RF010:** O sistema deve validar critérios de elegibilidade automaticamente.  
- **RF011:** O sistema deve permitir salvar inscrições em rascunho e envio final.  
- **RF012:** O sistema deve gerar protocolo único e enviar notificações ao candidato.  

### 3.4. Análise e Seleção
- **RF013:** O sistema deve permitir triagem de candidaturas (deferida/indeferida) com justificativa.  
- **RF014:** O sistema deve suportar avaliação por rubricas e cálculo automático de ranking.  
- **RF015:** O sistema deve aplicar critérios configuráveis de desempate.  
- **RF016:** O sistema deve suportar fluxo de recursos administrativos com reapreciação.  
- **RF017:** O sistema deve publicar resultados preliminares e finais com registros de data e relatório.  

### 3.5. Acompanhamento da Bolsa/Auxílio
- **RF018:** O sistema deve gerar termo de compromisso para assinatura digital ou upload.  
- **RF019:** O sistema deve permitir lançamento e acompanhamento de frequência/atividades.  
- **RF020:** O sistema deve gerenciar fluxos de renovação e prorrogação de bolsas.  
- **RF021:** O sistema deve registrar desligamento ou suspensão com motivo.  

### 3.6. Integrações e Dados
- **RF022:** O sistema deve integrar ou importar dados acadêmicos institucionais.  
- **RF023:** O sistema deve registrar e validar comprovação socioeconômica quando aplicável.  
- **RF024:** O sistema deve abrir links externos em nova aba e registrar acessos.  

### 3.7. Transparência
- **RF025:** O sistema deve disponibilizar mural público de editais abertos e encerrados.  
- **RF026:** O sistema deve publicar relatórios consolidados sobre inscrições e resultados.  
- **RF027:** O sistema deve registrar trilhas de auditoria de ações críticas.  

### 3.8. Administração
- **RF028:** O sistema deve implementar RBAC com papéis e permissões por unidade.  
- **RF029:** O sistema deve permitir cadastro e vínculo de unidades gestoras e campus.  
- **RF030:** O sistema deve oferecer templates reutilizáveis de editais e formulários.  
- **RF031:** O sistema deve permitir configurar modelos de notificações automáticas.  

---

## 4. Requisitos Não Funcionais

- **RNF001 – Usabilidade:** O sistema deve ser intuitivo, responsivo e fácil de usar em diferentes dispositivos.  
- **RNF002 – Performance:** O sistema deve responder buscas e filtros em até 2 segundos para até 50 mil registros.  
- **RNF003 – Segurança:** O sistema deve implementar autenticação segura (OAuth2/OIDC), criptografia em trânsito e em repouso, além de validação de uploads.  
- **RNF004 – Compatibilidade:** O sistema deve funcionar nos principais navegadores modernos (Chrome, Firefox, Edge) e integrar-se com sistemas institucionais (SIGAA ou equivalentes).  
- **RNF005 – Manutenibilidade:** O sistema deve possuir código modular, documentado e com versionamento em repositório Git.  
- **RNF006 – Escalabilidade:** O sistema deve suportar aumento no número de usuários e dados sem degradação perceptível de desempenho.  
- **RNF007 – Acessibilidade:** O sistema deve estar em conformidade com WCAG 2.1 nível AA, garantindo acesso a usuários com deficiência.  

---

# 4 Comparação entre versões de requisitos

## Diferenças principais
- **Numeração**: uma versão usa `RF001…RF031`, a outra `RF-01…RF-31`.  
  ➝ Padronizar para `RF001…` por clareza.  
- **Detalhamento**: a versão SRS traz descrições longas e critérios de aceite; a versão RF001 é mais objetiva.  
- **Repetição**: regras de upload aparecem em RF e RNF; ideal deixar no RNF e citar no RF.  
- **Classificação**: itens como abrir links em nova aba (RF024) e auditoria imutável (RF027) devem migrar para RNFs (usabilidade/segurança).

---

## Ajustes sugeridos

### Catálogo (RF001–RF005)
- Incluir paginação/ordenação.  
- Indicar disponibilidade por campus.  

### Editais (RF006–RF008)
- Acrescentar rastro detalhado de versões e rollback.  
- Garantir que mudança de fase dispare notificações.  

### Inscrições (RF009–RF012)
- Prever janela de retificação.  
- Garantir idempotência no envio.  
- Validar anexos conforme RNF.  

### Seleção (RF013–RF017)
- Criar engine de rubricas configurável.  
- Registrar critérios de desempate aplicados.  

### Acompanhamento (RF018–RF021)
- Aprovação de frequência em dois passos.  
- Renovação em lote de bolsas.  

### Integrações (RF022–RF024)
- Ter fallback (CSV) quando integração falhar.  
- Marcação “a validar” quando dados não forem confirmados.  

### Transparência (RF025–RF027)
- Relatórios exportáveis com anonimização.  
- Reforçar logs nos RNFs.  

### Administração (RF028–RF031)
- Escopo por unidade/campus.  
- Templates versionados e biblioteca de perguntas.  
- Notificações multicanal e agenda de envios.

---

## Adições necessárias
- **RF032** – Validação anti-fraude (duplicidade/documentos).  
- **RF033** – API para relatórios/BI.  
- **RF034** – Termo de consentimento LGPD versionado.  
- **RF035** – Rate limiting/proteção contra abuso.  
- **RF036** – Observabilidade/telemetria.  

---

## RNFs
- Incluir cenários de pico de concorrência.  
- Definir RPO/RTO para backup e recuperação.  
- Reforçar segurança (assinatura de logs, CSP, HSTS).  
- Automatizar testes de acessibilidade.  

---

## Conclusão
O conteúdo das versões é equivalente, mas a versão final deve:
1. Padronizar a numeração (`RF001…`).  
2. Mover alguns pontos para RNFs.  
3. Adicionar controles de fraude, segurança e observabilidade.  
4. Detalhar melhor os processos de edital, inscrição e acompanhamento.  
