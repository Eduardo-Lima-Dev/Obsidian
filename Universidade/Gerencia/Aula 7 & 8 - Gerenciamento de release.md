---
tags:
  - Universidade
materia: GC
tipo: Revisão
---
# Gerência de Configuração - Git: Gerenciamento de Releases

## **Conceitos Abordados**
1. **Atividades da Gerência de Configuração**
   - **Controle de versão**: Acompanhamento de versões e garantia de que mudanças não interfiram entre si.
   - **Construção do sistema**: Montagem e compilação de componentes para criar um executável.
   - **Gerenciamento de mudanças**: Avaliação de custo e impacto de mudanças solicitadas.
   - **Gerenciamento de release**: Preparação do software para liberação externa.

2. **Fases de um Sistema de Software**
   - **Desenvolvimento**:
     - Novas funcionalidades são adicionadas.
     - A equipe decide as mudanças necessárias.
   - **Teste do sistema**:
     - Sistema liberado internamente para testes.
     - Foco em correções de erros, melhorias e segurança.
   - **Lançamento**:
     - Sistema liberado aos clientes.
     - Bugs e solicitações são reportados pelos usuários.

3. **Releases**
   - Identificação de código e arquivos no sistema de controle de versão.
   - Configurações específicas para diferentes sistemas operacionais.
   - Preparação de scripts de instalação e documentação.

---

## **Versionamento**
1. **Semântica de Versionamento (SemVer)**
   - **Formato**: `MAJOR.MINOR.PATCH`.
     - **MAJOR**: Mudanças incompatíveis na API.
     - **MINOR**: Funcionalidades adicionadas, mantendo compatibilidade.
     - **PATCH**: Correções de erros.
   - **Regras**:
     - Não alterar pacotes já lançados.
     - Versão inicial: `0.1.0` ou `1.0.0` em produção.

2. **Versionamento Microsoft**
   - **Formato**: `MAJOR.MINOR.BUILD.REVISION`.
     - **MAJOR**: Reescritas significativas.
     - **MINOR**: Melhorias compatíveis.
     - **BUILD**: Diferenças de compilação.
     - **REVISION**: Atualizações intercambiáveis, como hotfixes.

---

## **Ciclo de Vida do Software**
1. **Pre-alpha**: Atividades antes dos testes formais (design, desenvolvimento, testes unitários).
2. **Alpha**:
   - Primeira fase de testes.
   - Contém instabilidades e erros graves.
   - Normalmente não é liberada externamente.
3. **Beta**:
   - Sistema completo, mas com bugs.
   - Testes focados em usabilidade.
   - Pode ser pública ou privada.
4. **Release to Manufacturing (RTM)**:
   - Produto pronto para entrega.
5. **Disponibilidade Geral (GA)**:
   - Produto disponível para compra.

---

## **Tags e Releases no Git**
1. **Tags**:
   - Marcam pontos fixos na aplicação, como lançamentos de versão.
   - Comando básico:
     ```bash
     git tag <tag_name>
     ```
   - Envio para repositórios remotos:
     ```bash
     git push origin <tag_name>
     ```
2. **Releases no GitHub**:
   - Associam tags a descrições detalhadas para usuários.

---

## **Softwares de Visualização**
1. **SourceTree**: Ferramenta visual para gerenciamento Git.
2. **GitLens**: Extensão para o VSCode que facilita a visualização de mudanças e histórico.

---

## **Dica**
- Crie tags e releases durante o desenvolvimento para cada entrega, facilitando o controle de versões.

---

> [!Camada Aplicação] Próximo Assunto 
> [[Aula 9]]