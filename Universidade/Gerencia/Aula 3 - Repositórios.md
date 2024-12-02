---
tags:
  - Universidade
materia: GC
tipo: Revisão
---
# Gerência de Configuração - Git e Repositórios

## **Conceitos Abordados**
1. **Repositórios Remotos**
   - Servem para armazenar o histórico de código em um local acessível, permitindo colaboração e compartilhamento de versões.
   - Podem estar:
     - Na máquina local (ex.: `C:/Users/usuário/servidor`).
     - Em servidores de rede interna (ex.: `http://192.168.0.181:8080`).
     - Na internet (ex.: `https://github.com/user/repository.git`).

2. **Servidor Git**
   - Criação de repositórios remotos pode ser feita usando:
     - `mkdir`: cria uma pasta.
     - `cd`: acessa uma pasta.
     - `git init --bare`: cria um repositório Git vazio, sem área de trabalho.

3. **Sincronização**
   - **Adicionar um repositório remoto**: 
     ```bash
     git remote add <nome> <url>
     ```
   - **Verificar repositórios remotos configurados**: 
     ```bash
     git remote -v
     ```

4. **Clonagem de Repositórios**
   - Para copiar um repositório existente: 
     ```bash
     git clone <url>
     ```

5. **Envio de Alterações (Push)**
   - Atualiza o repositório remoto com mudanças feitas localmente: 
     ```bash
     git push
     ```
   - O comando padrão é:
     ```bash
     git push origin <branch>
     ```
     Onde:
     - `origin`: nome do repositório remoto.
     - `<branch>`: ramo de desenvolvimento (ex.: `master`, `main`).

6. **Recebimento de Alterações (Pull)**
   - Atualiza o repositório local com mudanças feitas remotamente:
     ```bash
     git pull
     ```

7. **GitHub**
   - **O que é?**
     - Uma plataforma para hospedar repositórios Git, com funcionalidades adicionais para colaboração.
   - **Passos básicos:**
     - Criar um repositório no GitHub.
     - Adicionar o repositório como remoto:
       ```bash
       git remote add origin <url>
       ```
     - Fazer o primeiro envio:
       ```bash
       git push -u origin master
       ```

---

## **Fluxo de Trabalho no Git**
1. **Criação e Configuração de Repositório**
   - Inicializar um repositório local:
     ```bash
     git init
     ```
   - Configurar repositório remoto:
     ```bash
     git remote add <nome> <url>
     ```

2. **Manipulação de Arquivos**
   - Adicionar arquivos ao índice:
     ```bash
     git add <arquivo>
     ```
   - Salvar alterações no histórico:
     ```bash
     git commit -m "mensagem"
     ```

3. **Sincronização**
   - Enviar mudanças ao repositório remoto:
     ```bash
     git push
     ```
   - Buscar atualizações do repositório remoto:
     ```bash
     git pull
     ```

4. **Alterações e Colaboração**
   - Realizar alterações locais, fazer commits e enviá-las ao repositório remoto.
   - Sincronizar para obter alterações feitas por outros colaboradores.

---

## **Resumo**
- **Comandos Aprendidos:**
  - `git remote add`: adiciona um repositório remoto.
  - `git clone`: clona um repositório existente.
  - `git push`: envia mudanças para um repositório remoto.
  - `git pull`: atualiza o repositório local com mudanças do remoto.

- **Ferramentas e Plataformas:**
  - Git: controle de versão distribuído.
  - GitHub: plataforma para colaboração e hospedagem de repositórios.

---

> [!Camada Aplicação] Próximo Assunto 
> [[Lista de Exercı́cios 1|Lista de Exercı́cios 1]]