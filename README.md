# 🚀 Material de Consulta para Capacitação em Git e GitHub

Este documento serve como um material de consulta rápida para os trainees do PS 2025.1, cobrindo os principais conceitos e comandos do Git e GitHub apresentados na capacitação do dia 03/06/2025.

## 📚 Parte 1: Fundamentos do Git e Fluxo de Trabalho Básico

### 1. Introdução ao Git e Controle de Versão

* **O que é Git?**

    * Um sistema de controle de versão **distribuído** (DVCS).

    * Permite que várias pessoas trabalhem no mesmo projeto simultaneamente sem sobrescrever o trabalho um do outro.

    * Mantém um histórico completo de todas as alterações feitas nos arquivos do projeto.

* **Por que usar controle de versão?**

    * **Rastreamento de mudanças:** Saiba quem, o quê, quando e por que cada alteração foi feita.

    * **Colaboração:** Facilita o trabalho em equipe, permitindo a fusão de contribuições de diferentes desenvolvedores.

    * **Histórico:** Capacidade de reverter para qualquer versão anterior do projeto.

    * **Branching:** Permite desenvolver novas funcionalidades ou corrigir bugs em ambientes isolados.

### 2. 💻 Instalação e Configuração do Git

#### Pré-requisitos

* Acesso à internet.

* Permissões de administrador (Windows) ou `sudo` (Ubuntu).

#### Instalação no Ubuntu

1.  **Verificar versão existente:**

    ```
    git --version
    ```

2.  **Adicionar PPA do Git (para versão mais recente):**

    ```
    sudo add-apt-repository ppa:git-core/ppa
    sudo apt update
    ```

3.  **Instalar Git:**

    ```
    sudo apt install git -y
    ```

#### Instalação no Windows

1.  **Baixar o instalador:** Acesse `git-scm.com/downloads/win` e baixe a versão mais recente.

2.  **Executar o instalador:**

    * Siga as instruções.

    * **Importante:** Marque as opções "Git Bash Here" e "Git GUI Here".

    * Selecione "Git from the command line and also from 3rd-party software" para adicionar o Git ao PATH do sistema.

    * Escolha seu editor de texto padrão (ex: VS Code, Notepad++).

#### Verificação da Instalação (Ubuntu e Windows)

* Abra o terminal (Git Bash no Windows ou terminal padrão no Ubuntu) e digite:

    ```
    git --version
    ```

    Você deve ver o número da versão do Git instalada.

#### Configuração Inicial (Ubuntu e Windows)

* **Configurar seu nome de usuário:**

    ```
    git config --global user.name "Seu Nome Completo"
    ```

* **Configurar seu e-mail:**

    ```
    git config --global user.email "seu.email@exemplo.com"
    ```

* **Verificar suas configurações:**

    ```
    git config --list
    ```

### 3. ⚙️ Comandos Git Essenciais para um Fluxo de Trabalho Básico

O Git opera em três áreas principais:

* **Diretório de Trabalho:** Onde você edita seus arquivos.

* **Área de Staging (Index):** Uma área intermediária onde você prepara as alterações para o próximo commit.

* **Repositório Local (.git):** Onde o Git armazena o histórico do projeto.

#### Comandos:

* **`git init`**

    * **Finalidade:** Inicializa um novo repositório Git em um diretório existente.

    * **Sintaxe:** `git init`

    * **Exemplo:**

        ```bash
        mkdir meu-projeto
        cd meu-projeto
        git init
        ```

    * **Diferença `git init` vs. `git clone`:** `init` cria um novo repositório local do zero; `clone` copia um repositório existente (geralmente de um serviço como GitHub).

* **`git status`**

    * **Finalidade:** Mostra o estado do diretório de trabalho e da área de staging (quais arquivos foram modificados, quais estão prontos para serem commitados).

    * **Sintaxe:** `git status`

    * **Exemplo:**

        ```bash
        touch novo_arquivo.txt
        git status
        ```

        (Mostrará `novo_arquivo.txt` como "untracked")

* **`git add`**

    * **Finalidade:** Adiciona alterações do diretório de trabalho para a área de staging.

    * **Sintaxe:**

        * `git add <nome_do_arquivo>`: Adiciona um arquivo específico.

        * `git add .`: Adiciona todas as alterações no diretório atual.

        * `git add -A`: Adiciona todas as alterações (incluindo exclusões) no repositório.

    * **Exemplo:**

        ```bash
        git add novo_arquivo.txt
        git status
        ```

        (Mostrará `novo_arquivo.txt` como "changes to be committed")

* **`git commit`**

    * **Finalidade:** Salva as alterações que estão na área de staging no histórico do repositório local.

    * **Sintaxe:** `git commit -m "Mensagem descritiva do commit"`

    * **Exemplo:**

        ```bash
        git commit -m "Adiciona o primeiro arquivo de exemplo"
        git status
        ```

        (O diretório de trabalho estará limpo)

    * **Hash do Commit:** Cada commit é identificado por um hash SHA-1 único.

    * **`git log`:**

        * **Finalidade:** Exibe o histórico de commits.

        * **Sintaxe:**

            * `git log`: Histórico completo.

            * `git log --oneline`: Histórico conciso (hash curto e mensagem).

            * `git log --graph --decorate`: Visualiza branches e merges.

* **`git pull`**

    * **Finalidade:** Baixa as alterações de um repositório remoto e as integra (mescla) na sua branch local atual.

    * **Sintaxe:** `git pull origin main` (onde `origin` é o nome do seu remoto e `main` é a branch).

    * **Diferença `git pull` vs. `git fetch`:** `fetch` apenas baixa as alterações para o seu repositório local, mas não as mescla; `pull` faz o `fetch` e o `merge`.

* **`git push`**

    * **Finalidade:** Envia seus commits locais para um repositório remoto.

    * **Sintaxe:** `git push origin main`

    * **Primeiro push de uma branch:** `git push -u origin <nome-da-branch>` (o `-u` define o upstream para pushes futuros).

    * **Erros "non-fast-forward":** Ocorre se o repositório remoto tem commits que você não tem localmente. Resolva com `git pull` antes de `git push`.

## 📈 Parte 2: Cenários Avançados e Colaboração com GitHub

### 4. 🛠️ Comandos Git para Cenários Mais Avançados

* **`git reset --soft <commit-hash>` ou `git reset --soft HEAD~<n>`**

    * **Finalidade:** Desfaz um ou mais commits, mas mantém as alterações desses commits no seu diretório de trabalho e na área de staging. Útil para reescrever o último commit.

    * **Exemplo:** `git reset --soft HEAD~1` (desfaz o último commit).

    * **Implicações:** Reescreve o histórico. Cuidado ao usar em branches já publicadas, pois pode exigir `git push --force`.

    * **Variações:**

        * `--mixed` (padrão): Desfaz o commit e tira as alterações do staging, mas mantém no diretório de trabalho.

        * `--hard`: Desfaz o commit e **apaga** as alterações do diretório de trabalho e staging. **Use com extrema cautela!**

* **Criação de Novas Branches**

    * **Finalidade:** Criar ramificações independentes para desenvolver funcionalidades ou corrigir bugs sem afetar a branch principal.

    * **Sintaxe:**

        * `git branch <nome-da-branch>`: Cria a branch, mas não muda para ela.

        * `git checkout <nome-da-branch>`: Muda para uma branch existente.

        * `git checkout -b <nome-da-branch>`: **Cria e muda** para a nova branch (mais comum).

        * `git switch -C <nome-da-branch>`: Alternativa moderna ao `checkout -b`.

    * **Melhores Práticas:** Use nomes descritivos (ex: `feature/login-google`, `bugfix/erro-calculo`).

* **Alternar entre Branches (com alterações não commitadas)**

    * **Cenário:** Você fez alterações, mas precisa mudar para outra branch sem commitar.

    * **Opção 1: Criar uma nova branch e levar as alterações para ela:**

        ```bash
        git checkout -b nova-branch-com-mudancas
        ```

    * **Opção 2: Usar `git stash` (para salvar temporariamente):**

        * **Finalidade:** Salva suas alterações não commitadas e não staged, limpando o diretório de trabalho.

        * **Sintaxe:**

            * `git stash`: Guarda as alterações.

            * `git stash list`: Lista os stashes guardados.

            * `git stash apply`: Aplica o último stash de volta (mantém o stash na lista).

            * `git stash pop`: Aplica o último stash e o remove da lista.

            * `git stash drop`: Remove um stash específico da lista.

* **Resolução de Conflitos Básicos**

    * **Quando ocorrem:** Ao tentar mesclar branches onde as mesmas linhas de um arquivo foram modificadas de formas diferentes.

    * **Como identificar:** O Git informará sobre o conflito e o `git status` mostrará os arquivos em conflito.

    * **Passos para resolver:**

        1.  Abra o arquivo em conflito. Você verá marcadores como `<<<<<<< HEAD`, `=======` e `>>>>>>>`.

        2.  Edite o arquivo manualmente, decidindo qual versão manter ou combinando as partes.

        3.  Remova todos os marcadores de conflito.

        4.  Salve o arquivo.

        5.  Adicione o arquivo resolvido à área de staging: `git add <arquivo-resolvido>`.

        6.  Finalize o merge com um commit: `git commit`.

    * **Cancelar um merge:** `git merge --abort`

### 5. 🤝 Integração e Uso de Branches no GitHub

* **Visão Geral de Branches no GitHub:**

    * **Branch `main` (ou `master`):** A branch principal do projeto, geralmente contém o código estável e pronto para produção.

    * **Branches de funcionalidade (Feature Branches):** Criadas para desenvolver novas funcionalidades, correções de bugs ou experimentos, isolando o trabalho da `main`.

* **Criar e Gerenciar Branches Remotas:**

    * **No GitHub (UI):** Você pode criar branches diretamente na interface web do GitHub.

    * **Via CLI (após criar localmente):**

        ```bash
        git checkout -b minha-nova-branch # Cria localmente
        git push -u origin minha-nova-branch # Envia para o GitHub e define upstream
        ```

    * **Listar branches remotas:** `git branch -r` ou `git branch -a` (todas).

    * **Excluir branch remota:** `git push origin --delete <nome-da-branch-remota>`

* **Fluxo de Trabalho de Pull Requests (PRs)**

    * **O que é um PR?** Uma solicitação para mesclar suas alterações de uma branch para outra (geralmente da sua feature branch para a `main`). É o coração da colaboração no GitHub.

    * **Ciclo de um PR:**

        1.  **Criar Branch:** Desenvolva sua funcionalidade em uma branch separada.

        2.  **Push para Remoto:** Envie sua branch para o GitHub (`git push origin <sua-branch>`).

        3.  **Abrir Pull Request:** No GitHub, clique em "Compare & pull request". Dê um título e descrição claros.

        4.  **Revisar e Discutir:** Membros da equipe revisam seu código, fazem comentários e sugerem melhorias. Testes automatizados podem ser executados.

        5.  **Mesclar (Merge):** Após a aprovação, o PR é mesclado na branch de destino (ex: `main`), integrando suas alterações. A feature branch pode ser excluída após o merge.

* **Melhores Práticas para PRs:**

    * **Pequenos e Focados:** PRs menores são mais fáceis e rápidos de revisar.

    * **Contexto Claro:** Títulos e descrições devem explicar o que o PR faz e por que.

    * **Revisar seu próprio PR:** Antes de submeter, faça uma auto-revisão.

## 📝 Exercícios Práticos para Trainees

1.  **Criar uma conta no GitHub:** Se ainda não tiver, crie uma conta em `github.com`.

2.  **Criar um repositório local, fazer algumas alterações e subir para o remoto:**

    * Crie um diretório vazio.

    ```
    git init
    ```

    * Crie um arquivo (ex: `index.html`) e adicione conteúdo.

    ```
    git add .
    ```
    ```
    git commit -m "Primeiro commit do meu projeto"
    ```

    * Crie um repositório vazio no GitHub (pode ser público).

    * Conecte seu repositório local ao remoto: `git remote add origin <URL_do_repositorio_github>`

    * Envie seu código: `git push -u origin main`

3.  **Enviar o usuário do GitHub para os respectivos gerentes:** Isso permitirá que eles o adicionem à organização da EletronJun.

**Recomendação:** Pratique diariamente! Crie uma nova branch para cada tarefa ou funcionalidade, faça as alterações, commite, envie para o GitHub e abra um Pull Request. A prática leva à perfeição no Git.
