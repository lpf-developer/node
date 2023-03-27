Configuração inicial

```bash
git config –global user.name “Seu nome”
git config –global user.email “Seu email”
```

Novo projeto Git

> git init

Novo projeto Git com um nome específico

> git init <nome do repositório>

Clonar um repositório web

> git clone <url do repositório>

Adicionar arquivos ao repositório (adicionar todos os arquivos)

> git add . 

Versionando arquivos (adicionar e comitar)

> git commit -a 

Versionando arquivos (adicionar mensagem)

> git commit -m "mensagem descritiva"

Trabalhando com ramificações 

```bash
git branch # Lista todas as ramificações
git branch <nome da ramificação> # Cria uma ramificação com um nome específico
git branch -d <nome da ramificação> # Elimina a ramificação especificada
git checkout <nome_do_branch> # Alterna entre as ramificações
git checkout -b <nome_do_branch_novo> # Cria e alterna para uma nova ramificação
```

Ligação entre repositórios (local e remoto)

> git remote add <nomecurto> <url>

Copiando arquivos entre repositórios (local e remoto)

```bash
# É importante especificar a origem e o upstream antes de usar o git push.
git push –set-upstream <nome_curto> <nome_do_branch>

git push -u <nome_curto> <nome_do_branch>
```

Avaliando versões

* Quando você precisa baixar as mudanças criadas por outros membros do seu 
projeto colaborativo, você precisa do comando Git fetch. A partir desse comando, 
você irá receber todas as informações de commits, para avaliar, antes de aplicar 
essas alterações na sua versão local do repositório.

> git fetch

Atualizando o repositório local com o conteúdo remoto

* O comando Git pull baixa o conteúdo (não os metadados) do que foi alterado no repositório remoto para o seu repositório local e imediatamente atualiza seu 
contreúdo para a última versão.

> git pull <url>

Escondendo arquivos

* Armazena temporariamente seus arquivos modificados em uma área chamada stash (“esconderijo”), sem interagir com os outros arquivos até ser necessário.

```bash
git stash
git stash list # Lista todos os esconderijos
git stash apply # Aplica o conteúdo do stash a um branch
```

Commit detalhado

* Quer detalhes específicos sobre um commit que o log não mostra? O comando Git 
show é a resposta.

> git show <hash_do_commit>

Removendo arquivos do diretório git

> git rm <nome do arquivo>

Ajuda com comandos

> git help <nome do comando>

Integração de arquivos

* Integra as mudanças de dois branches diferentes em um único branch. Ele 
precisa ser iniciado a partir de um branch já selecionado, que será mesclado com outro, com o nome passado por parâmetro.

> git merge <nome_do_branch>

