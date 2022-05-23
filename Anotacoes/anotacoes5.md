## BLOBS

## TREES

## COMMITS

São os 3 tipos básicos de objetos no git responsáveis pelo versionamento do nosso código.

### **BLOBS**

```sh
echo 'conteudo' | git hash-object --stdin
> fc31e91b26cf85a55e072476de7f263c89260eb1

echo -e 'conteudo' | openssl sha1
> 65b0d0dda479cc03cce59528e28961e498155f5c
```

No exemplo acima, usamos a função echo para pegar uma string e mostrar o output dessa string, e vamos passar esse output(que é 'conteudo' no caso) para uma função do git que é hash-object. A flag --stdin é apenas porque essa função espera receber um arquivo e estamos enviando texto, para que ela entenda isso. Essa função vai nos devolver o SHA1 desse conteúdo.

O segundo exemplo é a mesma coisa só que usando o "openss1 sha1". Ele gerou um outro tipo de SHA. Porque isso? Isso acontece porque esse objetos específicos do git e o jeito que ele os manipula é através de objetos. Os arquivos ficam guardados dentro desses objetos chamado BLOB e esses objetos contém metadados dentro dele.

![1](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/5_1.png)

Então o objeto "BLOB" contém o tipo do objeto (Blob), o tamanho dessa string ou arquivo (Tamanho 42), uma barra contrária com 0 (\0) e o conteúdo de fato desse arquivo (Ola Mundo). A partir disso, conseguimos entender o por quê de não ter sido iguais os SHAs.

A partir disso podemos fazer:

```sh
echo 'conteudo' | git hash-object --stdin
> fc31e91b26cf85a55e072476de7f263c89260eb1

echo -e 'blob 9\0conteudo' | openssl sha1
> fc31e91b26cf85a55e072476de7f263c89260eb1
```

Passando os metadados o SHA é identico ao gerado pelo método git. Podemos compreender que o git armazena metadados dentro dos objetos.

*(Vide exemplos VM)

**TREES**

As TREEs armazenam BLOBs. A árvore também contém metadados. Ela contém \0, aponta para um blog que por sua vez tem um sha1. Ela também guarda o nome desse arquivo. O blog não guarda o nome do arquivo, ele só guarda o SHA do arquivo e só. O Blob é o bloco básico de composição. A árvore vai ser responsável por montar toda a estrutura de ondem que estão localizados esses arquivos. As árvores podem apontar tanto para blobs (que são arquivos) ou outras árvores. Isso é assim porque os diretórios dentro de um SO podem conter outros diretórios, sendo assim faz sentido que o git use um tipo de objeto recursivo que são as árvores. Sendo assim uma árvore pode aponter para outra árvore da mesma forma que um diretório pode ter outro diretório dentro. Por sua vez, a árvore tem um SHA1 desse metadado.

![2](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/5_2.png)

Os BLOBs (bolhas) tem o SHA1 do arquivo, as TREEs (árvores) apontam para esses BLOBs e tem um SHA1 encriptado os metadados das árvores. Estão se mudar uma "," em um arquivo ao qual essa árvore esta apontando, quando ela for gerar o SHA1 desses metadados, o SHA1 da bolha em si vai ter mudado, que consequentemente vai refletir no SHA1 da árvore. Uma coisa esta relacionada com a outra sempre.

Abaixo vemos o gráfico que mostra que as árvores contém a informação de quais arquivos que ela esta apontando (README, Rakefile e lib) e elas apontam para BLOBs e para TREEs que podem apontar para outras bolhas (BLOBs). O BLOB é um objeto que encapsula esse comportamento de diretórios, ele é usado para apontar para diretórios que contém arquivos e por consequência apontar para arquivos também.

![3](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/5_3.png)

Fonte: https://git-scm.com/

**COMMITS**

O objeto mais importante de todos:

![4](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/5_4.png)

O SHA1 desse commit é o hash de toda a informação.

O COMMIT é o objeto que vai juntar tudo e dar sentido para a alteração que você esta fazendo. Ele aponta para um árvore, aponta para um parente (o último commit realizado antes dele), aponta para um autor, aponta para um mensagem também (autor e mensagem faz parte dessa idéia de sentido). O que esses arquivos representados pelos BLOBs e dentro dessas pastas representados pelas árvores querem dizer? Ela significa uma alteração. Então você pode escrever uma mensagem nesse objeto chamado commit, que explicará e dará significado para esse monte de arquivo dentro desse monte de pastas. Esse objeto leva também o nome do autor. Esses commits também tem um timestamp que é um carimbo de tempo.

A parte genial de tudo é que os commits também possuem SHA1 (encriptação), a geração desse hash identificador dos seus metadados. Isso significa que se você alterar uma BLOB, ou seja, um dado dentro do arquivo, ele vai gerar um SHA1 daquela BLOB. Essa BLOB tem uma árvore apontando para ela, então se você alterar lá, vai alterar também os metadados daquela árvore, porque aquela árvore aponta para uma BLOB. E o commit aponta para uma árvore, que por sua vez pode apontar para outras árvores. Então se você mudar qualquer coisa em um arquivo isso vai refletir na árvore que por consequência vai refletir no seu commit. Por isso o git é tão confiável. Quando você tem um commit, você esta garantindo que ninguém alterou aquele commit. Se você olhar o histórico de commits você monta uma linha do tempo de como os commits foram realizados. Não tem como uma pessoa agir maliciosamente tentando alterar o código de um respectivo commit ou arquivo sem que isso fique muito claro dentro do histórico de commits.

![5](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/5_5.png)

Fonte: https://git-scm.com/

**Sistema Distribuído Seguro**

Porque Git é um sistema distribuído seguro? O sistema é distribuído pelo motivo de além de você ter seu código hostiado na núvem(GitHub) no estado final do seu código(versão recente e mais atualizada), você também tem várias pessoas(x maintainers) desenvolvendo o código com versões confiáveis em suas máquinas, caso a nuvem caia. Essas pessoas (maintainers) terão uma cópia confiável do software(commits são praticamente impossíveis de serem alterados devido a forma que estão encadeados) em suas máquinas. É confiável por causa da estrutura que o Git mantém e da forma que ele foi projetado. 