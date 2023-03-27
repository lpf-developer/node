### Comandos GIT para repositórios locais
***

**Iniciar um repositório:**

> git init

**Inserindo nome e email do usuário:**

```bash
git config --global user.name "Fulano de Tal"
git config --global user.email fulanodetal@exemplo.br
```

**Mudar branch master para main:**

> git branch -m master main

* O comando abaixo vai criar uma nova branch `main` no repositório remoto:

> git push -u origin main

**Apagando um repositório:**

> rm -rf .git

**Listando os arquivos modificados:**

> git status

**Desfazendo alterações:**

> git checkout .

* Para arquivos que não estão na área de stage, ou seja, antes da execução do 
  comando `git add`. 

> git clean -df

* Remove os arquivos que estão fora da área de stage.

**Removendo arquivos do Stage:**

> git reset

* Se você executou git add e quer desfazer, use o reset.

**Desfazendo o último commit:**

> git revert HEAD

* Caso você tenha feito alterações e já tenha chegado a realizar um commit, para desfazer é necessário usar o revert.
* Será criado um novo commit indicando que o último commit foi desfeito.
* Esse comando apaga novos arquivos.

**Renomear commit:**

> git commit --amend

* Escreveu algo errado no último commit? Esse comando te permite renomear a 
mensagem do último commit feito.

**Listando Branches (ramos):**

> git branch

* Esse comando lista todas as branches presentes no repositório do seu 
computador.

> $ git branch -a

* Caso você queira que ele liste também as branches que estão no repositório 
remoto, adicione `-a`.

> git checkout minha-branch

* Para mudar para uma outra branch basta usar o comando `checkout`, passando o 
nome da branch.

> git checkout -b minha-nova-branch

* Se você adicionar `-b`, uma nova branch será criada.

**Excluindo branches:**

```bash
git branch -d nome-da-branch
git branch -D nome-da-branch
```
* Para excluir uma branch local basta executar o comando branch com -d ou -D, 
passando o nome da branch que você quer apagar.

* A opção -d é mais segura, pois ela só apaga a branch se você já tiver feito 
merge ou enviado as alterações para seu repositório remoto, evitando perda de 
código.

* A opção -D ignora o estado da sua branch, forçando a sua remoção.

* Esse comando apaga apenas a branch local, não removendo branches remotas.

**Renomeando branches:**

> git branch -m novo-nome-da-branch

Para renomear a sua atual branch local, execute o comando branch com a opção -m, passando o novo nome.

> git branch -m nome-atual novo-nome

Se você estiver em uma branch e quiser renomear outra, você deve passar primeiro 
o nome atual da branch que quer renomear.

**Branch Órfã:**

```bash
          i---j---k     <== branch 'minha branch'
         /
a---b---c---d---h---l   <== branch 'main'
     \         /
      e---f---g         <== branch 'minha outra branch'
	  
1---2---3---4			<== branch `órfã`
```

* Uma branch órfã tem esse nome porque ela não está ligada à branch principal, 
então seus históricos não são compartilhados.

* Isso pode ser útil quando você quer colocar mais de um projeto em um mesmo repositório. Um bom exemplo é quando você tem um projeto no Github e quer criar 
um site para divulgar o seu projeto. A aplicação e o site são coisas diferentes, portanto os códigos deles devem ser versionados separadamente. Ter ambos em um 
mesmo repositório simplifica o gerenciamento.

* Para criar uma branch órfã basta usar o comando:

> git checkout --orphan minha-branch-orfa

**Visualizando o histórico de commits:**

> $ git log

**Histórico de um ou mais arquivos:**

> git log -p meus-arquivos

* Você pode indicar nomes de arquivo ou de um diretório para ver o histórico 
apenas de um grupo de arquivos ao invés do projeto inteiro.

**Histórico de um autor:**

> git log --autor=nome-autor

* Mostra o histórico de commits feitos por uma única pessoa

**Histórico por data:**

```bash
git log --after="MMM DD YYYY"
git log --before="MMM DD YYYY"
```
* Mostra o histórico de commits feitos antes ou após uma data.
* Exemplo do formato usado nas datas: “Jul 07 2019”.

**Histórico baseado em uma mensagem:**

> git log --grep produtos

* Mostra o histórico de commits filtrado por uma mensagem.

```bash
// procurar por "produtos" OU "usuarios"
git log --grep produtos --grep usuarios

// procurar por "produtos" E "usuarios"
git log --grep produtos --and --grep usuarios
```

* Com esse comando teremos o histórico de commits em que a mensagem do commit 
possua a palavra “produtos”. O que passamos pode ser uma expressão regular, e 
podemos passar mais de uma.

**Exibir branches em um modo mais legível:**

> git log --all --decorate --oneline --graph

É possível mandar imprimir o histórico exibindo as branches do repositório com 
algo mais legível e com cores com um comando. Teremos um resultado parecido com 
esse.

```bash
* a102055 (HEAD -> main) commit 8
| * 196d28e (branch-2) commit 7
| * 07e073c commit 3
| * 2b077ca new fie
| | * c1369d8 (branch-3) commit 6
| | * d11bdcd commit 5
| |/
|/|
* | 2b22b75 commit 2
|/
* d5a12b0 .gitignore
* 9535426 -- commit 1
```

* Mnemônico ADOG:
    * -all;
    * -decorate;
    * -online;
    * -graph.

**Atalhos personalizados:**

* Podemos criar atalhos para não ficar escrevendo comandos grandes como o do 
exemplo anterior.
* Para criar atalhos personalizados, basta adicionar uma configuração, passando 
o nome que você quiser para o `alias`.

* Por exemplo, se eu quiser que o comando ensinado anteriormente fosse chamado a 
partir do atalho `dog`:

```bash
//deixar o comando disponível apenas no repositório atual
git config alias.dog "log --all --decorate --oneline --graph"
//deixar o comando global em sua máquina, ficando disponível para qualquer repositório
git config --global alias.dog "log --all --decorate --oneline --graph"
```

* Como os comandos serão do Git, não precisamos ficar chamando-o. Note que o 
comando passado para o atalho não inicia com git.

* Para remover os atalhos basta executar:

```bash
//atalhos locais
git config --unset alias.dog
//atalhos globais
git config --global --unset alias.dog
```

* Agora podemos ter o comando do exemplo anterior apenas executando `git dog`.

**Listando atalhos personalizados:**

> git config -l | grep ^alias\. | cut -c 7- | sort

* Para exibir uma lista de atalhos personalizados, podemos executar o comando 
git config -l, que lista todas as configurações do seu Git. O problema é que 
esse simples comando vai listar todas as configurações. Podemos fazer um comando 
mais sofisticado para ele listar apenas os nossos atalhos personalizados e ainda organizá-los em ordem alfabética:

> git config alias.alias "! git config -l | grep ^alias\. | cut -c 7- | sort"

* O comando é grande, mas tudo bem, pois agora você sabe criar atalhos, não é 
mesmo? Podemos, por exemplo, criar um atalho com o nome `alias`:

* Por comandos como grep e sort não serem do Git, tivemos que iniciar a linha de comando com !. Perceba que por causa disso, nossa primeira instrução teve que 
chamar o Git.

* O $ git config -l lista as configurações do Git. Pegamos o retorno e passamos 
ao comando $ grep, que serve para fazer busca de textos. Como queremos os 
atalhos, que vimos que começa com “alias”, mandamos o grep buscar por tudo que 
começa com alias.. Para termos uma lista mais limpa, usamos o comando cut para 
remover a parte “alias.” do nome dos atalhos. Por fim, usamos o comando sort 
para ordenar nossos atalhos em ordem alfabética.

**Trabalhando em mais de uma coisa sem fazer commit:**

* Pode haver momentos em que você precisa parar o que está fazendo e começar a trabalhar em outra tarefa. Porém, pode não ser bom fazer o commit de algo que 
ainda não foi finalizado para depois voltar nele, resultando em um commit que 
ficará no histórico mas que possui um código que não funciona. Nós podemos 
salvar essas alterações feitas mesmo sem precisar realizar um commit para depois voltar a trabalhar nela, o que é chamado de `Stash` (algo como “esconder” ou “acumular”).

* Ao fazer isso, seu repositório voltará ao estado do último commit, e as 
alterações feitas anteriormente estarão “escondidas”.

**Salvando modificações em um Stash:**

* Simplesmente execute o comando stash.

> git stash

* Você ainda pode colocar um nome nesse stash:

> git stash push -m meu-novo-stash

**Listando Stashes:**

* Você pode fazer vários stashes. Para listá-los, execute o comando:

> git stash list

**Recuperando Modificações:**

* Se algo foi salvo no stash, basta executar o seguinte comando para recuperar 
as alterações que foram jogadas lá:

> git stash apply

* Isso vai recuperar o código do stash mais recente. Se quiser recuperar um 
stash mais antigo, basta ver o número do stash que aparece quando o listamos e 
passar para o seguinte comando:

> git stash apply stash@{2}

**Removendo Stashes:**

* Quando nós recuperamos alterações de um stash, ele continua guardado. Para 
apagá-lo da pilha, execute o comando `drop` junto ao nome do stash que você quer 
remover:

> git stash drop stash@{5}

* Se você quiser recuperar o código de um stash e já apagá-lo, pode usar o 
comando `pop` no lugar do `apply`.

**Juntando alguns pedaços do trabalho:**

* Pode ser que você esteja trabalhando em uma branch e queira fazer o merge do 
código dela com outra branch, mas não quer juntar o trabalho inteiro, apenas um 
commit específico. Isso é possível com o `Cherry Pick`.

> git cherry-pick id-do-commit

### Comandos GIT para repositórios remotos.
***

**Clonando um repositório remoto:**

* Para fazer download de um projeto basta executar o comando $ git clone, 
passando o endereço do repositório. Pode ser Github, Gitlab, Bitbucket, etc.

* Esse comando é bem conhecido, mas ele está aqui por um detalhe que muitas 
pessoas não sabem: por padrão será criada uma pasta com o nome do projeto, mas 
você também pode no final do comando indicar qual o nome da pasta que você quer 
que seja criada.

> git clone https://meu-endereco.com/meu-projeto.git minha-pasta

**Adicionar repositórios remotos:**

* Para ligar o seu repositório local com um repositório remoto, utilize o 
comando `remote add`. Precisamos passar dois parâmetros para esse comando:

    * nome: nome que daremos ao nosso repositório remoto, como se fosse um 
    atalho para não precisarmos ficar escrevendo a URL toda hora. O padrão é 
    usar o nome origin.
    
    * url: endereço do repositório remoto ao qual o nome passado anteriormente 
    vai se referir.

> git remote add origin https://meu-endereco.com/meu-projeto.git

* Caso você queira colocar outro nome ao invés de origin não tem problema. Isso 
pode ser muito útil caso você precise se conectar a mais de um repositório 
remoto. Mas se tiver apenas um, o recomendado é seguir o padrão e usar o nome 
origin.

* Ao adicionar mais de um repositório remoto, as alterações serão enviadas para 
todos. Isso pode ser útil caso você queira armazenar seu código em mais de um 
lugar ao mesmo tempo.

**Visualizar repositórios remotos**

* Esse comando nos mostra o endereço do repositório remoto para o qual estamos enviando nossos códigos.

> git remote -v

* Teremos um retorno como: 

```bash
origin https://meu-endereco/meu-projeto.git (fetch)
origin https://meu-endereco/meu-projeto.git (push)
```

**Excluir repositórios remotos:**

* Pode ser que você não queira mais o seu local repositório conectado a um 
repositório remoto. Esse comando não apaga o repositório, apenas desfaz a 
conexão criada com o comando `git remote add`.

* Nesse exemplo usamos o nome `origin`, mas lembre-se que ali pode ser o nome que 
você deu ao seu repositório remoto. Se você deu um nome diferente de origin, 
lembre-se de usar o comando anterior para listar os repositórios remotos.

> $ git remote rm origin

**Renomear repositórios remotos:**

* Pode ser que você não queira mais o nome que você deu ao seu repositório 
remoto com o comando $ git remote add. Há um comando bem simples para renomear.

> git remote rename nome-atual novo-nome

**Alterar o endereço dos repositórios remotos:**

* Já escreveu o endereço de um repositório remoto errado ou migrou ele para 
outro serviço? Com o comando set-url você será capaz de apenas alterar o 
endereço sem precisar mexer em mais nada. Precisamos passar dois parâmetros para 
esse comando:

    * nome: nome que demos ao nosso repositório remoto, como se fosse um atalho 
    para não precisarmos ficar escrevendo a URL toda hora. O padrão é usar o 
    nome origin.

    * url: novo endereço do repositório remoto.

> git remote set-url origin http://meu-novo-endereco/meu-projeto.git

**Listando branches remotas:**

* Esse comando lista todas as branches presentes no repositório do seu 
computador.

> git branch

* Caso você queira que ele liste também as branches que estão no repositório 
remoto, adicione `-a`:

> git branch -a

**Criando branches remotas:**

* Ao enviar o seu código para uma branch remota que ainda não existe, basta 
executar o `push` com a opção `-u` junto com o nome do repositório remoto e o 
nome da nova branch.

* Após a branch remota estar criada, você poderá executar simplesmente 
`$ git push`.

> git push -u origin minha-branch

**Apagando branches remotas:**

* Para apagar uma branch remota nós fazemos um `push` e adicionamos o 
`--delete`. Entre o `--delete` indicamos o repositório remoto e o nome da branch 
a ser apagada.

> git push origin -d minha-branch

* Também podemos escrever assim: 

> git push origin :minha-branch

**Renomeando branches remotas:**

* Vimos no post anterior que para renomear uma branch local executamos:

> git branch -m nome-atual novo-nome

* Após renomear a sua branch local, basta apagar a branch remota com o nome 
antigo e fazer um push com a branch com o novo nome:

> git push origin :nome-atual novo-nome

* Para terminar de ligar a branch local com a remota, entre na branch com o novo 
nome e execute:

> git push origin -u novo-nome

**Achando o culpado:**

* Deu problema e estão dizendo que foi você? Não mais! Com o comando blame você 
pode ver quem alterou cada linha de um arquivo.

> git blame nome-do-arquivo

* Para não ficar muito grande, podemos usar `-w` para ignorar espaços em branco 
e usar `-L` para indicar um intervalo de linhas a serem exibidas.

> git blame -w -L 1,12 nome-do-arquivo

* E ainda podemos usar `-e` para que seja exibido o email ao invés do nome do 
usuário.

**Compartilhamento Offline/Local**

* Podemos ter repositórios remotos que não estão na nuvem, como Github, Gitlab, 
ou Bitbucket. Podemos fazer com que um computador em nossa rede seja o 
responsável por armazenar o código e receber o push de todos os usuários. 
Isso é útil principalmente em empresas que possuem uma política mais rígida com 
a segurança de suas informações e não permitem que seus códigos sejam 
armazenados fora de seus próprios servidores.

* Outro uso para isso é quando adicionamos mais de um repositório remoto. 
Você pode continuar fazendo commits para o Github e ao mesmo tempo ir 
armazenando uma cópia em um pendrive.

* Primeiro, no local onde teremos o nosso repositório “servidor” (que receberá 
os pushes), iniciamos um repositório junto com --bare. Neste repositório você 
não poderá editar arquivos ou fazer commits, ele só permite receber pushes.

> git init --bare

* Se você iniciou, por exemplo, um repositório em uma pasta dentro de um 
pendrive com o caminho `E:\meu-projeto`, basta clonar com o comando:

> git clone E:\meu-projeto

* Ou então, como já vimos, podemos adicionar esse repositório na nossa lista de repositórios remotos, permitindo que nossos commits sejam enviados para algum 
lugar como o Github e para o pendrive ao mesmo tempo:

> git remote add usb E:\meu-projeto

* Nesse exemplo demos o nome usb ao invés de origin. Lembre-se que você pode dar qualquer nome.

* Do mesmo jeito que fizemos um repositório em um pendrive, você pode fazer o 
mesmo em um outro computador na sua rede. Assim todos os usuários em sua rede 
poderão usar este computador como repositório remoto.


### Git Merge e Git Rebase: quando usá-los? 
***

O Git é uma ferramenta de controle de versão que facilita muito o trabalho das 
equipes de desenvolvimento. Muitos desenvolvedores utilizam o Git para realizar 
o controle dos artefatos de código que vão sendo gerados ao longo do tempo. E, certamente, este controle envolve administrar os possíveis conflitos em arquivos quando dois ou mais desenvolvedores alteram o mesmo trecho de código ao mesmo 
tempo. Nesse tipo de situação, temos o famoso e temido “merge”, onde precisamos mesclar as alterações de todos os desenvolvedores, de modo que nenhum deles 
perca seu trabalho.

Quando falamos exclusivamente sobre o Git, nós temos duas maneiras de fazermos 
este trabalho de “mistura” de código: utilizando o comando rebase ou utilizando 
o comando merge. Vamos verificar nesse artigo as diferenças entre estes dois 
comandos e quando é a melhor hora de usar cada um. Ambos os comandos resolvem o 
mesmo problema, porém, de maneiras diferentes.

**O que é o git merge?**

Vamos imaginar que você precisa começar a trabalhar em uma tarefa dentro de um 
projeto controlado pelo Git. Se você seguir corretamente o Git Flow, você 
precisará criar um branch para que você consiga trabalhar em sua tarefa.

À medida que você for trabalhando na sua tarefa, você provavelmente irá gerar 
vários commits em seu branch. 

Até aí, tudo ocorrendo na normalidade. Porém, o grande problema que podemos 
enfrentar é quando o branch master em nosso cenário fica “dessincronizado” com 
relação ao branch da nossa funcionalidade. Essa dessincronização pode acontecer 
por uma situação bem comum: outras pessoas mexeram no branch master enquanto trabalhávamos no branch da nossa tarefa. E a grande confusão vem do fato que o 
branch da nossa tarefa também foi gerado através do master, porém, em um momento anterior destas alterações.

Nós precisamos, de alguma maneira, misturar os commits do branch da nossa tarefa 
com os commits posteriores que foram feitos no branch master, quando este for “fundido” novamente. Uma das maneiras de se fazer isso é justamente utilizar o 
git merge.

O merge basicamente cria um novo commit no branch onde o merge é realizado. Este commit puxa consigo a última referência do branch a partir do qual o merge é realizado. Este commit “especial” é chamado de merge commit. Supondo então que 
você rode os comandos abaixo:

```bash
git checkout feature # indo para o branch da feature
git merge master     # fazendo o merge entre o feature e o master

```
O merge é legal principalmente porque ele não altera os branches envolvidos. Na ilustração anterior, você pode perceber que tanto o branch feature quanto o 
branch master não são gerados. O master nem teve suas estruturas envolvidas na operação, enquanto o branch feature teve somente um commit adicional.

O fato de a estrutura dos branches envolvidos não ser diretamente modificada 
reduz a possibilidade de haver problemas durante a operação de merge, mas também 
cria um commit adicional “esquisito” a cada operação. Esse commit adicional pode prejudicar a leitura do histórico dos commits através do git log, principalmente 
para quem ainda não está tão ambientado ao Git e seus conceitos.


**O que é git rebase?**

Vamos, mais uma vez, considerar a situação na qual os branches feature e master 
estão “dessincronizados” e precisam ser misturados. Vamos relembrar a ilustração 
que mostra esta situação.

Nós também podemos resolver esta situação através do rebase. O rebase 
literalmente unifica os branches envolvidos, puxando os commits para frente do 
branch de destino. É como se ele estivesse “refazendo” a base do branch onde o 
comando é executado.

Sendo assim, se executarmos os comandos abaixo:

```bash
git checkout feature # indo para o branch da feature
git rebase master    # fazendo o rebase entre o feature e o master
```

Pela ilustração acima, podemos ver que algo legal que o rebase faz é produzir um histórico linear, mais limpo e mais fácil de ser lido, pois os branches são literalmente fundidos. Pela fusão, também não é gerado aquele commit adicional “estranho” que acontece no merge.

Agora, o grande problema é que o rebase mexe com toda a estrutura dos branches envolvidos, reescrevendo inclusive o histórico de commits destes branches. Se 
este processo de reescrita não for bem executado, podem ocorrer vários problemas 
no histórico dos branches envolvidos, causando até mesmo perda de trabalho 
durante o processo de mesclagem. Existe também o ponto de que, pelo fato de o 
rebase não gerar o merge commit, você não consegue ter a “rastreabilidade” de 
quando dois branches de fato foram fundidos, já que o rebase gera um branch 
linear no final do processo.

**Quando usar o git merge e quando utilizar o rebase?**

Ambos os comandos são muito úteis, porém, em situações diferentes. Quando 
seguimos corretamente o Git Flow, existe uma regra que chamamos de “Golden Rule 
of Rebasing”. Basicamente, essa regra diz que o rebase não deve ser utilizado em branches públicos, já que ele tem um alto potencial catastrófico e destrói o 
histórico de commits, causando sempre divergências entre os branches locais e os branches remotos. Porém, existe um fluxo de trabalho muito legal que pode ser utilizado, combinando ambos os comandos.

Vamos voltar à nossa situação inicial: você precisa desenvolver uma tarefa. Você provavelmente irá gerar um novo branch para desenvolver sua tarefa a partir do 
master. Podemos ter então o comando abaixo:

> git checkout –b feature # criando o branch de trabalho

Agora chega a hora de integrarmos nossos commits ao master. Nós precisamos fazer 
isso em duas vias, basicamente:

1) Trazer as alterações que foram inseridas no master posteriormente para dentro 
de nosso branch. Precisamos deste passo para garantir que as alterações 
posteriores não irão “quebrar” as alterações que fizemos em nosso branch;

2) Levar as alterações do nosso branch para o master, atualizando-o com o nosso trabalho e o disponibilizando para os demais desenvolvedores.

Vamos tratar do primeiro passo neste momento. Se pararmos para analisar a 
situação, faz mais sentido trazer os commits de master para feature de maneira “transparente”, ou seja: sem a necessidade de um commit adicional. Isso vai 
manter o nosso histórico completamente linear e irá garantir que os novos 
commits advindos do master serão aplicados a nosso branch no “momento correto”, preservando a ordem no qual eles foram gerados. Por isso, para esta primeira 
etapa, o rebase faz muito mais sentido. Sendo assim, supondo que já estejamos no branch feature, podemos executar o comando abaixo:

> git rebase master

O primeiro passo foi concluído! Nós temos o nosso branch feature devidamente sincronizado. Porém, nosso branch master, que é o branch principal, ainda está defasado, pois ele ainda não possui os nossos commits. Nós precisamos puxar 
nossos commits do branch feature para o branch master. Como estamos falando do 
branch principal, é importante mantermos a rastreabilidade do processo de gestão 
do código, deixando claro inclusive quando os commits de branches locais foram 
puxados para o branch master.

Por isso, para essa segunda etapa, o merge é muito mais interessante do que o 
rebase. Nesta situação, todos os possíveis problemas de “mistura” dos dois 
branches (como conflitos) foram resolvidos durante o processo de rebase. Nesta 
segunda etapa, nós podemos simplesmente trocar o ponteiro do nosso branch 
master, apontando-o para o último commit do nosso branch feature. Quando esse 
processo acontece, nós chamamos esta estratégia de merge de fast-foward. O 
fast-foward é possível quando não existem conflitos entre os branches envolvidos 
e quando o branch de desenvolvimento está à frente do branch principal. E, pela ilustração anterior, é exatamente esta a situação.

Portanto, se executarmos os comandos abaixo:

```bash
git checkout master # indo para o branch do master
git merge feature    # fazendo o merge entre o master e o feature
```

Veja que, dessa maneira, temos o melhor dos dois mundos: não temos o histórico 
de commits poluído pelos commits secundários no branch feature (graças ao 
rebase) e temos a rastreabilidade do momento onde o branch master foi modificado 
por uma integração (por causa do merge).















