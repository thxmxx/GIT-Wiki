# Git Tutorial

## Introdução
Git tem sido utilizado por todo mundo como ferramenta de apoio a desenvolvimento de codigos, oferecendo diversos recursos que tornam a vida dos desenvolvedores bem menos complicada.

A rigor, o Git faz o versionamento de códigos, todavia, a forma com a qual é feita o difere das demais ferramentas de versionamento (VSC, VSS, Subversion, Bazaar etc). Conceitualmente, a grande maioria de sistemas com esse intuito enxerga os codigos como uma lista de mudanças no codigo original. Veja a figura abaixo:

![git1](https://github.com/thxmxx/GIT-Wiki/raw/master/imagens_wiki_git/git1.png)

Note que na primeira versão existiam 3 arquivos (File A, File B e File C), na segunda versão os arquivos File A e File B sofreram alterações e seus deltas foram acrescidos na segunda versão. Ou seja, para se obter o arquivo File A na segunda versão, por exemplo, basta aplicar no arquivo File A da primeira versão o delta (∆1). Esse comportamento se repete em todas as versões, ou seja, só são inseridos deltas.

A forma com que o Git enxerga os dados é diferente, ao contrário dos versionadores tradicionais, ele operar como um conjunto de snapshots (fotografias) de todo seu codigo, ou seja, a cada versão é como se o Git tirasse uma foto (instantâneo) de todos os seus arquivos e armazenasse uma referência para esse instantâneo. Obviamente por questão de eficiência, o Git não armazena os arquivos que não foram alterados, ele apenas cria um link para o arquivo identico que não foi alterado e já se encontra armazenado. Ou seja, Git enxerga os dados como uma sequência de snapshots.

![git2](https://github.com/thxmxx/GIT-Wiki/raw/master/imagens_wiki_git/git2.png)

## Os Três Estados

O Git possui três estados principais nos quais seus arquivos podem residir: **committed**, **modified** and **staged**.

1. **Committed:** Significa que o dado está armazenado com segurança na sua base de dados local.

2. **Modified:** Significa que houve mudança no dado mas o mesmo ainda não foi persistido na base de dados local.

3. **Staged:** Significa que o arquivo foi marcado como modificado na versão atual para entrar para o proximo commit.

Vamos agora ver quais são as três sessões principais que o Git utiliza para operar: **Git directory**, **Working Directory** e **Staging area**, veja a figura abaixo:

![git3](https://github.com/thxmxx/GIT-Wiki/raw/master/imagens_wiki_git/git3.png)

### Git Directory
Git directory é onde o Git armazena os metadados bem como os arquivos do banco de dados do seu projeto. Essa é a parte mais importante do Git, é o que é copiado quando um repositório é clonado de um computador.

### Working Directory
Working directory é literalmente seu diretório de trabalho, contendo um único check-out de uma versão do seu projeto. Os arquivos deste diretório são descompactados do Git directory e disponibilizados para voce utiliza-los e modifica-los.

### Staging Area
Staging area é um arquivo, geralmente contido em seu diretório Git, que armazena informações sobre o que vai entrar em seu próximo commit . É às vezes referido como o "index" , mas também é comum referir-se a ele como stage


## Workflow

Workflow O fluxo de trabalho básico Git é algo semelhante à isto:

1. Você modifica os arquivos no Working directory.
2. Você marca os arquivos, adicionando instantâneos dos mesmos para a Staging Area.
3. Você faz um commit, persistindo todos os arquivos da Staging area no seu Git directory.

Se uma versão específica de um arquivo está no Git directory, é considerado comitado (committed). Se for modificado, e foi adicionado à Staging area, que é considerado marcado. E se ele foi alterado desde o ultimo checkout, mas não foi marcado então é considerado modificado .

**Obs:** Os passos abaixo assumem que voce esteja utilizando o uma distribuição like Debian (Ubuntu, por exemplo).

### Instalação do Git
`sudo apt-get install git`

### Configurações Iniciais
`git config --global user.name "Nome do Usuario"`

`git config --global user.email email@example.com`

### Editor Default:
Substitua **'Nome-Editor'** pelo editor de sua preferência.

`git config --global core.editor Nome-Editor`

### Conferindo configurações atuais:
`git config –list`

### Ajuda:
`git help comando`

Você deve substituir **comando** pela ação da ajuda que voce procura, por exemplo:

`git help config`



## Comandos Operacionais do Git

Você pode obter um projeto Git de duas maneiras. O primeiro partindo de um projeto existente ou diretório e inicializando o Git. E o segundo clonando de um repositório Git existente em outro servidor.

### Inicializando Repositório
Esse comando cria um subdiretório chamado **.git** contendo todos os arquivos necessários para o repositório Git. Todavia não existe nada rastreável (track) em seu projeto ainda.

`git init`


### Inicializando Repositório
`git clone https://github.com/exemplo/repositorio-exemplo`

O comando acima cria um diretório chamado **repositorio-exemplo**, inicializa um diretório .git dentro do mesmo, faz o download de todos os dados desse repositório, e disponibiliza a versão mais recente na **Working area**. Se você quiser clonar o repositório em um diretório com nome diferente, basta usar:

`git clone https://github.com/exemplo/repositorio-exemplo **nome_diretorio**`

### Adicionando Arquivos ou modificações à Stage area (tracking):
`git add <file>`

Por exemplo:

`git add arquivo.txt`

Este comando é usado dar início aos arquivos controladores de versão ou para o marcar um arquivo (pronto entrar no próximo commit).

### Conferindo status dos arquivos (status):
`git status`

`git stauts -s`

Utilizando o comando **git status -s** podemos rastrear o fluxo de alterações nos arquivos, veja a imagem abaixo:


![git4](https://github.com/thxmxx/GIT-Wiki/raw/master/imagens_wiki_git/git4.png)

Quando um arquivo é adicionado (tracked) ele aparece com a letra **A**, no nado esquerdo. Da mesma forma que quando ele é alterado, após ser adicionado, ele é marcado com a letra **M**, significando que no próximo commit essa modificação não será considerada, a menos que seja adicionada à **Stage area**, usando **git add file-name**. Quando aparece a letra **D** significa que o arquivo foi deletado. Os arquivos que não foram adicionados nenhuma vez são marcados com **??**. Essa é a saída do comando git status, para este caso:

![git5](https://github.com/thxmxx/GIT-Wiki/raw/master/imagens_wiki_git/git5.png)

### Ignorando arquivos indesejados (.gitignore)

Geralmente, você não deseja que algumas classes de arquivos sejam adicionadas automaticamente ou sendo mostradas como **untracked** a todo momento. Exemplos de arquivos são logs, builds de compiladores, bibliotecas compiladas etc. Para tratar isso, voce pode criar uma lista de regras num arquivo **.gitignore**.

Essas regras devem conter os padrões que voce deseja evitar, veja alguns exemplos em: https://github.com/github/gitignore

### Diferenças (diff)
`git diff`

`git diff --staged`

`git diff --cached`

Para verificar as modificações feitas mas que não estão na **Stage area** basta usar **git diff**, sem argumentos. Para verificar quais modificações foram marcadas para entrar no próximo commit use **git diff --staged** ou **git diff --cached**.

Veja um exemplo das saídas de cada comando (a primeira do comando **git diff** e o segundo comando do **git diff --staged**. Note que o que está de vermelho foi a exclusão, de branco foi mantido e verde foi adicionado).

**git diff**

![git6](https://github.com/thxmxx/GIT-Wiki/raw/master/imagens_wiki_git/git6.png)

**git diff --staged**

![git7](https://github.com/thxmxx/GIT-Wiki/raw/master/imagens_wiki_git/git7.png)

### Comitando modificações (commit)
`git commit -m “comentario do commit”`

Esse comando é usado para enviar as modificações que já estão adicionadas na **Stage area** para o **Git directory**, ou seja, para salvar com segurança suas modificações no banco de dados local. O parametro **-m** indica que você vai adicionar um comentário para o commit. Caso exista alguma modificação que não foi adicionada à **Stage area**, a mesma deve ser adicionada usando o comando **git add file-name**.

### Removendo Arquivos (rm)

`git rm file-name` 

Remove o arquivo file

`git rm log/*.log` 

O comando abaixo remove todos arquivos com extensão **.log** do diretorio **log/**

`git rm *~` 

Remove todos os arquivos terminados com ** ~ **

Para remover um arquivo do Git voce precisa remove-lo dos arquivos marcados (tracked files, mais especificamente, remove-los da **Stage area**) e então comitar para efetivar a remoção. O comando **rm** exclui o arquivo da **Stage area** e remove ele do seu **Working directory** para evitar que ele fique exibindo mensagem “**untraked file**” nas proximas vezes.

Uma coisa muito útil ocorre quando você deseja manter um arquivo no seu **Working directory** mas deseja remove-lo da **Stage area**. Em outras palavras, quando você quer manter o arquivo no seu HD mas não quer adicionar esse arquivo no Git. Isso é bem usal quando acidentalmente se esquece de adicionar uma extensão de arquivo no .gitignore e quer remover um Log, por exemplo, da Stage mas mante-lo no HD. Para isso, use a opção --cached.

`git rm --cached file`

### Renomeando e Movimentando Arquivos (mv)
`git mv arquivo-inicial arquivo-final`

Comando renomeia o arquivo-inicial para arquivo-final, também pode ser usado para mover um arquivo. Ele é equivalente a:

`mv arquivo-inicial arquivo-final`

`git rm arquivo-inicial`

`git add arquivo-final`


### Verificar Histórico de Commits (log)
`git log`

O comando acima exibe o log dos commits, para saber quais parametros usar, faça uso do **git help commit**.


### Removendo um arquivo da Stage
`git reset HEAD nome-arquivo`

Este comando remove o arquivo **nome-arquivo** da **Stage area**.

### Descartando Mudanças em um arquivo
`git checkout -- nome-arquivo`

Este comando descarta as mudanças feitas no arquivo **nome-arquivo**, em geral usado quando se quer baixar a versão recente de um repositório e desconsiderar o arquivo pois será substituido.

### Trabalhando com Repositórios Remotos 
`git remote`

O comando acima informa em qual servidor remoto seu git está configurado.

Se voce quiser saber a URL do servidor remoto, use o parâmetro **-v**.

Para adicionar um novo repositório Git remoto como um nome abreviado você pode fazer referência facilmente, basta executar o comando nesse padrão: **git remoto add [ nome_abreviado ] [url]**. Por exemplo: 

`git remote add nome-repositorio https://github.com/paulboone/ticgit`

(lembre de substituir **nome-repositorio** pelo nome do seu repositório)


### Baixando dados de Repositórios Remotos
`git fetch [remote-name]`

Esse comando encontra o repositório remoto e baixa todos os arquivos que você ainda não possui no repositório local. Após fazer isso , você terá referências a todos os branches do repositório remoto, e você pode mesclar ou inspecionar a qualquer momento. É importante notar que o comando git fetch baixa os dados para o repositório local mas não faz a mesclagem automaticamente com nenhum arquivo que que você esteja trabalhando atualmente. Voce deve mesclar manualmente.

### Atualizando Repositórios Remotos (pushing)

Template do comando: **git push [remote-name] [branche-name]**. Este comando faz o upload do seu código para o repositório remoto, atualizando este. Vale lembrar que o comando será efetuado com sucesso apenas se o código no qual foram feitas as modificações estiver na ultima versão disponível no repositório remoto. Em outras palavras, se você fez o download da ultima versão (pull) e antes de fazer o upload das modificações (push) algum outro desenvolvedor fez um upload antes de você, isso será um problema. Nesse caso você deve baixar a versão atual, fazer o merge e depois subir suas modificações. Exemplo de push:

`git push origin master`

### Adicionando Tags
`git tag -a v1.4 -m 'Minha versao V 1.4'`

Este Comando adiciona uma tag ao seu commit (muito usado para definir versões). Você pode usar tags de maneira mais simples apenas utilizando o comando:

`git tag v1.4-leve`

Por default, o Git não transfere automaticamente as tags para o repositório remoto utilizando o camando push. Para tal, você deve fazer isso explicitamente assim que criar sua tag. O comando é semelhante ao compartilhamento de branches (será explicado adiante): **git push [remote-name] [tag-name]**. Por exemplo:

`git push origin v1.4`

Caso queira transferir todas as tags do seu repositório local para o repositório remoto uma de uma única vez, basta utilizar o comando abaixo: **git push [remote-name] --tags**.

`git push origin --tags`

Adicionando Tags git tag -a v1.4 -m 'Minha versao V 1.4'

Este Comando adiciona uma tag ao seu commit (muito usado para definir versões). Você pode usar tags de maneira mais simples apenas utilizando o comando:

`git tag -a v1.4 -m 'Minha versao V 1.4'`

## Branches

Branches são ramificações de outros branches, usual quando se deseja trabalhar em uma nova funcionalidade (feature). O Branch, basicamente, é um clone do branch o originou. Dessa forma, você consegue desenvolver uma nova funcionalidade separadamente, o que tras grande facilidade para desenvolvimento distribuído. Veja a figura abaixo exemplificando o uso dos branches.

![git8](https://github.com/thxmxx/GIT-Wiki/raw/master/imagens_wiki_git/git8.png)

O comando abaixo cria um novo branch chamado **branch-name** (caso não exista) e faz o checkout para o mesmo. (lembre de substituir **branch-name** pelo nome do seu branch)

`git checkout -b branch-name`

Ele na verdade é um atalho para:

`git branch develop`

`git checkout develop`

## Tipos de Branches e Estrutura Básica

Esse o workflow descrito com boas praticas pra desenvolvimento de um software utilizando git como controle de versão. Vale ressaltar que em projetos muito maiores, deveria ser necessário adicionar outros branches fixos (homologação, teste etc).

A estrutura do Git para esse workflow é dividida em **Branches Fixos** e **Branches de Suporte**.

### **Branches Fixos**:

1. Develop
2. Production

### **Branches de Suporte**:

1. Feature
2. Releases
3. Hotfix


### Develop Branch :

Contém os codigos em desenvolvimeto pela equipe. Em geral, todos podem comitar para esse branch, mas nenhum comite deve tornar o código deste branch imcompilável.


### Production Branch:

Contém os codigos que estão (ou ja estiveram) em produção. Esse branch deve ser atualizado apenas pelo responsável do projeto e após cada comite para este branch, deve ser feito o deploy do novo compilado para produção, para que a versão em produção sempre seja a mesma deste branch.


### Feature branches

Estes branches são utilizados sempre quando se deseja alterar uma funcionalidade ou acrescentar uma nova. Por exemplo, adicionar um novo botão em uma página, ou alterar a forma como uma busca é feita. Dessa forma, você será capaz de trabalhar em sua nova funcionalidade sem impactar o branch develop. A rigor, o branch develop continuará recebendo **pulls** e **commits**, independente do progresso da sua feature. 

Uma vez que você concluir seus códigos, será necessário mesclar (fazer um merge) do seu feature branch com o branch develop. Se tiver sorte, ocorrerá um **fast forward** durante a etapa de merge,  significando que o merge ocorreu de forma automática (isso ocorre quando os trechos de código alterados por você não foram modificados por mais ninguém). Caso contrário, você deverá fazer a mesclagem manualmente, nas próximas sessões trataremos melhor de como fazer merge.

Features branches devem ser ramificados a partir do branch develop. Após modificações, os features branches serão mesclados com o branch develop. 
#### Convenção de nome: 
Qualquer coisa exceto **master**, **develop**, __release-*__, ou __hotfix-*__

#### Criação de Feature branches
Para criar um feature branch a partir do develop e já fazer o checkout para ele.

`git checkout -b myFeature develop`

#### Mesclagem de Feature branches com Develop Branch
Após concluir suas atividades, voce deve mesclar o feature branch com o branch develop, para tal:

`git checkout develop`

`git merge –no-ff myFeature`

Feito o merge, o branch myFeature já não é necessário pois o branch develop aponta para o mesmo commit da mesclagem. O parâmetro **–no-ff** se encarrega de gerar um novo commit se o merge automático (fast-forward) ocorrer com sucesso, se não, você precisa corrigir os conflitos da mesclagem manualmente. Para deletar o branch basta usar o comando abaixo.

`git branch -d myFeature`

### Release Branches
Release Branches são utilizados para facilitar o controle de **versão**, no que tange lançamentos de programas (ou deploys). É importante fazer a distinção entre os dois tipos de versão: **Versão do código** e **versão do lançamento**. 

**Versão do código** é feita elegantemente pelo git, registrando todas as modificações feitas em quaisquer partes do código, não é "legível", humanamente falando. 

**Versão de lançamento** adota padrões de versionamento utilizados pela comunidade de software, é de facil compreensão humana e carrega consigo algumas informações importantes sobre a versão. Para saber mais sobre Padrão de Versionamento, [clique aqui](padrao-versionamento).

Release Branches devem ser ramificados a partir do branch develop. Deve ser mesclado com os branches develop e production. 
#### Convenção de nome:
__release-*__

#### Criação de Release branches
Criando um release branch a partir do branch develop e fazendo o checkout para ele.

`git checkout -b release-X.Y.Z develop`

Voce deve trabalhar nesse branch corrigindo erros e pequenos ajustes planejados, conforme citado nos padrões de versionamento. **É proibida criação de grandes features nesse branch.**

`git commit -m “correcao do bug #421”`

#### Mesclagem de Release branches com Develop Branch e Production Branch
Quando voce terminar suas modificações, basta mesclar este branch com os branches develop e production, para tal:

`git checkout develop`

`git merge –no-ff release-X.Y.Z`

`git checkout production`

`git merge –no-ff release-X.Y.Z`

É interessante se criar uma tag no branch product para facilitar o rastreamento das R
releases e também para referências futuras.

`git tag -a X.Y.Z`

O branch release-X.Y.Z já não é necessário pois os branches production e develop já estão apontando para o commit gerado na mesclagem.
Para deletar o branch basta usar o comando abaixo:

`git branch -d release-X.Y.Z`

### Hotfix Branches
Hotfix são necessários quando um bug é encontrado na versão atual de produção e deve ser resolvido imediatamente. Em geral, ele recebe o nome da tag atual da versão **incrementando o último número**(correspontendo à letra **Z** nos exemplos).

Hotfix branches devem ser ramificados a partir do branch production. Após correções, será necessário mescla-lo com os branches develop e production.

#### Convenção de nome:
__hotfix-*__

#### Criação de Hotfix branches
Criando um hotfix branch a partir do branch production e fazendo o checkout para ele.

`git checkout -b hotfix-X.Y.Z product`

Voce deve trabalhar nesse branch corrigindo erros o mais rápido possível. **É proibida criação de grandes features nesse branch**, ao final, comite suas correções:

`git commit -m “correcao do bug #421 hotfix-X.Y.Z”`

#### Mesclagem de Hotfix branches com Develop Branch e Production Branch
Quando voce terminar as correções de erros, basta mesclar este branch com os branches develop e production.

`git checkout develop`

`git merge –no-ff hotfix-X.Y.Z`

`git checkout product`

`git merge –no-ff hotfix-X.Y.Z`

É interessante se criar uma tag no branch product para facilitar o rastreamento e referencias futuras, conforme ocorre nas releases.

`git tag -a X.Y.Z`

Uma vez feito o merge, o branch hotfix-X.Y.Z já não é necessário pois os branches production e develop já estão apontando para o commit gerado na mesclagem. Para deletar o branch basta usar o comando abaixo:

`git branch -d release-X.Y.Z`


## Etapa de Criação do Projeto:

A primeira coisa a ser feita é a criação dos branches fixos de desenvolvimento (develop) e produção (production). Um comportamento característico do GIT ocorre quando se clona um repositório vazio: nenhum branch é criado e o branch master só será criado quando você fizer seu primeiro commit. Para "contornar", prossiga da seguinte maneira:

`nano README.md`

`git add READE.md`

`git commit -m “Create Readme file”`

`git branch develop`

`git branch product`

Após a criação desses branches devemos envia-los ao repositório remoto:

`git push origin develop`

`git push origin product`

Dessa forma, os branches fixos develop e production estão disponíveis no repositório remoto, sendo assim, o branch master faz-se desnecessário. Então devemos excluí-lo do repositório:

`git checkout develop`

`git push origin :master`

## Merge

Para a parte resolver problemas de mesclagem veja o tutorial fornecido pela comunidade Git, clicando [aqui](https://git-scm.com/book/pt-br/v1/Ramifica%C3%A7%C3%A3o-Branching-no-Git-B%C3%A1sico-de-Branch-e-Merge).


## Workflow Básico

![workflow](https://github.com/thxmxx/GIT-Wiki/raw/master/imagens_wiki_git/workflow.jpg)

Esse é o workflow básico que adotamos. Através desse diagrama é possível verificar, visualmente, como é feita a integração entre os branches e commits.

## Tutoriais Externos

[Tutorial GIT-SCM](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows)

[Git Workflow Atlassian](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

[Tutorial Rodrigo Branas](https://www.youtube.com/watch?v=C18qzn7j4SM)

[Tutorial Vincent Driessen](http://nvie.com/posts/a-successful-git-branching-model/)

