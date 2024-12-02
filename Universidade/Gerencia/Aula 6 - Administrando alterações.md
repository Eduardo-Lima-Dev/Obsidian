---
tags:
  - Universidade
materia: GC
tipo: Revisão
---
# Gerência de Configuração - Git: Administrando Alterações

## **Conceitos Abordados**
1. **Comandos para Desfazer Alterações**
   - **`git restore`**:
     - Usado para descartar alterações no diretório de trabalho antes de adicioná-las ao staging.
     ```bash
     git restore <arquivo>
     ```
   - **`git restore --staged`**:
     - Remove um arquivo do staging, mantendo as alterações no diretório de trabalho.
     ```bash
     git restore --staged <arquivo>
     ```
   - **`git reset`**:
     - Desfaz commits já realizados.
       - **`--soft`**: Remove o último commit, mas mantém as alterações no staging.
       - **`--mixed`**: Remove o commit e retira os arquivos do staging, mas mantém as alterações no diretório.
       - **`--hard`**: Remove o commit e descarta todas as alterações do diretório de trabalho.
     ```bash
     git reset --soft HEAD~1
     git reset --mixed HEAD~1
     git reset --hard HEAD~1
     ```
   - **`git revert`**:
     - Desfaz um commit específico, criando um novo commit e preservando o histórico.
     ```bash
     git revert <commit-hash>
     ```

2. **Guardando Alterações Temporariamente**
   - **`git stash`**:
     - Armazena alterações não commitadas temporariamente.
     - Comandos úteis:
       ```bash
       git stash
       git stash list
       git stash pop
       git stash apply <stash-id>
       git stash drop
       ```
     - Usos principais:
       - Trocar de branch rapidamente.
       - Preservar mudanças ao trabalhar em algo urgente.

3. **Visualizando Alterações**
   - **`git diff`**:
     - Compara as mudanças feitas.
       ```bash
       git diff
       git diff <commit1>..<commit2>
       ```
   - **`git log -p`**:
     - Mostra o histórico de commits com as mudanças detalhadas.

---

## **Resumo**
- **Desfazendo alterações**:
  - Antes de adicionar ao staging: `git restore`.
  - Após adicionar ao staging: `git restore --staged`.
  - Após commitar: `git reset` ou `git revert`.

- **Guardando progresso temporariamente**:
  - Use `git stash` para preservar alterações não finalizadas.

- **Visualizando alterações**:
  - Use `git diff` ou `git log -p` para entender mudanças.

---
> [!Camada Aplicação] Próximos Assuntos
> [[Aula 7 & 8 - Gerenciamento de release]]