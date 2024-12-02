---
tags:
  - Universidade
materia: GC
tipo: Revisão
---
# Gerência de Configuração - Git: Resolvendo Conflitos

## **Conceitos Abordados**
1. **Rebase**
   - Permite reescrever o histórico de commits para criar um fluxo linear.
   - Comando básico:
     ```bash
     git rebase <nome_branch>
     ```

2. **Visualizando o Histórico**
   - Para visualizar o histórico em forma de grafo:
     ```bash
     git log --graph
     ```

3. **Criando e Resolvendo Conflitos**
   - **Passos para simular um conflito**:
     1. Criar uma branch e realizar alterações em um arquivo.
     2. Voltar para a branch principal (`master` ou `main`) e alterar o mesmo arquivo no mesmo ponto.
     3. Tentar fazer um merge entre as branches, o que resultará em um conflito.

   - **Resolvendo conflitos**:
     1. Editar os arquivos com conflitos.
     2. Marcar os arquivos como resolvidos:
        ```bash
        git add <arquivo>
        ```
     3. Finalizar o merge com:
        ```bash
        git commit
        ```

---

## **Dicas**
- Sempre realizar um `git pull` antes de fazer `git push` para evitar conflitos ao enviar alterações para o servidor.
- Use editores ou IDEs que facilitam a identificação e resolução de conflitos em arquivos.

---

## **Atividade Prática**
### **Simulação de Conflitos**
1. **Criar repositório e arquivos iniciais**:
   ```bash
   mkdir git-conflict-simulation
   cd git-conflict-simulation
   git init
   echo "<!DOCTYPE html><html><head><link rel='stylesheet' href='index.css'></head><body></body></html>" > index.html
   echo "body { background-color: white; }" > index.css
   git add .
   git commit -m "Initial commit with index.html and index.css"
   ```

2. **Criar branches e fazer alterações**:
   - Criar a branch `feature-a` e modificar `index.html`:
     ```bash
     git checkout -b feature-a
     echo "<h1>Feature A</h1>" >> index.html
     git add index.html
     git commit -m "Add header for Feature A in index.html"
     ```
   - Criar a branch `feature-b` e modificar `index.html` e `index.css`:
     ```bash
     git checkout -b feature-b main
     echo "<h1>Feature B</h1>" >> index.html
     echo "body { background-color: lightblue; }" > index.css
     git add index.html index.css
     git commit -m "Add header for Feature B in index.html and update index.css"
     ```

3. **Realizar merges e resolver conflitos**:
   - Voltar para a branch principal e fazer merge de `feature-a`:
     ```bash
     git checkout main
     git merge feature-a
     ```
   - Tentar fazer merge de `feature-b` (conflito ocorrerá):
     ```bash
     git merge feature-b
     ```
   - Resolver os conflitos editando os arquivos (`index.html` e `index.css`) e combinando as mudanças:
     ```html
     <h1>Feature A</h1>
     <h1>Feature B</h1>
     ```
   - Marcar os conflitos como resolvidos e finalizar:
     ```bash
     git add .
     git commit -m "Resolve merge conflicts between feature-a and feature-b"
     ```

4. **Visualizar o histórico após resolver os conflitos**:
   ```bash
   git log --graph --oneline
   ```

---

## **Resumo**
- Conflitos ocorrem quando diferentes branches alteram a mesma parte de um arquivo.
- Resolvem-se conflitos editando os arquivos, marcando como resolvidos (`git add`) e finalizando o merge (`git commit`).
- Ferramentas como `git log --graph` ajudam a entender o fluxo de alterações.

---
> [!Camada Aplicação] Próximos Assuntos 
> [[Aula 6 - Administrando alterações]]
> [[Aula 7 & 8 - Gerenciamento de release]]