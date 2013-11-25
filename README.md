masterhotfixdevel
=================

master hotfix devel approach

## Passo-a-passo:

### Commit parente de todos os branches

Neste caso, commit inicial.

Em caso de projeto começado, última release estável.

    git checkout master
    git add a.txt
    git commit -am "Commit inicial"
    git tag 1.0.0
    git push --tags

### Criando os branches longos a partir do parente

    git checkout -b hotfix
    git push --set-upstream origin hotfix

    git checkout -b devel
    git push --set-upstream origin devel

### Desenvolvendo coisas novas...

Novos desenvolvimentos devem ser feitos aqui.
Ex: features, refactor, etc...

Sempre fazer merge do master para pegar últimas atualizações.

Pode haver hotfix no master, como mostrado logo mais.

Disponibilizar no remote, para ser integrado (Jenkins e equipe).

    git checkout devel
    git merge master
    touch b.txt
    git add b.txt
    git commit -m "Inicia desenvolvimento B"
    git push

    touch b-2.txt
    git merge master
    git add b-2.txt
    git commit -m "Continua desenvolvimento B"
    git push

### Precisa de hotfix em produção...

Hotfixes devem ser feitos aqui.

Merge do master para garantir que está na última release estável.

Commitar em cima dela.

Disponibilizar no remote, para ser integrado (Jenkins e equipe).

Deploy do branch em dev/qa.

Validar aqui com o cliente antes de botar mudanças no master.

    git checkout hotfix 
    git merge master
    touch a-2.txt
    git add a-2.txt
    git commit -m "Conserta A"
    git push

### O hotfix foi homologado pelo cliente...

*IMPORTANTE*: --no-ff (evita fast-forward e força novo commit)

Ir para o master e fazer o merge do hotfix (com --no-ff)

Cria a tag com semântica de fix.

Deploy em dev/qa feito com a tag.

Deploy em produção feito com a tag.

    git checkout master
    git merge hotfix --no-ff
    git tag 1.0.1
    git push --tags

### Continuando desenvolvimento...

Merge do master para garantir que está na última release estável.

Commitar em cima dela.

Disponibilizar no remote, para ser integrado (Jenkins e equipe).

Deploy do branch em dev/qa.

Validar aqui com o cliente antes de botar mudanças no master.

    git checkout devel 
    git merge master
    touch b-3.txt
    git add b-3.txt
    git commit -m "Finaliza desenvolvimento B"
    git push

### Funcionalidade foi aprovada...

*IMPORTANTE*: --no-ff (evita fast-forward e força novo commit)

Análogo a quando disponibilizar um hotfix no master.

Cria a tag com semântica de feature.

Deploy em dev/qa feito com a tag.

Deploy em produção feito com a tag.

    git checkout master 
    git merge devel --no-ff
    git tag 1.1.0
    git push --tags

## Referência:

O esquema descrito neste repositório é uma versão simplificada de
[A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)
