---
tags:
  - Universidade
materia: GC
tipo: Revisão
---
# Gerência de Configuração - Git: Branches e Merge

## **Conceitos Abordados**
1. **Branches**
   - São ramificações do projeto que representam versões diferentes do código.
   - Permitem trabalhar em partes distintas do código ou em momentos diferentes de maturidade.
   - Cada repositório Git pode conter múltiplos branches:
     - **master**: o branch principal criado por padrão em repositórios antigos.
     - **main**: substitui o termo "master" como padrão em repositórios criados a partir de 1º de outubro de 2020.
     - **origin**: apelido para o repositório remoto padrão ao clonar (`git clone`).
     - **HEAD**: não é um branch, mas um ponteiro para o branch atualmente ativo.

2. **Por que usar Branches?**
   - Facilita o desenvolvimento paralelo de funcionalidades.
   - Permite isolar trabalhos em progresso, evitando impacto no código principal.

3. **Comandos Relacionados a Branches**
   - Criar um branch:
     ```bash
     git branch <nome_branch>
     ```
   - Alternar para outro branch:
     ```bash
     git checkout <nome_branch>
     ```
   - Criar e alternar simultaneamente:
     ```bash
     git checkout -b <nome_branch>
     ```

---

## **Merge**
- Une as mudanças de um branch ao branch ativo.
- Comando básico:
  ```bash
  git merge <nome_branch>
  ```
- Resultado do merge:
  - Integra as mudanças feitas no branch especificado ao branch atual.

---

## **Rebase**
- Integra mudanças de um branch de maneira linear, reorganizando os commits.
- Pode ser usado como alternativa ao merge para manter um histórico de commits mais limpo.
- Referência para aprender mais: [Git Rebase no Git SCM](https://git-scm.com/book/pt-br/v2/Branches-no-Git-Rebase).

---

## **Dicas**
1. Quando o merge abre a interface de edição no terminal:
   - Para sair, pressione `q`.

2. Evitar commits de merge:
   - Utilize `git rebase` ao invés de `git merge` para incorporar mudanças sem criar um commit adicional.

---
## **Resumo**
- Branches ajudam a organizar o trabalho em partes separadas do código.
- `git merge` combina alterações de branches, enquanto `git rebase` mantém o histórico linear.
- Comandos úteis:
  - `git branch`, `git checkout`, `git merge`, `git rebase`.

---

> [!Camada Aplicação] Próximos Assuntos 
> [[Aula 5 - Resolvendo conﬂitos]]
> [[Aula 6 - Administrando alterações]]
> [[Aula 7 & 8 - Gerenciamento de release]]