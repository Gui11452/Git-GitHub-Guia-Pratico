
# Git e Github - Guia Prático

## Sumário
1. [O que e Git](#1---o-que-e-git)
2. [O que e Github](#2---o-que-e-github)
3. [Instalacão do Git no Windows](#3---instalacão-do-git-no-windows)
4. [Salvando a primeira versão de um projeto no GitHub](#4---salvando-a-primeira-versão-de-um-projeto-no-gitHub)
5. [Salvando um Novo Commit](#5---salvando-um-novo-commit)
6. [Arquivo gitignore](#6---arquivo-gitignore)
7. [Branch no Git](#7---branch-no-git)
8. [Branches Locais e Remotas](#8---branches-locais-e-remotas)
9. [Estados dos Arquivos no Git](#9---estados-dos-arquivos-no-git)
10. [Desfazer e Excluir Commits](#10---desfazer-e-excluir-commits)
11. [Como Resolver Conflitos no Git](#11---como-resolver-conflitos-no-git)
12. [git pull](#12---git-pull)
13. [Pull Request](#13---pull-request)
14. [git log](#14---git-log)
15. [Fork e Clone](#15---fork-e-clone)
16. [Vários Desenvolvedores no Mesmo Projeto](#16---vários-desenvolvedores-no-mesmo-projeto)


## 1 - O que e Git
O Git é um sistema de controle de versão distribuído que permite rastrear as alterações em arquivos e coordenar o trabalho em equipe. Ele é essencial para o desenvolvimento de software, permitindo que vários colaboradores trabalhem simultaneamente, mantendo um histórico completo das modificações e facilitando a colaboração sem conflitos.

### Funcionalidades principais:
- **Controle de versão**: Acompanhe as mudanças em arquivos ao longo do tempo.
- **Branching (ramificações)**: Crie novas linhas de desenvolvimento sem interferir no código principal.
- **Fusões (merge)**: Combine as alterações de diferentes ramificações.
- **Reversão**: Volte para versões anteriores se necessário.


## 2 - O que e Github
O GitHub é uma plataforma de hospedagem de código baseada no Git, que facilita a colaboração em projetos. Além de armazenar e compartilhar repositórios, oferece ferramentas para gerenciamento de projetos, revisão de código e integração contínua.

### GitHub facilita:
- Armazenamento remoto de repositórios.
- Colaboração em tempo real com outros desenvolvedores.
- Gestão de projetos e tarefas.
- Implementação de CI/CD (Integração e Entrega Contínua).


## 3 - Instalacão do Git no Windows
- 1 = Baixar o Git: Acesse https://git-scm.com e baixe a versão para Windows.
- 2 = Instalar:
   - Execute o instalador.
   - Escolha as opções padrão, a menos que prefira personalizar.
   - Na etapa "Adjusting your PATH environment", selecione "Git from the command line and also from 3rd-party software".
   - Finalize e abra o Git Bash (terminal do Git) para confirmar que foi instalado com
   ```
   git --version
   ```
   - Se a versão for exibida, está instalado com sucesso.


## Configurando sua identificacão
É importante que seu Git saiba quem você é para associar os commits ao seu nome e email.

#### Configurar nome e email:
```
git config --global user.name "Seu Nome"
git config --global user.email "seuemail@exemplo.com"
```

#### Verificar se as configurações estão corretas:
```
git config --list
```

#### Alterar configurações localmente em um projeto (opcional):
```
git config user.name "Outro Nome"
git config user.email "outroemail@exemplo.com"
```


## Configurar chave SSH no GitHub
A chave SSH permite fazer push e pull do seu repositório sem precisar digitar sua senha sempre.

#### Gerar chave SSH: Abra o Git Bash e digite:
```
ssh-keygen -t ed25519 -C "seuemail@exemplo.com"
```
- Pressione Enter para usar o caminho padrão.
- Se quiser, defina uma senha (ou apenas aperte Enter para deixar sem senha).


#### Adicionar a chave SSH ao GitHub:

- Copie a chave pública
```
cat ~/.ssh/id_ed25519.pub
```
- Acesse GitHub SSH Settings.
- Clique em New SSH key e cole a chave copiada no campo.


#### Testar conexão: 
```
ssh -T git@github.com
```
Se funcionar, você verá uma mensagem de boas-vindas.


## 4 - Salvando a primeira versão de um projeto no GitHub

#### Criar um repositório no GitHub:
- Acesse GitHub e crie um novo repositório.
- Dê um nome e deixe-o público ou privado.

#### Inicializar o Git no projeto
- Abra o terminal ou Git Bash na pasta do seu projeto e digite:
```
git init
```

#### Adicionar arquivos para controle de versão:
```
git add .
```

#### Criar o primeiro commit:
```
git commit -m "Primeira versão do projeto"
```

#### Adicionar repositório remoto:
```
git remote add origin git@github.com:seuusuario/nomedorepositorio.git
```

#### Enviar a primeira versão para o GitHub:
```
git push -u origin main
```

- **git push**: Envia as alterações locais para o repositório remoto.
- **-u (upstream)**: Define a branch remota como padrão para futuros pushes. Assim, da próxima vez, você pode usar apenas: **git push**
- **origin**: É o nome padrão do repositório remoto.
- **main**: Indica a branch principal para onde você está enviando o código.




## 5 - Salvando um Novo Commit
#### 5.1 - Fazer alterações nos arquivos.

#### 5.2 - Verificar status das mudanças:
```
git status
```

#### 5.3 - Adicionar os arquivos modificados:
```
git add .
```

#### 5.4 - Criar o commit:
```
git commit -m "Descrição do que foi alterado"
```

#### 5.5 - Enviar o commit para o GitHub:
```
git push
```

## 6 - Arquivo gitignore
O arquivo .gitignore é usado para indicar quais arquivos ou pastas o Git deve ignorar e não versionar. Isso é útil para arquivos temporários, credenciais ou dependências que não precisam estar no repositório.

#### 6.1 - Criar um arquivo .gitignore na raiz do projeto.
Exemplo de conteúdo:
```
# Ignorar pastas de sistema
.DS_Store
node_modules/

# Ignorar arquivos de log e temporários
*.log
*.tmp

# Ignorar configurações locais
.env
```

#### 6.2 - Adicionar o .gitignore ao controle de versão:
```
git add .gitignore
git commit -m "Adicionar arquivo .gitignore"
git push
```


## 7 - Branch no Git
Uma branch (ramificação) é uma linha paralela de desenvolvimento dentro de um projeto Git. Ela permite que você trabalhe em novas funcionalidades ou correções sem afetar o código principal. Quando a nova funcionalidade está pronta, você pode mesclá-la (merge) com a branch principal, geralmente chamada de main ou master.

### Por Que Usar Branches?
- **Isolamento**: Trabalhe em novas funcionalidades sem interferir no código que já está funcionando.
- **Colaboração**: Cada colaborador pode trabalhar em uma branch específica, evitando conflitos.
- **Controle**: Teste e revise mudanças antes de integrá-las ao código principal.

### Branches Mais Comuns
- **main ou master**: A branch principal, onde geralmente está o código mais estável.
- **Branches de funcionalidades**: Usadas para desenvolver uma nova funcionalidade ou feature (recurso). Exemplo: nova-funcionalidade
- **Branches de correções**: Criadas para corrigir bugs no sistema. Exemplo: correcao-bug

### 7.1 - Comandos Básicos para Gerenciar Branches
#### Criar uma Nova Branch
```
git branch nome-da-branch
```

#### Trocar para Outra Branch
```
git checkout nome-da-branch
```

#### Criar e Mudar para uma Nova Branch ao Mesmo Tempo
```
git checkout -b nome-da-branch
```

### 7.2 - Visualizando Branches
#### Listar todas as branches locais
```
git branch
```

#### Listar branches remotas
```
git branch -r
```

#### Listar branches locais e remotas
```
git branch -a
```


### 7.3 - Fazendo Merge (Mesclando Branches)
Quando uma funcionalidade ou correção está pronta, você pode mesclar a branch com a branch principal. Exemplo de Merge:

#### Primeiro, vá para a branch main:
```
git checkout main
```

#### Agora, faça o merge da branch com a nova funcionalidade:
```
git merge nova-funcionalidade
```


### 7.4 - Deletando uma Branch
Após mesclar a branch, você pode deletá-la para manter o repositório organizado.

#### Deletar uma branch local:
```
git branch -d nome-da-branch
```

#### Deletar uma branch remota:
```
git push origin --delete nome-da-branch
```


### 7.5 - Quando e Como Usar Branches?
- **Funcionalidades grandes**: Crie uma branch para cada nova funcionalidade.
- **Correções críticas**: Use uma branch separada para corrigir bugs e depois mescle com o código principal.
- **Colaboração**: Cada membro da equipe pode trabalhar em sua própria branch e depois mesclá-la.


### 7.6 - Exemplo Completo de Uso de Branches
#### Crie e mude para uma nova branch:
```
git checkout -b nova-funcionalidade
```

#### Adicione algumas alterações:
```
git add .
git commit -m "Adicionar nova funcionalidade"
```

#### Envie a branch para o repositório remoto:
```
git push -u origin nova-funcionalidade
```

#### Mescle a branch com a main após a revisão:
```
git checkout main
git merge nova-funcionalidade
```

#### Delete a branch depois do merge:
```
git branch -d nova-funcionalidade
```

## 8 - Branches Locais e Remotas
No Git, uma branch (ramificação) é usada para isolar diferentes linhas de desenvolvimento. Essas branches podem ser **locais**, existindo apenas no seu computador, ou **remotas**, armazenadas no repositório remoto, como no GitHub, GitLab ou Bitbucket. Entender a diferença entre branches locais e remotas é essencial para trabalhar de forma colaborativa e eficiente.

### 8.1 - O Que é uma Branch Local?
É uma branch que existe apenas no seu repositório local (na sua máquina).
Essas branches são visíveis apenas para você, a menos que você as envie para o repositório remoto.

#### Comandos Relacionados a Branches Locais:
Criar uma nova branch local:
```
git checkout -b minha-branch
```
Listar branches locais:
```
git branch
```
Trocar para outra branch:
```
git checkout nome-da-branch
```
Deletar uma branch local:
```
git branch -d minha-branch
```

**Exemplo**:
Você pode criar uma branch local para trabalhar em uma nova funcionalidade:
```
git checkout -b nova-funcionalidade
```
Esta branch existe apenas no seu computador e não será visível para outras pessoas até que você a envie para o repositório remoto com git push.


### 8.2 - O Que é uma Branch Remota?
É uma branch armazenada em um repositório remoto (como no GitHub). Ela permite que outros colaboradores tenham acesso ao seu código. Branches remotas são identificadas pelo prefixo do repositório remoto, como origin/main.


#### Comandos Relacionados a Branches Remotas:
Listar branches remotas:
```
git branch -r
```
Criar uma branch remota (a partir de uma local):
```
git push -u origin nova-funcionalidade
```
Deletar uma branch remota:
```
git push origin --delete nome-da-branch
```
Trazer atualizações das branches remotas:
```
git fetch
```

**Exemplo**:
Se você criou uma branch chamada nova-funcionalidade e quer compartilhá-la com outros desenvolvedores:
```
git push -u origin nova-funcionalidade
```
Agora, essa branch estará disponível no repositório remoto e outras pessoas poderão usá-la.


### 8.3 - Diferenças Entre Branches Locais e Remotas

| Aspecto   | Branch Local       | Branch Remota                                   |
| :---------- | :--------- | :------------------------------------------ |
| `Localização` | No repositório local (sua máquina) | No repositório remoto (GitHub, etc.) |
| `Visibilidade` | Apenas você pode ver e trabalhar nela | Acessível para todos com acesso ao repositório remoto |
| `Criação` | Criada com git branch ou git checkout -b | Criada com git push a partir de uma branch local |
| `Uso` | Usada para desenvolver de forma isolada | Usada para colaborar e compartilhar código |
| `Sincronização` | Não precisa de conexão com internet | Requer comandos como git push ou git pull para sincronização |


### 8.4 - Como Sincronizar Branches Locais e Remotas
#### 8.4.1 - Criar uma Branch Local e Enviá-la para o Repositório Remoto
```
git checkout -b nova-funcionalidade
git push -u origin nova-funcionalidade
```
O parâmetro -u estabelece um upstream tracking para que futuras alterações possam ser enviadas com apenas:
```
git push
```

#### 8.4.2 - Atualizar Branch Local com Alterações Remotas
Se a branch foi modificada no repositório remoto, você pode atualizá-la localmente:
```
git pull origin nova-funcionalidade
```

#### 8.4.3 - Trazer Todas as Atualizações do Repositório Remoto
```
git fetch
```
Este comando não mescla as alterações, apenas baixa as referências do remoto. Para mesclar as mudanças, você precisa usar:
```
git merge origin/nome-da-branch
```

### 8.4 - Resumo
- **Branch Local**: Existe apenas no seu computador e é usada para desenvolver isoladamente.
- **Branch Remota**: Armazenada no repositório remoto e acessível por todos com acesso ao projeto.
- Para colaborar com outros desenvolvedores, você precisa enviar suas branches locais para o remoto usando **git push**. Já para receber as alterações mais recentes, você pode usar **git pull** ou **git fetch**.



## 9 - Estados dos Arquivos no Git

### Modified (Modificado)
- O arquivo foi editado, mas ainda não está no stage para ser commitado.
- O Git percebe que houve mudanças, mas essas mudanças ainda não fazem parte do próximo commit.

### Staged (Em Staging)
- O arquivo foi adicionado ao stage com **git add**.
- Ele agora está preparado para ser incluído no próximo commit.
Você pode adicionar vários arquivos ao stage antes de criar um commit.

### Committed (Comitado)
- As mudanças foram salvas no repositório com um commit.
- O commit guarda um histórico permanente do estado do projeto naquele momento.


### Fluxo Completo de Commit no Git

#### 9.1.1 - Fazer Alterações em um Arquivo
Modifique um ou mais arquivos no seu projeto. Esses arquivos agora estão no estado modified.
```
# Verifica o status do repositório
git status
```
Exemplo de Saída:
```
modified: arquivo.txt
```

#### 9.1.2 - Adicionar Arquivo ao Staging (Stage)
Use o comando **git add** para mover o arquivo do estado modified para staged.
```
# Adiciona um arquivo ao stage
git add arquivo.txt
```
Para adicionar todos os arquivos modificados:
```
git add .
```

#### 9.1.3 - Confirmar o Commit (Committed)
Depois de adicionar ao stage, você precisa fazer o commit para salvar as alterações.
```
# Cria um commit com uma mensagem
git commit -m "Descrição das alterações"
```
Após isso, o arquivo agora está comitado e faz parte do histórico do repositório.


### Comandos para Mover Entre os Estados
#### 9.2.1 - Mover do Stage de Volta para Modificado (Unstage)
Se você adicionou um arquivo ao stage, mas ainda não quer comitá-lo, use:
```
git reset HEAD arquivo.txt
```
O arquivo volta para o estado modified.

#### 9.2.2 - Desfazer Alterações Não Commitadas (Modified)
Se quiser descartar as alterações feitas em um arquivo (voltar à versão do último commit):
```
git checkout -- arquivo.txt
```

#### 9.2.3 - Alterar o Último Commit (Se Ainda Não Foi Enviado)
Se você comitou, mas percebeu que precisa ajustar algo (como a mensagem), pode usar:
```
git commit --amend -m "Nova mensagem de commit"
```

## 10 - Desfazer e Excluir Commits
No Git, é possível desfazer ou excluir commits, seja porque você cometeu um erro ou porque precisa reorganizar o histórico. Existem várias formas de desfazer commits, dependendo se você já enviou as alterações para o repositório remoto ou não.

### 10.1 - Desfazendo o Último Commit (Localmente)
Se o último commit foi feito localmente e ainda não foi enviado para o repositório remoto, você pode desfazê-lo com:

#### a) Desfazer o Commit, Mantendo as Alterações (Soft Reset)
```
git reset --soft HEAD~1
```
O commit é removido, mas as alterações continuam no stage (prontas para um novo commit).

#### b) Desfazer o Commit e Tirar as Alterações do Stage (Mixed Reset)
```
git reset HEAD~1
```
O commit é desfeito, e as alterações voltam para o estado modificado (fora do stage).

####  c) Desfazer o Commit e Apagar as Alterações (Hard Reset)
```
git reset --hard HEAD~1
```
O commit é desfeito, e todas as alterações são perdidas.

### 10.2 - Excluir Commits Enviados para o Remoto
Se você já fez push do commit para o repositório remoto, você precisará remover ou reverter o commit tanto localmente quanto no repositório remoto.

#### a) Reverter um Commit (Cria um Novo Commit de Reversão)
A reversão é a forma mais segura, pois mantém o histórico, mas desfaz as alterações feitas por um commit anterior.
```
git revert <ID-do-commit>
```
O Git abrirá um editor para você adicionar uma mensagem explicando a reversão.
Após confirmar, um novo commit é criado que desfaz as mudanças do commit especificado.

#### b) Excluir o Commit no Remoto com git push --force (Hard Reset)
Se você precisar apagar um commit do histórico remoto, pode usar git reset e depois enviar forçadamente para o repositório remoto.

#### b.1) Fazer um reset localmente:
```
git reset --hard HEAD~1
```
#### b.2) Enviar para o remoto forçadamente:
```
git push --force
```

#### Atenção:
- Usar --force pode causar problemas se outras pessoas estiverem trabalhando no mesmo repositório.
- Certifique-se de que ninguém depende do commit que você está removendo.



### 10.3 - Usando git checkout para Voltar a Um Commit ou Arquivo
Com o git checkout, você pode voltar a um commit específico ou restaurar um arquivo modificado, sem alterar o histórico de commits.

#### a) Navegar para um Commit Específico (Detached HEAD)
```
git checkout <ID-do-commit>
```
Isso coloca o repositório em estado detached HEAD. Você pode explorar o estado do projeto nesse commit, mas precisará voltar para uma branch para continuar trabalhando.
```
git checkout main
```

#### b) Voltar a Um Arquivo Modificado Sem Alterar o Histórico
```
git checkout -- nome-do-arquivo
```
Isso desfaz todas as alterações não commitadas no arquivo especificado, restaurando-o para o último commit.


### 10.4 - Desfazer Vários Commits
Se você quiser desfazer mais de um commit, pode usar o HEAD~n, onde n é o número de commits a desfazer.

#### Exemplo: Desfazer os Últimos 3 Commits
```
git reset --soft HEAD~3
```
Ou, para apagar completamente as alterações dos últimos 3 commits:
```
git reset --hard HEAD~3
```

### 10.5 - Excluir uma Branch com Commits Indesejados
Se você cometeu em uma branch específica e quer removê-la junto com os commits:

#### Deletar a branch local:
```
git branch -D nome-da-branch
```
#### Deletar a branch remota:
```
git push origin --delete nome-da-branch
```

### 10.6 - Cancelar um Commit Durante um Rebase
Se você está fazendo um rebase e quer excluir um commit específico:

#### a) Inicie um rebase interativo:
```
git rebase -i HEAD~n
```
#### b) No editor, altere pick para drop no commit que deseja excluir.
#### c) Salve e feche o editor para aplicar as mudanças.


### 10.7 - Resumo dos Comandos Importantes
| Comando   | Descrição       | 
| :---------- | :--------- | 
| `git reset --soft HEAD~1` | Remove o commit, mantém as alterações no stage. | 
| `git reset --hard HEAD~1` | Remove o commit e apaga as alterações. | 
| `git revert <ID-do-commit>` | Cria um novo commit que desfaz o anterior. |  
| `git push --force` | Envia forçadamente as mudanças para o remoto. |  
| `git branch -D nome-da-branch` | Deleta uma branch local com commits indesejados. |  
| `git checkout <ID-do-commit>` | Navega para um commit específico (Detached HEAD). |  
| `git checkout -- nome-do-arquivo` | Desfaz alterações não commitadas em um arquivo. |  
| `git rebase -i HEAD~n` | Edita ou exclui commits durante um rebase. |  


## 11 - Como Resolver Conflitos no Git
Um conflito no Git acontece quando duas ou mais pessoas (ou você mesmo) fazem alterações conflitantes na mesma parte de um arquivo, e o Git não consegue mesclar essas alterações automaticamente. Isso geralmente ocorre durante operações como merge, rebase, ou pull.

### Quando Ocorrem Conflitos?
- **Merge**: Quando você tenta combinar duas branches e ambas possuem mudanças conflitantes no mesmo arquivo.
```
git merge nome-da-branch
```
- **Pull**: Quando você traz alterações do remoto e há mudanças conflitantes.
```
git pull origin main
```
- **Rebase**: Ao aplicar commits de uma branch em cima de outra que tem alterações incompatíveis.
```
git rebase main
```

### Passo a Passo para Resolver Conflitos
#### 11.1 - Detectando o Conflito
Quando ocorre um conflito, o Git vai exibir uma mensagem no terminal:

```
Auto-merging arquivo.txt
CONFLICT (content): Merge conflict in arquivo.txt
Automatic merge failed; fix conflicts and then commit the result.
```
Use git status para verificar quais arquivos estão em conflito:

```
git status
```

Exemplo de saída:
```
both modified: arquivo.txt
```

#### 11.2 - Editar Arquivos em Conflito
Abra o arquivo em conflito e você verá algo assim:
```
<<<<<<< HEAD
Código da sua branch atual
=======
Código vindo da branch que você está mesclando
>>>>>>> nome-da-branch-remota
```
- **<<<<<<< HEAD**: Esta é a versão da sua branch atual.
- **=======**: Separador entre as versões conflitantes.
- **>>>>>>>**: Esta é a versão da branch que você está mesclando.

#### 11.3 - Resolver o Conflito Manualmente
Agora você precisa escolher qual código manter ou combinar as mudanças.

- Exemplo: Se você quer manter sua versão, apague a versão que veio do merge:
```
Código da sua branch atual
```

- Ou, se você deseja manter a versão da outra branch:
```
Código vindo da branch que você está mesclando
```

- Se necessário, combine as duas versões:
```
Código da sua branch atual + Código vindo da branch que você está mesclando
```

#### 11.4 - Adicionar os Arquivos Resolvidos ao Stage
Depois de resolver o conflito em todos os arquivos, adicione-os ao stage.

```
git add arquivo.txt
```


#### 11.5 - Criar um Novo Commit
Após resolver os conflitos e adicionar os arquivos ao stage, crie um commit para concluir a operação de merge.

```
git commit -m "Resolver conflitos durante o merge"
```

- No caso de pull, o git pull será concluído após o commit.
- No caso de rebase, finalize o rebase:
```
git rebase --continue
```


#### 11.6 - Cancelar o Merge ou Rebase (Se Preciso)
Se você quiser abortar o processo de merge ou rebase e voltar ao estado anterior:

- Cancelar um merge:
```
git merge --abort
```

- Cancelar um rebase:
```
git rebase --abort
```


### Exemplo Completo de Resolução de Conflito Durante um Merge
- **a)** Tentar fazer o merge:
```
git merge nome-da-branch
```

- **b)** Verificar arquivos em conflito:
```
git status
```

- **c)** Editar e resolver conflitos em cada arquivo.
- **d)** Adicionar os arquivos ao stage:

```
git add arquivo.txt
```

- **e)** Criar o commit de resolução:
```
git commit -m "Resolver conflitos durante o merge"
```


### Verificar Histórico de Merge e Conflitos
Visualizar o histórico de commits:
```
git log --oneline --graph
```

Verificar o conteúdo dos arquivos mesclados:
```
git diff HEAD
```


### Dicas para Evitar Conflitos
- **a)** Sincronize com o repositório remoto frequentemente:
```
git pull origin main
```

- **b)** Divida seu trabalho em pequenos commits e mescle frequentemente para evitar grandes divergências.

- **c)** Comunique-se com a equipe para evitar trabalhar no mesmo código simultaneamente.

- **d)** Use ferramentas de comparação (diff) para resolver conflitos mais facilmente:
   - Ferramentas como VSCode, Meld, ou P4Merge ajudam a visualizar as diferenças e resolver conflitos rapidamente.



## 12 - git pull 

### Como Funciona o git pull origin main
```
git pull origin main
```
- **git pull**: Busca e mescla as alterações do repositório remoto no repositório local.
- **origin**: É o nome padrão do repositório remoto configurado no seu projeto.
- **main**: Refere-se à branch principal do projeto.

###  Quando Usar git pull origin main?
- Antes de começar a trabalhar, para garantir que você tenha a versão mais atualizada do código.
- Para sincronizar seu trabalho local com as últimas alterações feitas por outros colaboradores.

###  O Que o git pull Faz Internamente?
O **git pull** é, na verdade, uma combinação de dois comandos:
- **git fetch** – Baixa as referências e commits mais recentes do remoto, mas não os mescla.
- **git merge** – Mescla as mudanças do repositório remoto na sua branch local.


### Exemplo de Uso Prático
#### a) Você está na branch main local:
```
git checkout main
```

#### b) Verifique se há mudanças no repositório remoto e as mescle:
```
git pull origin main
```

#### c) Se não houver conflitos, o terminal indicará que a mesclagem foi bem-sucedida.
Exemplo de Saída:

```
Updating 2f4d8c3..6f5a89b
Fast-forward
 arquivo.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```


### Lidando com Conflitos Durante o Pull
Se houver alterações conflitantes entre o que você fez localmente e o que foi alterado remotamente, você verá algo assim:

```
Auto-merging arquivo.txt
CONFLICT (content): Merge conflict in arquivo.txt
Automatic merge failed; fix conflicts and then commit the result.
```

### Passo a Passo para Resolver Conflitos
#### a) Use o git status para ver quais arquivos estão em conflito:
```
git status
```

#### b) Abra os arquivos em conflito e resolva as diferenças manualmente.

#### c) Adicione os arquivos resolvidos ao stage:
```
git add arquivo.txt
```

#### d) Crie um commit para concluir a mesclagem:
```
git commit -m "Resolver conflitos durante o pull"
```


### Como Evitar Conflitos ao Usar git pull
- Faça commits pequenos e frequentes.
- Puxe as mudanças regularmente (ou seja, use git pull antes de fazer muitas alterações).
- Comunique-se com a equipe para evitar que várias pessoas modifiquem os mesmos arquivos ao mesmo tempo.


### Se Você Quiser Apenas Baixar as Alterações (Sem Mesclar)
Se você quer apenas baixar as atualizações do repositório remoto sem mesclar automaticamente, use:
```
git fetch origin main
```
Isso baixa as alterações para seu repositório local, mas você pode decidir quando e como fazer o merge manualmente.



## 13 - Pull Request
Um Pull Request (PR) é uma solicitação de merge em plataformas de hospedagem de código, como GitHub, GitLab ou Bitbucket. Ele é utilizado quando você quer mesclar as mudanças de uma branch para outra, geralmente de uma branch de funcionalidade para a branch principal (main ou master).

### Quando Usar um Pull Request?
- Quando você conclui uma nova funcionalidade ou correção em uma branch separada e deseja que essa mudança seja revisada antes de ser incorporada à branch principal.
- Em projetos colaborativos, outros desenvolvedores podem revisar, comentar e aprovar as alterações antes do merge.


### Fluxo Completo de um Pull Request
#### 13.1 Criar uma Nova Branch

- **a)** Crie uma nova branch para desenvolver a funcionalidade:
```
git checkout -b nova-funcionalidade
```

- **b)** Adicione e faça commits com as mudanças:
```
git add .
git commit -m "Adiciona nova funcionalidade"
```

- **c)** Envie a branch para o repositório remoto:
```
git push -u origin nova-funcionalidade
```


#### 13.2 Abrir um Pull Request no GitHub
- **a)** Acesse seu repositório no GitHub.
- **b)** Clique em "Compare & pull request" ao lado da branch que você acabou de enviar.
- **c)** Verifique se:
   - **Base branch**: É a branch para onde você deseja enviar as alterações (geralmente main ou master).
   - **Compare branch**: É a branch que contém suas mudanças (ex: nova-funcionalidade).

- **d)** Adicione um título e uma descrição explicando o que foi alterado e por quê.
- **e)** Clique em "Create pull request".


#### 13.3 Revisão e Aprovação
- Outros desenvolvedores podem agora revisar o PR, adicionar comentários ou solicitar alterações.
- O PR pode ser aprovado e mesclado depois que todos concordarem que está pronto.

#### 13.4 Mesclando o Pull Request
- **a)** Se as alterações estão prontas, clique em "Merge pull request".
- **b)** Escolha o tipo de merge:

   - **Merge commit**: Cria um novo commit para o merge.
   - **Squash and merge**: Combina todos os commits em um só antes do merge.
   - **Rebase and merge**: Aplica os commits da branch de funcionalidade diretamente sobre a branch principal.
- **c)** Clique em **"Confirm merge"** para concluir.

#### 13.5 Deletando a Branch Após o Merge
- Após o merge, é uma boa prática excluir a branch de funcionalidade para manter o repositório organizado.
- No GitHub, você pode clicar em "Delete branch" logo após a mesclagem.


### Comandos Úteis para Pull Requests
- **a)** Atualizar a Branch Antes do PR
Antes de abrir o PR, é importante garantir que sua branch está atualizada com a branch principal.
```
git checkout nova-funcionalidade
git pull origin main
git push
```

- **b)** Verificar Branches Remotas e Locais
Listar branches locais:
```
git branch
```
Listar branches remotas:
```
git branch -r
```

### Diferença Entre Pull Request e git pull
- **Pull Request**: É uma solicitação para mesclar uma branch em outra e geralmente envolve uma revisão de código.
- **git pull**: Atualiza seu repositório local com as alterações do repositório remoto.


## 14 - git log

### Uso Básico do git log
```
git log
```
Saída:
```
commit a1b2c3d4 (HEAD -> main)
Author: Seu Nome <seuemail@exemplo.com>
Date:   Fri Oct 25 12:00:00 2024 -0300

    Adiciona nova funcionalidade
```
- **commit a1b2c3d4**: O ID (ou hash) do commit.
- **HEAD -> main**: Indica a branch atual e onde o HEAD está apontando.
- **Author**: Quem fez o commit.
- **Date**: Quando o commit foi realizado.
- **Mensagem**: A mensagem associada ao commit, explicando as alterações.


### Opções Úteis do git log
#### 14.1 - Exibir Histórico Resumido (oneline)
```
git log --oneline
```
- Saída:

```
a1b2c3d4 Adiciona nova funcionalidade
5f6e7d8a Corrige bug na tela de login
```
- Cada commit é exibido em uma linha com seu ID curto e a mensagem de commit.


#### 14.2 - Limitar o Número de Commits Exibidos
```
git log -n 5
```
Exibe apenas os últimos 5 commits.


#### 14.3 - Mostrar Commits de um Arquivo Específico
```
git log -- arquivo.txt
```
Exibe apenas os commits que modificaram o arquivo arquivo.txt.


#### 14.4 - Mostrar Diferenças Entre Commits (git log -p)
```
git log -p
```
Exibe as alterações feitas em cada commit (um diff para cada um).


#### 14.5 - Ver Log de Uma Branch Remota
```
git log origin/main
```
Exibe o histórico de commits da branch remota main.


#### 14.6 - Filtrar Commits por Autor
```
git log --author="Nome do Autor"
```
Exibe apenas os commits realizados pelo autor especificado.


#### 14.7 - Log Com Data e Mensagens Resumidas
```
git log --pretty=format:"%h %an %ar - %s"
```

Saída:
```
a1b2c3d4 Seu Nome 2 days ago - Adiciona nova funcionalidade
5f6e7d8a Outro Autor 4 weeks ago - Corrige bug
```
- **%h**: Hash curto.
- **%an**: Nome do autor.
- **%ar**: Data relativa.
- **%s**: Mensagem do commit.


### Comandos Relacionados
- Ver um Commit Específico:

```
git show <ID-do-commit>
```
Exibe os detalhes e alterações feitas no commit especificado.

- Comparar Dois Commits:
```
git diff <ID-commit-1> <ID-commit-2>
```

### Resumo dos Comandos Importantes
| Comando   | Descrição       | 
| :---------- | :--------- | 
| `git log` | Exibe o histórico completo de commits. | 
| `git log --oneline` | Exibe o histórico resumido (um commit por linha). | 
| `git log -n 5` | Mostra os últimos 5 commits. |  
| `git log --author="Nome"` | Filtra commits por autor. |  
| `git log -- arquivo.txt` | Mostra commits que alteraram um arquivo específico. |  
| `git log -p` | Exibe as diferenças em cada commit. |  



## 15 - Fork e Clone
Fork e Clone são dois conceitos importantes no Git/GitHub, mas são usados para propósitos diferentes. Ambos permitem trabalhar em repositórios, mas o fork cria uma cópia completa do repositório em sua conta GitHub, enquanto o clone cria uma cópia local do repositório para trabalhar no seu computador.

### O Que é Fork?
- Fork é uma cópia do repositório remoto para sua conta no GitHub ou GitLab.
- Ele é útil quando você quer modificar um projeto existente sem alterar diretamente o repositório original.
- Permite que você trabalhe livremente e, se quiser, envie Pull Requests para o projeto original.
- **Uso comum**: Contribuições em projetos open-source ou personalização de repositórios de outras pessoas.

### Como Fazer Fork de um Repositório
- Acesse o repositório no GitHub que deseja forkar.
- Clique em "Fork" no canto superior direito.
- Escolha sua conta pessoal ou uma organização.
- O GitHub criará uma cópia do repositório na sua conta.


### Exemplo de Fork:
Você quer colaborar com um projeto chamado projeto-exemplo. Após o fork, ele estará disponível na sua conta com o nome:

```
https://github.com/seu-usuario/projeto-exemplo
```
Agora, você pode modificá-lo e enviar um Pull Request para o repositório original.


### O Que é Clone?
- Clone é o processo de baixar uma cópia local de um repositório remoto (seu ou de outra pessoa) para o seu computador.
- Ele permite que você trabalhe localmente, faça alterações e depois envie essas mudanças de volta para o repositório remoto.
- **Uso comum**: Desenvolver localmente em um projeto e sincronizar com o repositório remoto.


### Como Clonar um Repositório
- No repositório no GitHub, clique em "Code".
- Escolha HTTPS ou SSH e copie a URL.
- No terminal, execute:
```
git clone <URL-do-repositorio>
```


### Exemplo de Clone:
Você quer baixar o repositório forkado ou original para trabalhar localmente.
```
git clone https://github.com/seu-usuario/projeto-exemplo.git
```
Isso criará uma pasta chamada projeto-exemplo contendo todos os arquivos do repositório.


### Diferença Entre Fork e Clone
| Aspecto   | Fork       | Clone | 
| :---------- | :--------- |  :--------- | 
| `Localização` | Cópia no GitHub (repositório remoto) | Cópia local no seu computador | 
| `Propósito` | Modificar sem afetar o repositório original	 | Trabalhar localmente no projeto |
| `Modificação` | Precisa enviar Pull Request para o projeto original | Envia mudanças com push para o remoto |
| `Comando Git` | Feito via interface do GitHub | `git clone <URL>`  |


### Como Usar Fork e Clone Juntos
- **1** = Fork o projeto original no GitHub para sua conta.

- **2** = Clone o fork para sua máquina:
```
git clone https://github.com/seu-usuario/projeto-exemplo.git
```
- **3** = Trabalhe localmente fazendo alterações e commits:

```
git add .
git commit -m "Minha contribuição"
git push origin main
```
- **4** = Envie um Pull Request para o repositório original.


### Sincronizando o Fork com o Repositório Original
- **1** = Adicione o repositório original como upstream:
```
git remote add upstream https://github.com/original-usuario/projeto-exemplo.git
```
- **2** = Busque atualizações do upstream:
```
git fetch upstream
```

- **3** = Mescle as mudanças na sua branch local:
```
git merge upstream/main
```

- **4** = Envie as atualizações para o fork no GitHub:
```
git push origin main
```


### Resumo dos Comandos
| Comando   | Descrição       | 
| :---------- | :--------- | 
| `git clone <URL>` | Clona um repositório remoto para sua máquina.
| `git remote add upstream <URL-original>` | Adiciona o repositório original como upstream.
| `git fetch upstream` | Busca as atualizações do repositório original.
| `git merge upstream/main` | Mescla as atualizações na branch local.
| `git push origin main` | Envia as mudanças para o fork no GitHub.



## 16 - Vários Desenvolvedores no Mesmo Projeto
Quando dois ou mais desenvolvedores trabalham no mesmo projeto, é fundamental organizar o fluxo de trabalho para evitar conflitos e manter o repositório sincronizado. O Git e o GitHub oferecem ferramentas para facilitar a colaboração, garantindo que as alterações de todos sejam incorporadas sem problemas.

### 16.1 - Fluxo com Branches (Feature Branch Workflow)
Cada desenvolvedor cria branches específicas para trabalhar em suas tarefas. Quando uma tarefa é concluída, o desenvolvedor abre um Pull Request para mesclar a branch no repositório principal.

- **a)** Clonar o Repositório
```
git clone https://github.com/empresa/projeto.git
cd projeto
```

- **b)** Criar uma Nova Branch para a Tarefa
```
git checkout -b minha-funcionalidade
```

- **c)** Fazer Alterações e Criar Commits
```
git add .
git commit -m "Implementa nova funcionalidade"
```

- **d)** Enviar a Branch para o Remoto
```
git push origin minha-funcionalidade
```

- **e)** Abrir um Pull Request no GitHub
   - Acesse o repositório no GitHub e clique em Compare & Pull Request.
   - Descreva as alterações e envie para revisão.

- **f)** Revisar, Aprovar e Mesclar
   - Outros desenvolvedores revisam o Pull Request.
   - Quando aprovado, a branch é mesclada na main.


### 16.2 - Atualizando o Repositório Local
Antes de começar a trabalhar, é essencial garantir que seu código esteja atualizado com as últimas mudanças no repositório remoto.

- **a)** Mudar para a Branch Principal
```
git checkout main
```

- **b)** Baixar e Mesclar Alterações do Remoto
```
git pull origin main
```


### 16.3 - Resolver Conflitos de Código
Conflitos podem acontecer quando dois desenvolvedores alteram a mesma parte de um arquivo. Veja como resolvê-los:

- **a)** Fazer Pull para Verificar Alterações do Remoto
```
git pull origin main
```

- **b)** Se houver conflitos, o Git mostrará uma mensagem como esta:
```
CONFLICT (content): Merge conflict in arquivo.txt
Editar o Arquivo em Conflito
O Git marca as seções conflitantes assim:

plaintext
Copiar código
<<<<<<< HEAD
Código do desenvolvedor A
=======
Código do desenvolvedor B
>>>>>>> main
```

- **c)** Escolha e Combine o Código Corretamente, depois adicione o arquivo ao stage:
```
git add arquivo.txt
```

- **d)** Criar um Commit para Finalizar a Resolução
```
git commit -m "Resolve conflito em arquivo.txt"
```

- **e)** Enviar as Alterações para o Repositório Remoto
```
git push origin minha-funcionalidade
```


### 16.4 - Sincronizando Forks
Quando você trabalha com um fork do projeto, é necessário manter o seu fork sincronizado com o repositório original.

- **a)** Adicionar o Repositório Original como Upstream
```
git remote add upstream https://github.com/empresa/projeto.git
```

- **b)** Buscar Alterações do Upstream
```
git fetch upstream
```

- **c)** Mesclar Alterações com a Branch Principal
```
git checkout main
git merge upstream/main
```

- **d)** Enviar para o Fork
```
git push origin main
```


### 16.5 - Fluxo com Revisão de Código e Pull Requests
- **Pull Requests (PRs)**: São usados para revisar e aprovar alterações antes de integrá-las à branch principal.
- **Revisores**: Outros desenvolvedores podem adicionar comentários, sugerir melhorias ou solicitar mudanças.
- **Checks Automatizados**: Pode-se configurar CI/CD para rodar testes automáticos sempre que um PR é aberto.


### 16.6 - Exemplo Completo de Trabalho Colaborativo

- **a)** Desenvolvedor A cria a branch nova-funcionalidade:
```
git checkout -b nova-funcionalidade
```

- **b)** Desenvolvedor A faz commits e envia para o GitHub:
```
git add .
git commit -m "Implementa nova funcionalidade"
git push origin nova-funcionalidade
```

- **c)** Desenvolvedor B atualiza sua branch main com o repositório remoto:
```
git checkout main
git pull origin main
```

- **d)** Desenvolvedor A abre um Pull Request para mesclar nova-funcionalidade na main.
- **e)** Desenvolvedor B revisa, aprova e mescla o PR.


### 16.7 - Resumo de Comandos Importantes
| Comando   | Descrição       | 
| :---------- | :--------- | 
| `git clone <URL>` | Clona o repositório para a máquina local.
| `git checkout -b <nova-branch>` | Cria e muda para uma nova branch.
| `git pull origin main` | Atualiza a branch local com o remoto.
| `git push origin <branch>` | Envia uma branch para o repositório remoto.
| `git remote add upstream <URL>` | Adiciona o repositório original como upstream.
| `git fetch upstream` | Baixa as atualizações do upstream.
| `git merge upstream/main` | Mescla as atualizações com a branch local.
